#### Boolean Algebra
**Logic Gates**
![[Screen Shot 2024-05-03 at 4.39.33 PM.png | center | 500]]

**Transistors**
![[Screen Shot 2024-01-22 at 12.38.55 PM.png | center | 450]]

**Logic Gates with Transistors**
![[Screen Shot 2024-01-22 at 12.47.19 PM.png | center | 500]]

![[Screen Shot 2024-01-22 at 1.03.16 PM.png]]

#### Binary Arithmetic
**2-bit Adder**
![[Screen Shot 2024-05-03 at 4.51.37 PM.png | center | 450]]

**4-bit Adder**
- sum = XOR
- carry when 2 true inputs
![[Screen Shot 2024-05-03 at 4.52.03 PM.png | center | 450]]

**Ripple Carry Adder**
- half-adder + full-adder + full-adder…
![[Screen Shot 2024-01-24 at 2.31.34 PM.png | center | 500]]

![[Screen Shot 2024-01-28 at 4.07.18 PM.png | center | 250]]
#### Signed Bitwise and Hex
**Sign Bit**: highest bit represents sign
![[Screen Shot 2024-05-03 at 5.01.02 PM.png | center | 500]]

**Bias**: middle number represents 0
![[Screen Shot 2024-05-03 at 5.07.44 PM.png | center | 500]]

![[Screen Shot 2024-05-03 at 5.10.34 PM.png | center | 500]]

**Twos Complement**: top most bit represents negative $-2^n$
![[Screen Shot 2024-05-03 at 5.14.03 PM.png | center | 500]]

![[Screen Shot 2024-05-03 at 5.17.42 PM.png | center | 300]]

**Overflow**: adding two numbers of the same sign = the opposite sign
![[Screen Shot 2024-01-28 at 4.50.12 PM.png | center | 200]]

**Hexadecimal**
![[Screen Shot 2024-01-26 at 2.41.44 PM.png | center | 300]]
#### Bitwise Operations
**Operators**
![[Screen Shot 2024-05-03 at 5.23.54 PM.png | center | 600]]

**Shifts**
![[Screen Shot 2024-05-03 at 5.25.44 PM.png | center | 600]]

**Setting**
![[Screen Shot 2024-05-03 at 5.29.27 PM.png | center | 450]]
**Flipping**
![[Screen Shot 2024-05-03 at 5.29.45 PM.png | center | 450]]

**Masking**
![[Screen Shot 2024-05-03 at 5.30.08 PM.png | center | 450]]

**Combining**
![[Screen Shot 2024-05-03 at 5.30.28 PM.png | center | 450]]

**Parity**
- 1 = total # of “1” bits is odd
- 0 = total # of “1” bits is even
#### Endian and Floating Point
**Endianness**
![[Screen Shot 2024-01-29 at 2.38.16 PM.png | center | 450]]

**Floating Point**
![[Screen Shot 2024-05-03 at 7.55.08 PM.png | center | 400]]

![[Screen Shot 2024-05-03 at 8.02.57 PM.png | center | 500]]
![[Screen Shot 2024-05-03 at 8.03.09 PM.png | center | 400]]
#### ISA Components
**Muxes**
![[Screen Shot 2024-05-03 at 5.39.09 PM.png]]

**Mux as a Look-up Table**
![[LookupTables | center]]

**Clocks**
![[Screen Shot 2024-05-03 at 5.44.31 PM.png | center | 350]]

**Flip-Flops**
![[Screen Shot 2024-05-03 at 5.49.06 PM.png | center | 500]]

**3-bit Counter Using Registers/Flip-Flops**
![[Screen Shot 2024-05-03 at 5.51.09 PM.png]]

**Demux**
![[Screen Shot 2024-05-03 at 5.53.23 PM.png]]

**Register File**
![[Screen Shot 2024-05-03 at 5.54.41 PM.png | center | 500]]

**Reading and Writing to a Register File**
![[Screen Shot 2024-05-03 at 5.57.31 PM.png]]

**ALU**
![[Screen Shot 2024-05-03 at 6.21.24 PM.png | center | 500]]

**Additional Memory Components**
![[Screen Shot 2024-05-03 at 6.02.29 PM.png | center | 500]]

**Instruction Memory and Instruction Register**
![[Screen Shot 2024-05-03 at 6.50.56 PM.png | center | 300]]

**Hardwired Control Unit**
![[Screen Shot 2024-05-03 at 6.52.17 PM.png | center | 400]]
#### ISA Code
![[Screen Shot 2024-05-03 at 6.24.01 PM.png | center | 400]]

**Register Instructions**
![[Screen Shot 2024-02-18 at 4.38.50 PM.png]]

**Main Memory Instructions**
![[Screen Shot 2024-02-18 at 5.05.10 PM.png]]

**icode 5**
- b-values of 0, 1, and 2 can be executed with the ALU
- data path is long, make sure clock is slow enough for all data to propagate
![[Screen Shot 2024-02-18 at 8.29.30 PM.png]]

- b = 3 can be executed by adding PC as an input to the mux leading to WD3
![[Screen Shot 2024-02-18 at 9.02.44 PM.png]]

**icode 6**
- b = 0 can be executed by adding IM as an input to the mux leading to WD3
![[Screen Shot 2024-02-18 at 9.04.44 PM.png]]

- b = 3 can be executed by adding a mux to the address input of the data memory
![[Screen Shot 2024-02-18 at 9.06.34 PM.png]]

- b = 1, 2 can be executed by adding a mux to the second input of the ALU
![[Screen Shot 2024-02-18 at 9.10.45 PM.png]]

**icode 7**
![[Screen Shot 2024-02-18 at 9.23.43 PM.png]]

**Processing Stages**
![[Screen Shot 2024-02-18 at 9.32.32 PM.png]]
#### Functions, Push, and Pop
**Functions**
- save pc+2 to be accessed by ret (return instruction), set pc = M\[pc+1\]
![[Screen Shot 2024-02-18 at 9.37.02 PM.png | center | 600]]

**The Stack**
![[Screen Shot 2024-05-03 at 6.30.13 PM.png | center | 450]]

**ISA extended R=1**
![[Screen Shot 2024-02-25 at 10.36.11 PM.png | center | 500]]
1. R2 = first parameter
2. R3 = second parameter
3. R0 = return value of the function
![[Screen Shot 2024-02-18 at 9.59.09 PM.png | center | 300]]

**Recursive Function Example**
![[Screen Shot 2024-02-25 at 11.05.33 PM.png]]

![[Screen Shot 2024-02-25 at 11.52.11 PM.png | center | 200]]
![[Screen Shot 2024-02-25 at 11.51.26 PM.png]]
