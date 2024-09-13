---
layout: default
title: Bitwise
---
##### Negative Numbers
**Sign Bit**: the highest order bit indicates the sign of the number
- doesn’t work with ripple carry adders
- used in floating-point numbers
![[Screen Shot 2024-01-26 at 2.08.33 PM.png | 300]]   ![[Screen Shot 2024-01-26 at 2.09.45 PM.png | 300]]

**Bias**: find the middle number and have it represent 0
- doesn’t work with ripple carry adder
- addition, subtraction, and comparisons work the same for signed and unsigned numbers
- used to represent the exponents of floating-point numbers stored in binary scientific notation
![[Screen Shot 2024-01-26 at 2.13.32 PM.png | 300]]   ![[Screen Shot 2024-01-26 at 2.17.43 PM.png | 300]]
- to find the middle: $floor( (2^n - 1) / 2 )$
- to convert from decimal to bias: add N to the decimal value then convert as if unsigned
- from original to biased: representation = original + bias
- from biased to original: original = representation - bias
![[Screen Shot 2024-05-03 at 5.10.34 PM.png | center | 500]]

**Two complement**: top most bit represents negative $-2^n$
- works with ripple carry adder
- to convert from between signs:
	1. flip the bits
	2. add 1
- addition, subtraction, and multiplication work the same for signed and unsigned values
- used for signed integers
![[Screen Shot 2024-01-28 at 4.46.41 PM.png | 300]]   ![[Screen Shot 2024-01-26 at 2.21.23 PM.png | 300]]

**Overflow**: if $\oplus + \oplus = \circleddash, or \circleddash + \circleddash = \oplus$
- carry is not considered overflow
![[Screen Shot 2024-01-28 at 4.50.12 PM.png | 200]]   ![[Screen Shot 2024-01-28 at 4.50.26 PM.png | 200]]
##### Hexadecimals
- group the binary number into nibbles, convert, then put them together
- prefix for hex is 0x
![[Screen Shot 2024-01-26 at 2.41.44 PM.png | center | 300]]

![[Screen Shot 2024-01-28 at 10.08.42 PM.png | center | 350]]

##### Exam Questions
![[Screenshot 2024-09-12 at 9.52.27 PM.png | center]]