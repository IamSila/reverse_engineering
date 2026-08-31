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
- In a little-endian system, the least significant byte is located at the smallest address. In a big-endian system, the most significant byte is at the smallest address.


# Registers
- Divided into two:
    i) General Purpose Registers - Used for general storing data, addresses,etc., and are directly manipulable
        eax: eax is the “accumulator” register. Its name comes from the fact that it is commonly used to hold the result of an arithmetic operation.
        ebx: ebx is the “base” register. It is commonly used to hold the base address of the chunk of memory used to store a variable. For example, the expression
        ecx: ecx is the “counter” register and is traditionally used to count. For example,ecx might be used to track the current iteration of a loop. In the command for (i=0; i<10; i++), the variable i is likely to be stored in the ecx register.
[ebx + 5] can be used to access the fifth element of an array.
        edx: edx is the “data” register. It's name comes from the fact that it is commonly used to hold data. For example, an application may include the instruction sub edx, 7.
        esi: esi is the “source index” register. It is traditionally used to store an index into a source array. For example, in the command array[i] = array[k], the value of k would likely be stored in esi.
        edi: edi is the “destination index” register. It is used to store an index into a destination array. For example, in the command array[i] = array[k], the value of i would likely be stored in edi.
        ebp: ebp is the “base pointer” register. Its purpose is to store the address of the base of the current stack frame.
        esp: esp is the “stack pointer” register. It stores the address at the top of the current stack frame.
    ii) Special purpose registers. - Used to store the program state.


# working with registers.
- e.g How do you break a register i.e eax into ax and further that ax into al and ah.


# Memory Access
- Intel syntax uses [] notation and AT&T syntax uses () notation. E.g [0x12345678] to access the data in that memory.


# addressing modes
- absolute addressing modes
- Base + displacement addressing modes
- index based addressing mode.
- based-indexed addressing mode.



# Assembly instructions
- Operands can be registers, immediate values or memory addresses.
- add [0x12345678], [0x87654321] --> this assembly syntax is wrong coz it accesses two memory locations at the same time.

arithmetic mnemonics
add --> add destination, value ---> destination + value ---> result in destination. Size of the two operands must be same: 32 bit and 32 bit.
sub ---> same as addition above just that we are subtracting this time.
mul ---> The syntax of a mul operation is ```mul operand```, where operand
can be a register or memory address. The operation multiplies the value stored
in eax with the value specified in the operand.
The results are stored in edx:eax with edx containing the high 32 bits of the result.
div ---> quotient is stored in eax and the reminder is stored in edx. High 32 bits are in edx and low 32 bits are in eax. e.g div eax is equivalent to eax, edx = eax:edx / eax.
inc
dec

bit manipulation
and
or
xor
not

stack
call
pop
return
push


data movement
mov - does not move data. It compies data.

execution flow
jmp
conditional jump

comparison
cmp
test

other
lea
nop

shr and shl
shr and shl are logical shift operators. This means that when shifting the
value by the indicated immediate value, they will zero-extend the value to the
left or right.



