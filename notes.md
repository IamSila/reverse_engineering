# x86 syntax
- AT&T syntax
- Intel syntax

# bits, bytes and words
- bit: 0s and 1s
- Nibble; 4 bits
- byte: 8 bits
- word: 2 bytes or 16 bits.
- Double word: 4 bytes or 32 bits.
- Quard word: 8 byts or 64 bits.


# Important terms to understand in reverse_engineering
- Zero extension: On a 32-bit architecture, this means adding 0s to the left of the value until it is 32 bits long. On a 64 bit architecture it means the same.
- most significant bytes --> 00000000 00000000 00000000 00001101  <--- least significant bytes
bytes near msb   -           high order bytes         low order bytes - bytes near lsb

- Endianness: The order in which these bytes are stored in memory. In a little-endian system, the least significant byte is stored first (at the lowest address). In a big-endian system, the most significant byte is stored first (at the lowest address).

