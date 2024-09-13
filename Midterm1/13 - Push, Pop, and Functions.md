---
layout: default
title: Push, Pop, and Functions
---
##### icode 5
- b-values of 0, 1, and 2 can be executed with the ALU
- data path is long, make sure clock is slow enough for all data to propagate
![[Screen Shot 2024-02-18 at 8.29.30 PM.png]]

- b = 3 can be executed by adding PC as an input to the mux leading to WD3
![[Screen Shot 2024-02-18 at 9.02.44 PM.png]]
##### icode 6
- b = 0 can be executed by adding IM as an input to the mux leading to WD3
![[Screen Shot 2024-02-18 at 9.04.44 PM.png]]

- b = 3 can be executed by adding a mux to the address input of the data memory
![[Screen Shot 2024-02-18 at 9.06.34 PM.png]]

- b = 1, 2 can be executed by adding a mux to the second input of the ALU
![[Screen Shot 2024-02-18 at 9.10.45 PM.png]]
##### icode 7
![[Screen Shot 2024-02-18 at 9.23.43 PM.png]]
##### Processing Stages
![[Screen Shot 2024-02-18 at 9.32.32 PM.png]]
##### Functions
- the location of the function can be hard-coded, but the return location cannot
- the solution is to save PC = next instruction, then read and jump back to that location after executing the function
- save pc+2 to be accessed by ret (return instruction), set pc = M\[pc+1\]
![[Screen Shot 2024-02-18 at 9.37.02 PM.png]]
##### The Stack
- used for recursive calls
- the stack holds function states and their associated return addresses
- the stack grows to lower addresses → functions are pushed to the bottom of the stack
- RSP (register stack pointer) holds the location of the TOP of the stack in memory
![[Screen Shot 2024-02-18 at 9.53.09 PM.png | center | 250]]
##### Push and Pop Instructions
**Push**
- decrements the RSP
- pushes to the top of the stack

**Pop**
- returns the value at the top of the stack
- increments RSP