---
tags:
  - devops
references: 
date_created: 2025-07-16
date_modified: 2025-07-17
---
---

This guide outlines the steps to set up an Ubuntu server for self-hosting, from initial installation to configuring network and SSH access.

## 0. Prerequisites

Before you begin, ensure you have the following:

- **Server Hardware:** A computer with a 64-bit CPU architecture, at least 1 GB RAM, and 16 GB storage. It should have a keyboard, mouse, and monitor, and be connected to a stable 24/7 internet and power supply. This will serve as your dedicated server.
- **Remote Access Computer:** A separate computer (MacOS or Windows recommended) to perform remote actions via SSH.
- **Domain Name:** A public domain name (this will eventually be used for API access).
- **Bootable USB Drive:** A flash drive with at least 4 GB capacity to create a bootable Ubuntu installer.

## 1. Ubuntu Server Installation

Follow these steps to install Ubuntu Server on your designated hardware:

1. **Download Ubuntu Server:** Obtain the latest Long Term Support (LTS) version of Ubuntu Server from the official website (e.g., `22.04.5 LTS amd64 Jammy Jellyfish`).
2. **Create Bootable USB:** Use a tool like Rufus to create a bootable USB drive with the downloaded ISO image.
3. **Data Backup (Optional but Recommended):** Perform a physical backup of all data on your server computer, as the installation process will erase all existing data.
4. **Boot from USB:** Insert the bootable USB drive into the server computer and restart it. You may need to access the BIOS/UEFI settings (often by pressing `F10` or `Del` during startup) to change the boot order and prioritize the USB drive.
5. **Install Ubuntu Server:**
    - Proceed with the Ubuntu Server installation.
    - **Crucial Step:** During disk setup, ensure you **uncheck** "Set up this disk as an LVM group" to avoid manual disk space allocation.
    - Accept all other default installation options.
6. **Initial Login & Upgrade:** After installation, log in with your created username and password, then upgrade your server:
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

> [! Tip]
> Adjust Advanced BIOS settings if you encounter booting issues. The goal is for your server to boot automatically without manual intervention.

---
## 1.5. Fixing Network Issues (Optional: For Wi-Fi Connectivity)

If your server lacks Ethernet support and you're encountering Wi-Fi issues, follow these steps to install necessary network packages offline:

1. **Download Packages (on a computer with internet):**
    - Plug a flash drive into a computer with an internet connection.
    - Go to [packages.ubuntu.com](https://packages.ubuntu.com/ "null") and select your Ubuntu distribution (e.g., `jammy`).
    - Search for and download the following `.deb` packages to your flash drive:
        - `libbluetooth3`
        - `libndp0`
        - `libnm0`
        - `libteamdctl0`
        - `network-manager`
2. **Install Packages (on your Ubuntu server):**
    - Plug the flash drive into your running Ubuntu server.
    - Identify your flash drive's device name:
        ```bash
        lsblk
        ```
        (e.g., `sdb1` for SATA, `sda1` for NVMe).
		
    - Mount the flash drive:
        ```bash
        sudo mount /dev/sdb1 /mnt
        ```
        (Adjust `sdb1` if your drive/partition is different).
		
    - Navigate to the directory containing the downloaded `.deb` files:
        ```bash
        cd /mnt/yourfolder # e.g., cd /mnt/ubuntu-wifi
        ```
		
    - Install all downloaded `.deb` files:
        ```bash
        sudo dpkg -i *.deb
        ```
		
3. **Configure Wi-Fi using `nmtui`:**
    - Launch the NetworkManager Text User Interface:
        ```bash
        nmtui
        ```
        
    - Select "Activate a connection".
    - Choose your Wi-Fi network, enter the password, and select "OK".
    - Go back and select "Quit".
4. **Verify Connectivity:** Confirm internet access:
    
    ```bash
    ping google.com
    ```

> [! Warn]
> After connecting, run `sudo apt update && sudo apt upgrade -y` again.
#### Optional: Reduce Boot Time

To prevent long boot times caused by "start job is running for wait for network to be configured," disable the service:

```bash
sudo systemctl disable systemd-networkd-wait-online.service
```

---
## 2. Making Private IP Address Static

To ensure your server always has the same local IP address, configure it as static using NetworkManager's `nmtui`. Remove any existing `netplan` configurations if you've previously modified them.

1. **Access NetworkManager TUI:**
    ```bash
    sudo nmtui
    ```
    
2. **Edit Connection:** Select "Edit a connection" and choose your active Wi-Fi connection.
3. **Configure IPv4:**
    - Change "IPv4 CONFIGURATION" from "Automatic" to "Manual".
    - Select "Show" next to "Addresses".
    - **Add Address:** Select `<Add>` and enter your desired static IP address in CIDR notation (e.g., `192.168.29.50/24`).
        - _Note:_ The first three octets of the static IP address must match your current IP address. Verify your current IP with `ip a` before setting a static one.
    - **Gateway:** Navigate to "Gateway" and enter your router's IP address (eg `192.168.29.1`).
    - **DNS Servers:** Navigate to "DNS servers" and enter your preferred DNS server(s), separated by a comma if multiple (e.g., `8.8.8.8, 8.8.4.4`).
4. **Optional: Disable IPv6:** You can uncheck the IPv6 requirement to simplify the configuration if not needed.
5. **Save & Reconnect:**
    - Save your changes and exit the connection editor.
    - Navigate to `<Activate a connection>` and reconnect to your Wi-Fi network to apply the changes.
    - Save and exit `nmtui`.
6. **Verify Static IP & Internet:**
    - Confirm your new static IP address:
        ```bash
        ip a
        ```
		
    - Verify internet connectivity:
        ```bash
        ping google.com
        ```

---
## 3. Glorious SSH

Now that your server has a static IP and internet access, set up SSH for remote management. Ensure your server is fully updated and upgraded.

1. **Install SSH:** Install the SSH client and server on both your Ubuntu server and your personal computer:
    ```bash
    # On Ubuntu Server
    sudo apt install openssh-server -y
    
    # On your Personal Computer (if not already installed)
    sudo apt install ssh -y # For Linux/WSL, macOS usually has it
    ```
    
2. **Connect via SSH** (Password Authentication):
    - Ensure your personal computer is on the same local network as your server.
    - Open a terminal on your personal computer (preferably a Unix-like environment) and run:
        ```bash
        ssh your_server_username@your_static_ip
        # Example: ssh artoriax@192.168.29.50
        ```
        
    - Enter your server's password when prompted. You should now be connected.
        
3. **Configure SSH Key Authentication** (Recommended for Security & Convenience):
    - **Generate SSH Key** (if you don't have one): On your personal computer, follow [this GitHub guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent "null") to generate a new SSH key pair (e.g., `id_ed25519`).
    - **Copy Public Key:** Display your personal computer's public SSH key:
        ```bash
        cat ~/.ssh/id_ed25519.pub
        ```
        
        Copy the entire output.
    - **Add Key to Server:** On your Ubuntu server (either directly or via the password-authenticated SSH session):
        - Create the `.ssh` directory if it doesn't exist:
            ```bash
            mkdir -p ~/.ssh
            chmod 700 ~/.ssh
            ```
            
        - Create or append your public key to the `authorized_keys` file:
            ```bash
            echo "PASTE_YOUR_PUBLIC_KEY_HERE" >> ~/.ssh/authorized_keys
            chmod 600 ~/.ssh/authorized_keys
            ```
			
            Replace `"PASTE_YOUR_PUBLIC_KEY_HERE"` with the actual public key copied earlier.
    - **Test Key Authentication:** Exit the current SSH session (`exit`) and try connecting again from your personal computer. You should now be able to SSH in without a password.
4. **Disable Password Login:** (for enhanced security):
	- Once you have SSH key authentication working, disable password login for enhanced security.
	- Firstly make sure to generate SSH key (step 3) for all required devices via which you SSH.
	- Edit `/etc/ssh/sshd_config`:
		- Change `PasswordAuthentication yes` to `PasswordAuthentication no`.
		- Reload SSH service: `sudo systemctl reload sshd`.

You have successfully set up your Ubuntu server for self-hosting with static IP and secure SSH access!

---
## 4. Making your IP Public - Cloudflare Tunneling

Refer: [video](https://youtu.be/BnWfbv7Fy-k?si=h2n-wD2aAmw_tmz7)

1. **Create a Cloudflare Account and Add Your Domain**
	- Sign up for a free Cloudflare account at `cloudflare.com`.
	- In your Cloudflare dashboard, click "Add a domain" and enter your domain name.
	- Select the free plan and continue.
2. **Update Your Domain's Nameservers**
	- Cloudflare will provide you with two nameservers.
	- Go to your domain registrar's DNS settings (where you purchased your domain).
	- Replace your existing nameservers with the ones provided by Cloudflare.
	- Propagation can take 5-10 minutes, up to 48 hours. Cloudflare will notify you when your site is active.
3. **Create a Permanent Tunnel in Cloudflare Zero Trust**
	- In your Cloudflare dashboard, navigate to "Zero Trust", then "Access" > "Tunnels".
	- Click "Create a tunnel" and give it a name (e.g., "my-server-tunnel").
	- Click "Save tunnel". Cloudflare will provide a command to install the connector on your server, including a unique token. Copy and run this command (e.g., `sudo cloudflared service install YOUR_TUNNEL_TOKEN`).
	- Confirm the service is installed and click "Next" in the Cloudflare dashboard.
4. **Configure Public Hostnames for Your Tunnel**
	- Under "Public Hostnames", click "Add a public hostname".
	- Enter a **Subdomain** (e.g., `web`), select your **Domain**, choose **HTTP** as the **Service Type**, and enter your local service **URL** (e.g., `localhost:3000`).
	- Click "Save tunnel" or "Save hostname". You can add multiple hostnames to expose different services.
5. **(Optional) Configure SSL/TLS**
	- In your Cloudflare dashboard for your site, go to "SSL/TLS".
	- Set the encryption mode to "Full" for end-to-end encryption.
6. **Test Your Tunnel**
	- Open your configured public URL (e.g., `https://web.yourdomain.com`) in a browser.
	- It should now display content from your local service. (setup pm2)
	- If you encounter issues, try: waiting longer, using an incognito window, a different browser, or clearing DNS cache.

---
## 5. SSH into Home Server via Browser (Zero Trust)

This guide outlines how to securely access your home server via SSH through a web browser, leveraging Cloudflare Zero Trust without the need for port forwarding.

1. **Configure Public Hostname in Cloudflare Tunnel**
	- Navigate to your Cloudflare Zero Trust dashboard, then to "Networks" and select your existing tunnel.
	- Add a new public hostname.
	- **Subdomain:** Choose a subdomain (e.g., `ssh`) and your primary domain.
	- **Type:** Select "SSH".
	- **URL:** Enter the local IP address of your server (`localhost:22`).
	- Save the configuration.
2. **Set Up an Access Policy (Application)**
	- An Access Policy is required to enable browser-based SSH.
	- Go to "Access" > "Applications" and add a new "self-hosted" application.
	- **Application Name:** Enter a descriptive name (e.g., "SSH Access").
	- **Application Domain:** This _must_ match the subdomain and domain you set up for the tunnel (e.g., `ssh.yourdomain.com`).
	- Configure **Identity Providers** and **Session Duration** as desired. (default)
	- Set **Rules** for access (e.g., based on email or everyone).
	- **Crucial Step:** Under "Browser rendering," ensure you select "SSH".
	- Add the application.

Now you should be able to SSH into your home server via browser. Require email verification, user name and password. Can replace password with private key.

**SSH Key Authentication (Optional)**
- **Generate a new SSH key pair on your local machine:**
    - Use `ssh-keygen` and provide a unique filename (e.g., `Cloudflare_ssh_key`)
    - **Important:** Set a strong passphrase for your private key, as Cloudflare might require it
- **Add the public key to your server:**
    - Copy the contents of your public key file (e.g., `Cloudflare_ssh_key.pub`).
    - Paste it into the `~/.ssh/authorized_keys` file on your server
- **Use the private key in the browser:**
    - When prompted by the browser SSH interface, select "private key"
    - Paste the _entire content_ of your **private key** file
    - Enter the passphrase you set for the private key
    - Submit to establish the SSH connection

This method provides a highly secure and convenient way to access your home server via SSH from any web browser, leveraging Cloudflare's robust security features.

---

Now you're ready and can deploy any application or service that you like on your personal machine. Boom!


I installed NextCloud and it's great. I'm also running web sockets on it, but the speed is horrible. This is still self hosted. I can run CRUD applications on it at decent pace. No problemo. This was fun.