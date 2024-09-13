##### C Main Entry
![[Screen Shot 2024-03-26 at 9.45.28 AM.png | center | 500]]

**Status Codes**
![[Screen Shot 2024-03-26 at 9.50.13 AM.png | center | 350]]

**Debugging**
- `clang -g puts.c -o puts.out`: the -g flag allows for line level debugging
- `lldb` allows you to step into a function and see the corresponding assembly
##### C Syntax
**Types**
- each type has a certain size
![[Screen Shot 2024-03-26 at 10.05.33 AM.png | center | 150]]

```C
int x = 3;
int number_of_bytes = sizeof(x);    // sizeof(x) returns 4
```

**printf**
- follows the format `printf([specifier], [argument])`
![[Screen Shot 2024-03-26 at 10.40.07 AM.png | center | 400]]

**Variables**
`int [variable_name];    // declares an integer variable`
- 32 bits from a 64 bit address are dedicated to storing the integer value
![[Screen Shot 2024-03-26 at 2.04.05 PM.png | center | 350]]

- uninitialized variables are free-floating and their value may change
![[Screen Shot 2024-03-26 at 2.13.49 PM.png | center | 500]]

**Pointers**
`int *pointer = &variable;    //& gives the address of the variable`
- hold memory addresses
- uninitialized pointers are also free-floating

`int variable2 = *pointer` sets variable2 to the value the pointer points to

`*pointer = 4` goes to the memory location and sets the value to 4

##### scanf and the Stack
- `scanf`: performed a formatted read
![[Screen Shot 2024-03-27 at 12.39.08 AM.png]]
