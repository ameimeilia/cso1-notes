##### Compilation Pipeline Overview
![[Screen Shot 2024-03-13 at 2.10.15 PM.png | center | 400]]
##### From C to an Executable
**C → Assembly**
![[Screen Shot 2024-03-13 at 2.57.36 PM.png | center | 500]]

**Assembly → Object File**
![[Screen Shot 2024-03-13 at 2.58.11 PM.png | center | 450]]

**Inspect Object File**
![[Screen Shot 2024-03-13 at 2.58.46 PM.png | center | 400]]

**Objdump**
- note: address of the function to call and the location of the string is missing
![[Screen Shot 2024-03-13 at 3.02.04 PM.png | center | 400]]

**Object File → Executable**
![[Screen Shot 2024-03-13 at 3.08.59 PM.png | center | 400]]

- addresses are now filled in
- stored in little endian
![[Screen Shot 2024-03-13 at 3.09.53 PM.png | center | 500]]

**Overview**
![[Screen Shot 2024-03-13 at 3.11.43 PM.png | center | 600]]
##### Pushing and Popping with Moves
- no need to use register
![[Screen Shot 2024-03-14 at 11.33.03 AM.png]]
