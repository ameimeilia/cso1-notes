- the stack will start after the kernel
##### AT&T Syntax
- suffixes determine how many bytes are processed
- instructions that change <32 bits preserves the rest of the register
- note: X86 will truncate if the constant is larger than the destination
- $: constant
- %: register
- no $: memory address
![[Screen Shot 2024-02-28 at 2.07.48 PM.png | center | 250]]

![[Screen Shot 2024-02-28 at 2.11.03 PM.png | 300]]   ![[Screen Shot 2024-02-28 at 2.11.37 PM.png | 360]]
##### Assembly
- Assembly is more precise than C
![[Screen Shot 2024-02-28 at 2.19.51 PM.png]]
![[Screen Shot 2024-02-28 at 2.20.02 PM.png]]
![[Screen Shot 2024-02-28 at 2.20.17 PM.png]]

![[Screenshot 2024-09-12 at 10.05.20 PM.png]]
![[Screenshot 2024-09-12 at 10.05.50 PM.png]]
![[Screenshot 2024-09-12 at 10.06.11 PM.png]]
##### GUI
![[Screen Shot 2024-03-05 at 12.23.01 AM.png]]
![[Screen Shot 2024-03-05 at 12.23.11 AM.png]]
##### Bracket Syntax
- brackets () can represent value in memory
![[Screen Shot 2024-03-05 at 12.24.33 AM.png | center | 400]]
##### Computed Addresses
- **displacement(base, index, scale) = base + (index * scale) + displacement**
- base = starting point in memory
- scale = size of value (limited to 1, 2, 4, 8)
- displacement and base are signed
![[Screenshot 2024-09-12 at 10.02.28 PM.png | center | 500]]

![[Screenshot 2024-09-12 at 10.01.28 PM.png | center | 500]]