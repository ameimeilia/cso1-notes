##### Optimization
**No optimization**
![[Screen Shot 2024-03-14 at 4.57.49 PM.png | center | 300]]
**-03 Optimization**
- `(%rdi, %rsi)` produces a computed address using the load effective address instruction
![[Screen Shot 2024-03-14 at 4.58.09 PM.png | center | 300]]
##### Additional Instructions
**Compare (CMP) Instruction**
- subtracts but doesn’t store result
- `cmp %rax, %rdi -> rdi-rax`

**Test Instruction**
- computes bitwise and
- `test %rax, %rdi -> rdi & rax`
##### Condition Codes and Jumps
**Flags**:
- CF: carry flag(for unsigned)
- SF: sign flag (for signed negatives)
- ZF: zero flag
- OF: overflow flag (for signed overflow)

- implicitly set by arithmetic operations (not changed by `leal)
- 1 = true, 0 = false

**Jumps**
- `jle, jg, je` read condition codes following a comparison
- `jg` is simply the NOT of `jle`
![[Screen Shot 2024-03-14 at 5.27.33 PM.png | center | 400]]

**Example**
![[Screen Shot 2024-03-14 at 5.34.28 PM.png | center | 400]]
##### Computed Jumps
![[Screen Shot 2024-03-14 at 5.48.01 PM.png | center | 400]]
##### Overlapping Registers
- setting 32-bit registers clears the corresponding 64-bit register
```
movq $0xFFFFFFFFFFFFFFFF, %rax
movl $0x1, %eax

// %rax is $0x1, not $0xFFFFFFFF00000001
```

- setting 8 or 16-bit registers does not clear the 64-bit register
```
movq $0xFFFFFFFFFFFFFFFF, %rax
movb $0x1, %al

// %rax is $0xFFFFFFFFFFFFFF01
```
##### Factorial Example
![[Screen Shot 2024-03-14 at 6.08.44 PM.png]]