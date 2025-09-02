#concept 

All data in computer programs are internally stored as **bits**, i.e., as numbers 0 and 1.

![[WhatsApp Image 2025-07-10 at 05.38.23.jpeg]]

In programming, an n-bit integer is internally stored as a binary number that consists of n bits. For example, the C++ type `int` is a *32*-bit type, which means that every int number consists of 32 bits.

```cpp
int n = 13;
cout << bitset<32>(n); // 000000000000000000000000000001101
```

The bits in the representation are indexed from right to left. From least significant to most significant bit.

To convert a bit representation $b_k\ldots b_2b_1b_0$ into a number, we can use the formula:
$$b_k2^k + \ldots + b_12^1 + b_02^0$$
Example:
$$1101 = 2^3 + 2^2 + 0*(2^1) + 2^0 = 8 + 4 + 0 + 1 = 13$$

---

The bit representation of a number is either ***signed*** or ***unsigned***.

Generally, a signed representation is used, which means that both negative and positive numbers can be represented.

A signed variable of n bits can contain any integer between $-2^{n-1}$ and $2^{n-1}-1$

The `int` type in C++ is a signed type, so an `int` variable can contain any integer between $-2^{31}$ and $2^{31}-1$.

$$1000\ldots0000 \text{ = INT\_MIN} = -2^{31} \, = -2147483648$$
$$0111\ldots1111 \text{ = INT\_MAX} = 2^{31} - 1 = 2147483647$$

The first bit in a signed representation is the **sign bit** of the number

- 0 for non-negative numbers
- 1 for negative numbers
- and the remaining n−1 bits contain the magnitude of the number.

> *2's complement* is used to represent a negative number is bits.
> Hence, 2's complement is used to calculate the value of a signed `int` with sign bit 1.

In an ***unsigned*** representation, only non-negative numbers can be used, but the upper bound for the values is larger.

In C++, an `unsigned int` variable can contain any integer between $0$ and $2^{32}-1$.

There is a connection between the representations:

$$\text{signed int } -x = \, \text{ unsigned int }2^n-x$$

```cpp
int x = -43
unsigned int y = -43;
cout << x << endl; // -43
cout << y << endl; // 429234234
```

If a number is larger than the upper bound of the bit representation, the number will ***overflow***.

In a signed representation, the next number after  $2^{n-1}-1$ is $-2^{n-1}$

In an unsigned representation, the next number after $2^n-1$ is $0$.

```cpp
int x = INT_MAX;
cout << x << endl; // 2147483647
x++;
cout << x << endl; // -2147483648
```

---
## Common Bitwise Operators

#### AND Operation (`&`)

Intersection. Both bits must be 1.
$$\text{Decimal : } 5 \,\&\, 3 = 1$$
$$\text{Binary : }0101 \,\&\, 0011 = 0001 $$

#### OR Operation (`|`)

Union. Any one bit should be 1.
$$\text{Decimal : } 5 \,|\, 3 = 7$$
$$\text{Binary : }0101 \,|\, 0011 = 0111 $$

#### XOR Operation (`^`)

Xor of odd 1's is 1. Even 1's is 0.
$$\text{Decimal : } 5 \,\oplus\, 3 = 6$$
$$\text{Binary : }0101 \,\oplus\, 0011 = 0110 $$

#### NOT Operation (`~`)

Flips all bits of a number.
$$\text{Decimal : } \sim 5 = -6$$
$$\text{Binary : } \sim 0101 = 1010 \text{ (read in 2's complement)}$$

#### Left Shift Operation (`<<`)

Shifting left multiplies the number by `2` for each shift.
$$\text{Decimal : } 5 \, \ll \, 1 = 10$$
$$\text{Binary : } 0101 \, \ll \, 1 = 1010$$
$$\text{Formula : } n \, \ll \, k = n \times 2^k$$
If you shift a number too far to the left (beyond its bit capacity), the sign bit may change, making the number negative. Resulting in unexpected outputs.

#### Right Shift Operation (`>>`)

Shifting right divides the number by `2` for each shift.
$$\text{Decimal : } 5 \, \gg \, 1 = 2$$
$$\text{Binary : } 0101 \, \gg \, 1 = 0010$$
$$\text{Formula : } n \, \gg \, k = \frac{n}{2^k}$$

#### 1's Complement

The **1's complement** of a binary number is obtained by flipping all the bits.

$$ \text{Binary: } 0000\ldots0001011$$
$$\text{1's Complement: } 1111\ldots1110100$$

```cpp
int n = 5; // Binary: 0...0101
int onesComplement = ~n; // Binary: 1...1010 : -6
```

#### 2's Complement

The **2's complement** of a binary number is obtained by taking the 1's complement of the number and then adding `1` to the result.

It is commonly used to represent negative integers in binary form.

$$\text{Binary: } 0\ldots0101$$
$$\text{1's Complement: } 1\ldots1010$$
$$\text{2's Complement: } 1\ldots1011$$

For positive integers, the 2's complement representation is the same as their binary form.

```cpp
int n = 5; // Binary: 0...0101
int twosComplement = ~n + 1; // Binary: 1...1011 : -5
```

### Common Properties

$$X \wedge 0 = X$$
$$X \wedge 1 = \textasciitilde X$$
$$X \wedge X = 0$$
$$X \,\&\, 0 = 0$$
$$X \,\&\, 1 = X$$
$$X \,\&\, X = X$$
$$X \,|\, 0 = X$$
$$X \,|\, 1 = 1$$
$$X \,|\, X = X$$

---
## Programs

#### Swap two numbers

```cpp
int a = 5;
int b = 3;

a = a ^ b;
b = a ^ b;
a = a ^ b;

/*
OR
a = a + b;
b = a - b;
a = a - b;
*/

cout << a << endl;    // 3
cout << b << endl;    // 5
```

#### Decimal to Binary Conversion
$$(13)_{10} = (1101)_2$$
```cpp
string decimal_to_binary(int n = 13) {
	string binary = "";
	while(n)
	{
		binary += (n & 1) ? '1' : '0';
		n /= 2;
	}
	reverse(binary.begin(), binary.end());
	return binary;
}
```

#### Binary to Decimal Conversion
$$(1101)_2 = (13)_{10}$$
```cpp
int binary_to_decimal(string binary = "1101") {
    int decimal = 0;
	int n = binary.size();
    for (int i = 0; i < n; i++)
        if (binary[n - 1 - i] == '1')
            decimal += pow(2, i);
    return decimal;
}
```

#### Get $i$th Bit

```cpp
int bit = (num >> i) & 1;
/* OR */
int bit = num & (1 << i);
```

#### Set $i$th Bit

```cpp
int newNum = num | (1 << i);
```

#### Clear $i$th Bit

```cpp
int newNum = num & (~(1 << i));
```

#### Toggle $i$th Bit

```cpp
int newNum = num ^ (1 << i);
```

#### Find last set bit (rightmost)

2's compliment flips all bits to the left of the rightmost bit. Which means, AND operation between a number and it's 2's compliment results in the rightmost set bit mask.

```cpp
int n = 12;    // 00...01100
int x = ~n;    // 11...10011
x = x + 1;     // 11...10100
return n & x;  // 00...00100
/* OR */
return n & -n;
```

Similarly you can perform same operation on `~n` instead to find rightmost *unset* bit.

#### Remove last set bit (rightmost)

If you take a number down by one, it's rightmost bit turned to zero. And all 0s to its right, get turned into 1s.

```cpp
int n = 12;    // 1100
n - 1 = 11;    // 1011
return n & (n - 1); // 1000
```

#### To Check if $n$ is a Power of 2

An integer $n$ is a power of 2 if there is only one set bit in its binary representation.

```cpp
bool isPowerOfTwo(int n) {
    return (n & (n - 1)) == 0;
    /* OR */
    return floor(log2(n)) == ceil(log2(n));
}
```

#### To Check if $n$ is a Power of 4

An integer $n$ is a power of 4 if it is a power of 2 and it's previous number is divisible by 3.

```cpp
bool isPowerOfFour(int n) {
    return (n & (n - 1)) == 0 && (n - 1) % 3 == 0;
    /* OR */
    return floor(log2(n)) == ceil(log2(n)) && (int(log2(n)) % 2 == 0);
}
```

#### Count Set bits

```cpp
int n = 28;
int count = 0;
while (n)
{
	n = n & (n - 1);
	count++;
}
return count;
```

---
## STL

#### `std::bitset`

A class that provides an easy way to represent and manipulate fixed-size binary numbers.

```cpp
bitset<8> b("1010");      // Binary representation: 1010
cout << b << endl;        // Output: 00001010

b.set(2);                 // Set the 2nd bit (0-based index)
cout << b << endl;        // Output: 00001110

b.reset(3);               // Clear the 3rd bit
cout << b << endl;        // Output: 00000110

b.flip();                 // Flip all bits
cout << b << endl;        // Output: 11111001

cout << b.count() << endl;  // Count the number of 1's (Output: 6)
cout << b.any() << endl;    // Check if any bit is set (Output: 1)
cout << b.none() << endl;   // Check if no bit is set (Output: 0)

int num = b.to_ulong();    // Convert bitset to unsigned long
cout << num << endl;       // Output: 249
```

#### `__builtin_popcount` and Variants

GCC/Clang built-in functions for fast bit-level operations.

- `__builtin_popcount(x)`: Counts the number of set bits in an integer.
- `__builtin_clz(x)`: Counts leading zeros.
- `__builtin_ctz(x)`: Counts trailing zeros.
- `__builtin_parity(x)`: Checks if the number of set bits is odd (returns 1 for odd, 0 for even).

```cpp
int n = 13;  // Binary: 1101
cout << __builtin_popcount(n) << endl;  // Output: 3 (number of 1's)
cout << __builtin_clz(n) << endl;      // Output: 28 (leading zeros in 32-bit representation)
cout << __builtin_ctz(n) << endl;      // Output: 0 (trailing zeros)
cout << __builtin_parity(n) << endl;   // Output: 1 (odd number of 1's)
```

