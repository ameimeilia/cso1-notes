##### Caller Calling Convention
1. save the content from caller saved registers
2. parameters are passed into argument registers; if there are more than 6 parameters push the rest onto the stack in reverse order
3. call the subroutine; this places the return address on top of the parameters on the stack
4. after the subroutine returns, remove any additional parameters from the stack, restoring it to its state before the call was performed
5. the subroutine’s return value should be in RAX
6. restore the contents of caller saved registers by popping them off the stack
![[Screen Shot 2024-03-14 at 1.38.45 PM.png | center | 400]]

**Note**
- %rdi and %edi are the same, except %rdi is 64-bit and %edi is 32-bit
- if register values are unchanged, we can optimize by not pushing and popping, although we lose code understandability
##### Callee Calling Convention
1. allocate local variables, either with registers or the stack
2. push values from registers that are callee saved that will be used by the function
3. return value for the function should be in RAX
4. restore the values of callee-saved registers
5. deallocate local variables by subtracting from RSP
6. execute the ret instruction
![[Screen Shot 2024-03-14 at 4.18.14 PM.png | center | 400]]
##### Stack Frames
Contains:
1. local storage of variables (optional)
2. temporary scape (optional)
3. return address

- stack pointer %rsp points to the top of the stack
- frame pointer %rbp points to the base of the frame (optional)
![[Screen Shot 2024-03-14 at 4.24.04 PM.png | center | 300]]

![[Screen Shot 2024-03-14 at 4.29.16 PM.png | center | 300]]
##### Callee’s Prologue and Epilogue
- the following code may be added at the beginning and end of a function:
![[Screen Shot 2024-03-14 at 4.31.03 PM.png | center | 350]]
- this code in unnecessary; you can tell the compiler not to include it by invoking it with the -fomit-frame-pointer flag
