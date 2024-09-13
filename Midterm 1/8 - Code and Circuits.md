##### Demux
- connects one input to one of the N outputs
![[Screenshot 2024-09-12 at 9.58.33 PM.png | center | 400]]

![[Screenshot 2024-09-12 at 9.59.29 PM.png | center | 400]]

##### Register File
**32-Bit Register File**
- temporary storage location
- stores immediately needed variables
- allows you to simultaneously read from two registers and write into one register
![[Screenshot 2024-09-12 at 10.00.04 PM.png | center | 500]]

**Read From a Register File**
- use muxes to read from a register file
![[Screen Shot 2024-02-07 at 5.10.23 PM.png | center | 450]]

**Write to a Register File**
- use demuxes to write to a register file
- additional inputs: write enable (WE), write data (WD), address of register to be written to (A3)
![[Screen Shot 2024-02-07 at 5.17.42 PM.png | center | 450]]
##### Additional Memory Components
**Program Counter**
- to track where we are in a program
![[Screen Shot 2024-02-05 at 2.31.19 PM.png | 200]] ![[Screen Shot 2024-02-05 at 2.31.57 PM.png | 250]]

**Instruction Memory**
- stores the program
- read data (RD) for a given address (A)
![[Screen Shot 2024-02-07 at 6.17.22 PM.png | center | 150]]

**Data Memory**
- contains data needed by the program
- read data (RD) for a given address (A)
- write data (WD) for a given address (A)
![[Screen Shot 2024-02-07 at 6.24.47 PM.png | center | 150]]