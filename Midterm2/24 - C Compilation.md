##### Pointer Rules
**Rule 1**
- `[type] *[variable_name]` is a declaration
- reserve a memory location on the stack to store an address
- ex. `int *p;`
![[Screen Shot 2024-03-28 at 11.35.04 AM.png | center | 400]]

**Rule 2**
- `*[variable_name] = ` means go to the address stored at the pointer and update it
- ex. `*p = 4`
![[Screen Shot 2024-03-28 at 11.35.46 AM.png | center | 400]]

**Rule 3**
- ` = *p` means go to the address stored at the pointer an retrieve the value
- ex. ` = *p -> = 4`

**Rule 4**
- ` = &p` means get the address of the variable
- ex ` = &p -> = 0x...0006`
![[Screen Shot 2024-03-28 at 11.37.56 AM.png | center | 400]]

**Example**
![[Screen Shot 2024-03-28 at 11.51.36 AM.png | center | 400]]
##### Pass by Value
**Pass by Reference Example**
- variables in main are unchanged by the swap function
![[Screen Shot 2024-03-28 at 12.05.46 PM.png | center | 450]]

- to fix this, pass an address that gets stored in a pointer
![[Screen Shot 2024-03-28 at 12.08.36 PM.png | center | 450]]

**Fixed Example**
![[Screen Shot 2024-03-28 at 12.15.18 PM.png | center | 450]]
##### Arrays
**Declaration and Initialization**
- `[type] [array_name][size];`
- `[type] [array_name][size] = {...};`

**Representation in Memory**
- a slots is allocated on the stack for each element in the array
- the width of the slot is dependent on the data type
- ex. `int myArray[4] = {1,2,3,4};`
![[Screen Shot 2024-03-28 at 1.35.45 PM.png | center | 250]]

**Accessing Elements**
- `[type] [variable_name] = [array_name][index];`
- ex. `int variable = myArray[0];`

**Setting Elements**
- `[array_name][index] = [value];`
- ex. `myArray[0] = 3;`

**sizeof Array**
- return the total number of bytes in the array
```C
int x[4] = {1,2,3,4};
int totalNumberOfBytes = sizeof(x);    //4*4 = 16

int x[4] = {'A','B','C','D'};
int totalNumberOfBytes = sizeof(x);    //4*1 = 4
```

**Array Syntax and Pointers**
- in the example `int x[4] = {1,2,3,4};` x is the location in memory that holds the address of the first element in the array
![[Screen Shot 2024-03-28 at 1.43.00 PM.png | center | 250]]

**Setting Values Using Pointers**
```C
int x[4] = {1,2,3,4};
*x = 7;    // goes to the address x points to and sets it to 7
```
![[Screen Shot 2024-03-28 at 1.44.29 PM.png | center | 250]]

```C
*(x + 1) = 7;
```
- in Assembly, `x + 1` would be represented as `0xDD + 4
- in pointer arithmetic, constants are treated as multiples of the size of the pointer type

```C
*x = *x + 1;
```
- at the value x points to, set that equal to the value x points to + 1
![[Screen Shot 2024-03-28 at 2.16.58 PM.png | center | 450]]

**Array Accesses Examples**
![[Screen Shot 2024-03-28 at 2.10.34 PM.png | center | 450]]
##### Array Nuances
- arrays are not simply pointers, they are of type `int[n]`, meaning they cannot be assigned
```C
int x[4] = {1,2,3,4};
int y[5] = {1,2,3,4,5};
int *p;

x = y;    // NOT ALLOWED!!!

p = x;    // same as p = &(x[0])
x = p;    // not allowed, array is not assignable
```

**Examples**
![[Screen Shot 2024-03-28 at 3.50.36 PM.png | center | 500]]

![[Screen Shot 2024-03-28 at 3.52.58 PM.png | center | 500]]
##### Char Array and Strings
```C
char message[6] = {'h', 'e', 'l', 'l', 'o', '\0'};    // declaring/instantiating

char *message = "hello";    // assigning
```
- the `'\0'` is a null byte used to terminate the string
- used to find the length of the string: iterate until the null byte