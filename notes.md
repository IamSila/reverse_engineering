# x86 syntax
- AT&T syntax
- Intel syntax

# bits, bytes and words
- bit: 0s and 1s
- Nibble; 4 bits
- byte: 8 bits
- word: 2 bytes or 16 bits.
- Double word: 4 bytes or 32 bits.
- Quad word: 8 bytes or 64 bits.


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
- stands for no operation.
- While nop technically does nothing, it is used for a variety of legitimate purposes, including the following:
    Timing
    Memory alignment
    Hazard prevention
    Branch delay slot (RISC architectures)
    A placeholder to be replaced later by a future patch
And in the security world it is used for the following:
    Hacking (nop sleds)
    Cracking (nop outs)

shr and shl
shr and shl are logical shift operators. This means that when shifting the
value by the indicated immediate value, they will zero-extend the value to the
left or right.

NB: Zero-extending a right-shifted value will fill empty bits with zeros and is called a logical shift. Sign-extending a right-shifted value will fill empty bits with the same value as the most significant bit and is called an arithmetic shift.

sar and sal
- are arithmetic shift operators.
- they fill the shifted bits with the most significant bit.


reference point for assembly mnemonics 
http://ref.x86asm.net/coder32.html



# Building and running assembly programs.
- ASCII and UTF8 are encoding schemes which determines how data is represented in computers.
- More practice needed here.



# Understanding condtion codes.
- when we want to track the condition in an if statement, there are special register which store this information. It is called flags.
- In x32 systems this is called eflags.
- In 16 bits they are called flags.
- In 64 bit systems they are called rflags.


eflags
- contains different flags which are a single bit each. Each flag can be set to either true or false.
- There are different flags:
  - status flag. - show status of operations e.g whether the previous operations completed successfully.
  - control flag. - controls how the processor operates. Such as enabling and disabling interupts.
  - system flags - contain the state of the processor. e.g whether the system is virtualised.


status flags.
carry flag.
- is at bit 0 of the eflag register.
- specifies whether the last operation resulted in a carry.
zero flag.
- is at bit 6 of the eflag register.
- indicates whether the last arithmetic operation resulted in a zero.
- if the result is a zero the flag is set to a 1.
sign flag.
- Found at the seventh flag of the eflag.
- Specifies whether a sign bit was set for the previous arithmetic operation.
- If the bit is set it is negative, if it is not set, it is positive.
overflow flag.
- Is the 11th flag of the eflag.
- the overflow flag is used for signed math to detect when something didn’t go right.
- Often, this indicates one of two cases:
  Positive + Positive = Negative
  Negative + Negative = Positive


# Analysing and debugging assembly code.
Binary Analysis.
- Can be done in different ways:
    static analysis - analysing the source code without ever running it.
    dynamic analysis - running the program and analysing its behaviour when it is running.
    debugging - 

debug flow
  1. Set breakpoints on points of interest.
  2. Run the code.
  3. The execution pauses (“breaks”) at the breakpoint.
  4. Examine the program state.
  5. Optionally make modifications.
  6. Repeat.

- There are hardware and software debuggers.
- H/W breakpoints are stored in DR 0-7 which is the debugger registers.
- dr 0-4 stores the breakpoint addresses while 6 and 7 stores the configuration info.


the gnu debugger
- commandline, it is scriptable and has remote debugging support.

debugging with gdb
e.g gdb a.out ----> to open a binary in gbb 
(gdb) set disassembler-flavour intel -----> to set the syntax to intel flavour.
(gdb)  disassemble  ----> starts disassembling at the current instruction 
(gdb) disassemble <address>  -----> starts disassembling at the current instruction.
(gdb) disassemble <label name>  -----> start disassembling at the current label.
(gdb) disassemble <label name> + <const number>    ----> start disassembling at <lable name> and print <const number> of lines.



