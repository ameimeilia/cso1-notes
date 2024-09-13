##### Muxes
- selector S input selects between one of N inputs to connect to output
- represented each input with log<sub>2</sub>N bits
![[Screen Shot 2024-02-05 at 11.56.05 AM.png | center | 600]]

![[Screen Shot 2024-02-05 at 12.25.40 PM.png | center | 600]]

**Mux as a Look-up Table**
![[Screenshot 2024-09-12 at 9.55.05 PM.png | center | 400]]

##### Clocks
- produces a periodic signal
- **period/cycle** = length of time for one clock cycle (1 / frequency)
- **frequency** = 1 / period
- ex. Intel Core i-9 3.0GHz processor → 3,000,000,000 cycles/sec where every cycle executes one instruction
![[Screenshot 2024-09-12 at 9.55.57 PM.png | center | 400]]

**Clocks Using Ring Oscillators**![[Screenshot 2024-09-12 at 9.57.21 PM.png | center | 400]]
##### Flip-Flops
**Positive Edge-Triggered D Flip-Flop**
Inputs:
1. D - Data in (the single bit to be stored)
2. Clock - output wave determines when the values change and how long they remain

Outputs:
1. Q - value of the internal state
2. $\overline{Q}$ - the inverse of Q

![[Screen Shot 2024-02-05 at 1.21.47 PM.png | center | 550]]

**Registers Using Flip-Flops**
- a memory unit that stores a bit for 1+ clock cycles
![[Screen Shot 2024-02-05 at 1.56.05 PM.png | center | 550]]![[Screen Shot 2024-02-05 at 1.57.53 PM.png | center | 550]]

**3-Bit Counter Using a Register + Ripple-Carry Adder**
![[Screen Shot 2024-02-05 at 1.59.12 PM.png | center | 500]]
##### Exam Questions
![[Screenshot 2024-09-12 at 9.58.01 PM.png | center ]]