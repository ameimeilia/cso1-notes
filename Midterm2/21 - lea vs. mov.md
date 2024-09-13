##### Swap()
- `()` indicates the value stored at the memory of the address in the register
![[Screen Shot 2024-03-15 at 2.25.39 PM.png | center | 400]]
##### leaq vs. movq
- leaq calculates an address and loads it into the destination
- movq moves content and will access memory if the source operand is a memory location
![[Screen Shot 2024-03-15 at 2.37.36 PM.png]]

**lea Tricks**
```
leaq (%rax, %rax, 4), %rax
rax <- rax * 5
rax <- address-of(memory[rax + rax * 4])
```

```
leaq (%rbx, %rcx), %rdx
rdx <- rbx + rcx
rdx <= address-of(memory[rbx + rcx])
```
##### Exam Question