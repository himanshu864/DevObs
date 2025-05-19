#python 

Okay, let's implement the DNS Resolver with TTL Caching in Python using only standard libraries as required.

This code will:

1. Build a raw DNS query packet.
2. Send it using UDP sockets.
3. Parse the raw DNS response packet.
4. Extract IPv4 addresses and TTL.
5. Implement a simple in-memory cache with TTL expiry.

Python

```python
import socket
import struct
import random
import time
import sys

# --- Cache ---
# Structure: { 'hostname': {'ips': ['ip1', 'ip2'], 'expiry_time': timestamp} }
DNS_CACHE = {}

# --- Constants ---
DNS_SERVER_IP = "8.8.8.8"  # Google's Public DNS
DNS_PORT = 53
QUERY_TIMEOUT = 2  # seconds
BUFFER_SIZE = 1024

# DNS Query Types
TYPE_A = 1
# DNS Query Classes
CLASS_IN = 1

def encode_dns_name(domain_name):
    """Encodes a domain name in the DNS format (e.g., www.google.com -> 3www6google3com0)"""
    encoded = b''
    for label in domain_name.encode('ascii').split(b'.'):
        encoded += struct.pack('!B', len(label)) + label
    return encoded + b'\x00' # Null byte to terminate the name

def parse_dns_name(reader):
    """
    Parses a potentially compressed DNS name from a response.
    'reader' is an object with read(n) and tell() methods, and a 'data' attribute.
    Returns the decoded name (str) and the number of bytes originally consumed
    from the reader's position *before* pointer jumps.
    """
    parts = []
    bytes_consumed_original = 0
    jumped = False
    expected_end_offset = -1 # Track end offset after first jump

    while True:
        length_byte = reader.read(1)
        if not length_byte:
            raise EOFError("Reached end of data while parsing name.")

        length = length_byte[0]
        if not jumped:
             bytes_consumed_original += 1

        # Check for pointer (compression)
        if (length & 0xC0) == 0xC0:
            if not jumped:
                # This is the first jump, remember where we should be after the pointer
                expected_end_offset = reader.tell() + 1 # +1 because we need to read the second byte of the pointer
                jumped = True

            pointer_byte2 = reader.read(1)
            if not pointer_byte2:
                 raise EOFError("Reached end of data while parsing name pointer.")
            if not jumped: # This check is redundant now but kept for clarity
                 bytes_consumed_original += 1

            offset = ((length & 0x3F) << 8) | pointer_byte2[0]
            # Create a new reader for the jump
            import io
            jump_reader = io.BytesIO(reader.data)
            jump_reader.seek(offset)
            # Recursively parse the name at the pointer location
            parts.append(parse_dns_name(jump_reader)[0]) # Only need the name part from recursive call
            # If this was the first jump, the parsing for this name is complete.
            # Return the combined name and the original bytes consumed (usually 2 for the pointer).
            return ".".join(parts), bytes_consumed_original

        # End of name marker
        elif length == 0:
            break

        # Normal label
        else:
            if not jumped:
                bytes_consumed_original += length
            label = reader.read(length)
            if len(label) < length:
                 raise EOFError("Reached end of data while reading label.")
            parts.append(label.decode('ascii'))

    # If we never jumped, the total bytes consumed is correct
    # If we did jump, the original_bytes_consumed is set before the first jump (usually 2)
    return ".".join(parts), bytes_consumed_original


def build_dns_query(hostname, query_type=TYPE_A):
    """Builds a DNS query packet for the given hostname and type."""
    transaction_id = random.randint(0, 65535)

    # Header section (12 bytes)
    # Pack format: ! signifies network byte order (big-endian)
    # H = unsigned short (2 bytes)
    flags = 0x0100  # Standard query (Recursion Desired RD=1)
    qdcount = 1     # Question count
    ancount = 0     # Answer count
    nscount = 0     # Authority count
    arcount = 0     # Additional count

    header = struct.pack('!HHHHHH', transaction_id, flags, qdcount, ancount, nscount, arcount)

    # Question section
    qname = encode_dns_name(hostname)
    qtype = struct.pack('!H', query_type)
    qclass = struct.pack('!H', CLASS_IN)

    query = header + qname + qtype + qclass
    return query, transaction_id

def parse_dns_response(response_bytes, expected_id):
    """Parses the DNS response packet and extracts A records and TTL."""
    try:
        # --- 1. Parse Header ---
        header_struct = struct.Struct('!HHHHHH')
        if len(response_bytes) < header_struct.size:
             print("Error: Response too short for header.")
             return None, None

        header = header_struct.unpack(response_bytes[:header_struct.size])
        resp_id, flags, qdcount, ancount, nscount, arcount = header

        # Verify Transaction ID
        if resp_id != expected_id:
            print(f"Error: Transaction ID mismatch. Expected {expected_id}, got {resp_id}")
            return None, None

        # Check flags (QR=1 for response, RCODE=0 for no error)
        is_response = (flags & 0x8000) >> 15
        opcode = (flags & 0x7800) >> 11
        authoritative = (flags & 0x0400) >> 10
        truncated = (flags & 0x0200) >> 9
        recursion_desired = (flags & 0x0100) >> 8
        recursion_available = (flags & 0x0080) >> 7
        rcode = flags & 0x000F

        if not is_response:
            print("Error: Received packet is not a response.")
            return None, None
        if rcode != 0:
            print(f"Error: DNS server returned error code {rcode}")
            return None, None
        if truncated:
             print("Warning: Response was truncated. Results may be incomplete.")
             # We could handle this by retrying with TCP, but that's beyond the scope here.

        # --- 2. Setup Reader and Skip Question Section ---
        import io
        reader = io.BytesIO(response_bytes)
        reader.data = response_bytes # Store full data for pointer jumps
        reader.seek(header_struct.size) # Move past the header

        for _ in range(qdcount):
            # Parse and discard the question name
            qname, name_bytes_len = parse_dns_name(reader)
            # Skip QTYPE (2 bytes) and QCLASS (2 bytes)
            reader.seek(reader.tell() + 4)


        # --- 3. Parse Answer Section ---
        ips = []
        min_ttl = float('inf')

        if ancount == 0:
            print("No answer records found.")
            # This might be valid (e.g., NXDOMAIN), but for this assignment we seek A records.
            # We could parse Authority section for SOA record's negative caching TTL if needed.
            return None, None

        for _ in range(ancount):
            current_pos = reader.tell()
            # Parse name (often compressed)
            ans_name, name_bytes_len = parse_dns_name(reader)

            # Read the fixed part of the Resource Record (RR) header (10 bytes)
            # HHIH = Type (2), Class (2), TTL (4), RDLength (2)
            rr_header_struct = struct.Struct("!HHIH")
            rr_header_bytes = reader.read(rr_header_struct.size)
            if len(rr_header_bytes) < rr_header_struct.size:
                 print("Error: Truncated answer RR header.")
                 break
            rr_type, rr_class, rr_ttl, rdlength = rr_header_struct.unpack(rr_header_bytes)

            # Read the RDATA
            rdata = reader.read(rdlength)
            if len(rdata) < rdlength:
                 print("Error: Truncated answer RDATA.")
                 break

            # Process A records (IPv4)
            if rr_type == TYPE_A and rr_class == CLASS_IN:
                if rdlength == 4: # Standard IPv4 length
                    ip_address = socket.inet_ntoa(rdata) # Convert 4 bytes to dotted decimal string
                    ips.append(ip_address)
                    min_ttl = min(min_ttl, rr_ttl)
                    # print(f"  Found A record: {ans_name} -> {ip_address} (TTL: {rr_ttl})") # Debug
                else:
                    print(f"Warning: Found A record with unexpected data length {rdlength}")
            # else: # Debugging for other record types
                # print(f"  Skipping RR type {rr_type}, class {rr_class} for {ans_name}")


        if not ips:
            print("No valid A records found in the answer section.")
            return None, None

        # Ensure we got a valid TTL
        if min_ttl == float('inf'):
             print("Warning: Could not determine a valid TTL for A records.")
             # Decide on a default behavior: maybe return None or a default small TTL?
             # For simplicity, let's treat this as failure to get a cacheable result.
             return ips, None


        return ips, min_ttl

    except EOFError as e:
        print(f"Error parsing response: Ran out of data. {e}")
        return None, None
    except struct.error as e:
        print(f"Error unpacking data: {e}")
        return None, None
    except Exception as e:
        print(f"An unexpected error occurred during parsing: {e}")
        import traceback
        traceback.print_exc()
        return None, None


def resolve(hostname, use_cache=True):
    """
    Resolves a hostname to an IP address using manual DNS query and caching.
    """
    global DNS_CACHE
    current_time = time.time()

    # --- 1. Check Cache ---
    if use_cache and hostname in DNS_CACHE:
        cache_entry = DNS_CACHE[hostname]
        if cache_entry['expiry_time'] > current_time:
            print(f"Cache HIT for {hostname}. Returning cached IPs: {cache_entry['ips']}")
            return cache_entry['ips']
        else:
            print(f"Cache EXPIRED for {hostname}.")
            del DNS_CACHE[hostname] # Remove expired entry
    elif use_cache:
        print(f"Cache MISS for {hostname}.")

    # --- 2. Build Query ---
    print(f"Building query for {hostname}...")
    query_bytes, query_id = build_dns_query(hostname)

    # --- 3. Send Query via Socket ---
    sock = None
    try:
        sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
        sock.settimeout(QUERY_TIMEOUT)

        print(f"Sending query to {DNS_SERVER_IP}:{DNS_PORT}...")
        sock.sendto(query_bytes, (DNS_SERVER_IP, DNS_PORT))

        # --- 4. Receive Response ---
        print("Waiting for response...")
        response_bytes, server_address = sock.recvfrom(BUFFER_SIZE)
        print(f"Received {len(response_bytes)} bytes from {server_address}")

    except socket.timeout:
        print(f"Error: Request timed out for {hostname}")
        return None
    except socket.error as e:
        print(f"Error: Socket error for {hostname}: {e}")
        return None
    finally:
        if sock:
            sock.close()

    # --- 5. Parse Response ---
    print(f"Parsing response for query ID {query_id}...")
    ips, ttl = parse_dns_response(response_bytes, query_id)

    # --- 6. Update Cache ---
    if ips and ttl is not None and ttl > 0:
        expiry_time = current_time + ttl
        DNS_CACHE[hostname] = {
            'ips': ips,
            'expiry_time': expiry_time
        }
        print(f"Cached result for {hostname}: IPs={ips}, TTL={ttl}s (Expires at {time.ctime(expiry_time)})")
        return ips
    elif ips:
         # Got IPs but no valid TTL for caching
         print(f"Resolved {hostname} to {ips} but could not cache (invalid TTL).")
         return ips
    else:
        print(f"Failed to resolve {hostname}.")
        return None


# --- Main Execution Example ---
if __name__ == "__main__":
    host_to_resolve = "www.google.com"
    if len(sys.argv) > 1:
        host_to_resolve = sys.argv[1]

    print(f"--- Resolving {host_to_resolve} (1st time) ---")
    result1 = resolve(host_to_resolve)
    if result1:
        print(f"Resolved IPs: {result1}")
    print("-" * 20)

    print(f"--- Resolving {host_to_resolve} (2nd time - testing cache) ---")
    result2 = resolve(host_to_resolve)
    if result2:
        print(f"Resolved IPs: {result2}")
    print("-" * 20)

    # Example to test TTL expiry (if TTL is short enough)
    if result1 and host_to_resolve in DNS_CACHE:
        ttl_value = DNS_CACHE[host_to_resolve]['expiry_time'] - time.time()
        print(f"Cached TTL is approx {ttl_value:.0f}s. Waiting for slightly longer...")
        if ttl_value < 60: # Only wait if TTL is reasonably short
            wait_time = ttl_value + 2
            print(f"Sleeping for {wait_time:.0f} seconds...")
            time.sleep(wait_time)
            print(f"--- Resolving {host_to_resolve} (3rd time - after waiting for expiry) ---")
            result3 = resolve(host_to_resolve)
            if result3:
                print(f"Resolved IPs: {result3}")
            print("-" * 20)
        else:
            print("TTL is too long to demonstrate expiry in this example.")

    print("--- Resolving another host (cloudflare.com) ---")
    result4 = resolve("cloudflare.com")
    if result4:
        print(f"Resolved IPs: {result4}")
    print("-" * 20)

    print("--- Cache contents ---")
    print(DNS_CACHE)
```

**How to Run:**

1. Save the code as a Python file (e.g., `dns_resolver.py`).
2. Run from your terminal: `python dns_resolver.py`
3. You can optionally provide a hostname as a command-line argument: `python dns_resolver.py example.com`

**Explanation:**

1. **Cache:** A simple dictionary `DNS_CACHE` stores results.
2. **`encode_dns_name`:** Converts standard hostnames into the required DNS label format (e.g., `3www6google3com0`).
3. **`parse_dns_name`:** This is crucial for reading names from the response. It handles the pointer/compression mechanism (where parts of a name point to earlier occurrences in the packet to save space). It carefully tracks the reader's position.
4. **`build_dns_query`:** Creates the byte sequence for a standard DNS 'A' record query, including a random Transaction ID, flags, and the encoded hostname.
5. **`parse_dns_response`:**
    - Unpacks the header and verifies the Transaction ID and flags.
    - Uses the `parse_dns_name` helper to skip the Question section.
    - Loops through the Answer Records (RRs) indicated by `ancount`.
    - For each RR, it parses the (potentially compressed) name.
    - It unpacks the RR type, class, TTL, and data length.
    - If it's an 'A' record (Type 1, Class 1) and the data length is 4, it uses `socket.inet_ntoa` to convert the RDATA bytes into an IP address string.
    - It keeps track of the _minimum_ TTL found among the relevant A records, as the cache entry should expire when the shortest TTL expires.
6. **`resolve`:**
    - Checks the cache first (if `use_cache` is True).
    - If not cached or expired, it calls `build_dns_query`.
    - Creates a UDP socket, sends the query, and waits for the response (with a timeout).
    - Calls `parse_dns_response`.
    - If successful, updates the cache with the IPs and calculated expiry time.
    - Returns the list of IPs or `None` on failure.
7. **`if __name__ == "__main__":`:** Contains example usage demonstrating resolution, cache hits, and potentially cache expiry.

---
# THEORY

Okay, let's break down the theory behind the Python DNS resolver we built.

**1. What is DNS? (The Big Picture)**

- **Analogy:** Think of DNS (Domain Name System) as the **phonebook of the Internet**.
- **Problem:** Humans remember website names like `www.google.com`, but computers connect to each other using numerical IP addresses (like `172.217.167.196`).
- **Solution:** DNS is the system that translates the human-friendly domain names into the computer-friendly IP addresses. When you type a website address in your browser, your computer (usually) performs a DNS lookup behind the scenes to find the correct IP address to connect to.

**2. The Core Process: Query and Response**

DNS works on a simple question-and-answer model:

- **Client (Your Resolver):** Needs the IP address for a hostname.
- **DNS Server:** Knows (or can find) the answers.
- **Query:** The client sends a **DNS Query packet** to the server asking, "What is the IP address (A record) for `www.google.com`?"
- **Response:** The server sends back a **DNS Response packet** saying, "The IP address for `www.google.com` is `172.217.167.196`, and you can consider this information valid for X seconds (the TTL)."

**3. DNS Packet Structure (The Message Format)**

Both Query and Response packets follow a specific binary format (defined mainly in RFC 1035). They aren't plain text. Our Python code manually constructs and interprets this binary format using the `struct` module.

- **Header (12 bytes):** Present in both queries and responses. Contains metadata:
    
    - **Transaction ID (ID):** A random 16-bit number chosen by the client. The server copies this ID into the response so the client can match responses to its queries.
    - **Flags:** A set of bits indicating:
        - Is this a query (0) or response (1)?
        - Is it a standard query? (Opcode)
        - Should the server attempt recursion (try to find the answer fully)? (RD - Recursion Desired, set in query)
        - Is recursion available at the server? (RA - Recursion Available, set in response)
        - Was there an error? (RCODE - Response Code, 0 means success)
        - And others (Authoritative Answer, Truncated, etc.)
    - **Counts:** Number of entries in the following sections (Question, Answer, Authority, Additional).
- **Question Section:** Contains the actual question being asked.
    
    - **QNAME (Query Name):** The hostname being looked up (e.g., `www.google.com`). This name is encoded in a special format (see below).
    - **QTYPE (Query Type):** What kind of record is being asked for? `1` (or `TYPE_A`) means an IPv4 address. Other types exist (AAAA for IPv6, MX for mail servers, etc.).
    - **QCLASS (Query Class):** Usually `1` (or `CLASS_IN`) for Internet addresses.
- **Answer Section (Mainly in Responses):** Contains the Resource Records (RRs) that answer the question. Each RR typically includes:
    
    - **NAME:** The hostname this answer pertains to (often uses compression, see below).
    - **TYPE:** The record type (e.g., `1` for 'A').
    - **CLASS:** The class (e.g., `1` for 'IN').
    - **TTL (Time To Live):** **Crucial for caching.** A 32-bit integer representing the number of _seconds_ the receiver should consider this RR valid.
    - **RDLENGTH:** The length (in bytes) of the RDATA field.
    - **RDATA (Resource Data):** The actual answer. For an 'A' record, this is the 4-byte IPv4 address.
- **Authority & Additional Sections (Mainly in Responses):** Contain RRs pointing to authoritative name servers or providing other helpful information. Our simple resolver focuses primarily on the Answer section.
    

**4. Special Encodings**

- **Hostname Encoding:** Domain names aren't stored as simple strings. They are broken into labels, each preceded by its length. `www.google.com` becomes `\x03www\x06google\x03com\x00`. The final `\x00` marks the end of the name. The `encode_dns_name` function did this.
- **Name Compression:** To reduce packet size, if a domain name (or part of it) has already appeared earlier in the packet, subsequent occurrences can be replaced with a pointer (a 2-byte value starting with `11` bits) that points back to the first occurrence. The `parse_dns_name` function needs to detect and follow these pointers.

**5. Transport Protocol (UDP)**

- DNS queries and responses are typically sent using **UDP (User Datagram Protocol)** on **port 53**.
- UDP is connectionless and lightweight, making it fast for simple request-response protocols like DNS.
- It doesn't guarantee delivery or order, but for DNS, if a query is lost, the client usually just times out and tries again.
- If a DNS response is too large for UDP (historically > 512 bytes, now often larger), it might be truncated, requiring the client to retry using TCP (which is connection-oriented and reliable but slower to set up). Our resolver only used UDP.

**6. DNS Caching (The Key Efficiency)**

- **Problem:** Constantly asking DNS servers for the same popular domain names (like https://www.google.com/search?q=google.com) is inefficient for both the client and the servers.
- **Solution:** Caching! Store the results locally for a short period.
- **How it Works (using the TTL):**
    1. When our resolver receives a DNS response with an IP address in the Answer section, it also extracts the **TTL** value for that record.
    2. It stores the hostname, its IP address(es), and calculates an `expiry_time` (current time + TTL seconds) in a local cache (our `DNS_CACHE` dictionary).
    3. **Crucially:** Before sending _any_ new DNS query, the resolver _first_ checks its cache:
        - Does an entry for this hostname exist?
        - If yes, has its `expiry_time` passed?
    4. If an entry exists and is still valid (not expired), the resolver uses the cached IP address directly – **no network request is needed!** This is a "cache hit".
    5. If no entry exists or the entry has expired ("cache miss" or "cache expired"), the resolver proceeds to send the query over the network, gets the response, and updates the cache with the new data and its TTL.

**In Summary:** The Python code manually constructed a binary DNS query packet according to protocol rules, sent it via a raw UDP socket, received the binary response, parsed the response (handling special name encoding and compression), extracted the IP address and the TTL from the answer section, and used the TTL to implement a local cache to avoid redundant network lookups. This was done using only basic Python modules (`socket`, `struct`, `random`, `time`) as required by the assignment, forcing a hands-on understanding of the DNS protocol.