#### Toy ISA
##### ISA extended R=1
![[Screen Shot 2024-02-25 at 10.36.11 PM.png | center | 500]]

1. R2 = first parameter
2. R3 = second parameter
3. R0 = return value of the function
4. save registers before modifying and restore them before returning
5. use 0xFF for halt instead of 0x80
##### Functions
- save registers before modifying and restore them before returning
- use 0xFF for halt instead of 0x80

1. R2 = first parameter
2. R3 = second parameter
3. R0 = return value of the function

**Recursive Sum Function Example**
![[Screen Shot 2024-02-25 at 11.52.11 PM.png | center | 200]]
![[Screen Shot 2024-02-25 at 11.51.26 PM.png]]
#### Assembly
##### Assembly Syntax
**Register Aliasing**
- RAX: 64 bits
- EAX: lower 32 bits
- AX: lower 16 bits, split into AH (higher 8) and AL (lower 8)
![[Screen Shot 2024-02-26 at 2.32.07 PM.png | center | 450]]

**AT&T Syntax**
- $: value of constant 
- %: value in register
- 0x: value at memory address
- ( ): value at memory address of register

**Example Usage**
```
movl $10, %eax // Move the constant value 10 into the EAX register

movl 0x1234, %eax // Move the value stored at memory address 0x1234 into EAX

addl 4(%ebx), %edx // Add the value at memory address EBX+4 to the contents of EDX
```

![[Screen Shot 2024-02-28 at 2.07.48 PM.png | center | 250]]
##### Computed Addresses
- **displacement(base, index, scale) = base + (index * scale) + displacement**
- base = starting point in memory
- scale = size of value (limited to 1, 2, 4, 8)
- displacement and base are signed
![[ComputedMemory | 600]]

**Computed Address Example**
![[ComputedAddressExample | 600]]
##### Calling Convention
**Caller**
![[Screen Shot 2024-03-14 at 1.38.45 PM.png | center | 400]]

**Callee**
![[Screen Shot 2024-03-14 at 4.18.14 PM.png | center | 400]]
##### Stack Frames
**Contains:**
1. local storage of variables (optional)
2. temporary scape (optional)
3. return address

- stack pointer %rsp points to the top of the stack
- frame pointer %rbp points to the base of the frame (optional)
![[Screen Shot 2024-03-14 at 4.24.04 PM.png | center | 300]]

![[Screen Shot 2024-03-14 at 4.29.16 PM.png | center | 300]]
##### cmp, test, and jmp
**Compare (CMP) Instruction**
- subtracts but doesn’t store result
- `cmp %rax, %rdi -> rdi-rax`

**Test Instruction**
- computes bitwise and
- `test %rax, %rdi -> rdi & rax`

**Jumps**
- `jle, jg, je` read condition codes following a comparison
	1. CF: carry flag(for unsigned)
	2. SF: sign flag (for signed negatives)
	3. ZF: zero flag
	4. OF: overflow flag (for signed overflow)

![[Screen Shot 2024-03-14 at 5.27.33 PM.png | center | 400]]

**Computed Jumps**
![[Screen Shot 2024-03-14 at 5.48.01 PM.png | center | 400]]
##### Overlapping Registers
- setting 32-bit registers clears the corresponding 64-bit register
```
movq $0xFFFFFFFFFFFFFFFF, %rax
movl $0x1, %eax

// %rax is $0x1, not $0xFFFFFFFF00000001
```

- setting 8 or 16-bit registers does not clear the 64-bit register
```
movq $0xFFFFFFFFFFFFFFFF, %rax
movb $0x1, %al

// %rax is $0xFFFFFFFFFFFFFF01
```
##### movq and leaq
**movq**
- can be used to perform pushing and popping
- uses subsections of rsp/rbp rather than multiple registers
- `-4(%rsp)`: value at the memory of rsp - 4
![[Screen Shot 2024-03-14 at 11.33.03 AM.png]]

**movq vs leaq**
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
rdx <- address-of(memory[rbx + rcx])
```
##### Switch Statement and Jump Tables
**General Form**
![[Screen Shot 2024-03-25 at 8.09.29 PM.png | center | 450]]

**Example**
![[Screen Shot 2024-03-25 at 8.20.03 PM.png | center | 500]]

- for fall through cases, add an extra label for the fall and its instruction
- when it is case 2, it will not perform w = 1
![[Screen Shot 2024-03-25 at 8.25.30 PM.png | center | 400]]
#### C
##### C Syntax
**Types**
- each type has a certain size
![[Screen Shot 2024-03-26 at 10.05.33 AM.png | center | 150]]

```C
int x = 3;
int number_of_bytes = sizeof(x);    // sizeof(x) returns 4
```

**Variables**
`int [variable_name];    // declares an integer variable`
- 32 bits from a 64 bit address are dedicated to storing the integer value
![[Screen Shot 2024-03-26 at 2.04.05 PM.png | center | 350]]

- uninitialized variables are free-floating and their value may change
![[Screen Shot 2024-03-26 at 2.13.49 PM.png | center | 500]]

**printf**
- follows the format `printf([specifier], [argument])`
![[Screen Shot 2024-03-26 at 10.40.07 AM.png | center | 400]]

**scanf**
- performs a formatted read
![[Screen Shot 2024-03-27 at 12.39.08 AM.png]]

**Pointers**
`int *pointer = &variable;    //& gives the address of the variable`
- hold memory addresses
- uninitialized pointers are also free-floating

`int variable2 = *pointer` sets variable2 to the value the pointer points to

`*pointer = 4` goes to the memory location and sets the value to 4
##### Pointers
**Pointer Rules**
1. `[type] *[variable_name]` is a declaration
2. `*[variable_name] = ` means go to the address stored at the pointer and update it
3. ` = *[variable_name]` means go to the address stored at the pointer an retrieve the value
4. ` = &[variable_name]` means get the address of the variable

**Pointers Example**
![[Screen Shot 2024-03-28 at 11.51.36 AM.png | center | 400]]

**Pass by Value**
- can’t pass references, must pass an address that gets stored in a pointer

**Pass by Value Example**
![[Screen Shot 2024-03-28 at 12.15.18 PM.png | center | 450]]

**Pointer to a Pointer**
![[Screen Shot 2024-04-02 at 11.39.08 AM.png | center | 500]]

![[Screen Shot 2024-04-02 at 11.43.38 AM.png | center | 500]]

**Null Pointer**
- pointer that does not point to any memory location
```C
#include<stdio.h>
#define NULL 0

int main)(){
	int *ptr = NULL;
	printf("%d", *ptr);    // dereferencing NULL can crash the program
	return 0;
}
```

**Void Pointer**
- generic pointer type that can point to any data type
- can’t be dereferenced, need to cast
```C
int a = 7;
char x = 'y';

void *p = NULL;
p = &a;
p = &x;    // valid!

char q = *p;    // NOT ALLOWED

// cast p to a char*
// derefence to get char
char q = *((char*)p);
```
##### Arrays
**Example Implementation**
```C
// declaration and initialization
// a slot (4-bytes wide for int) is allocated on the stack for each element
// x is the location in memory that holds the address of the first element

int x[4] = {1,2,3,4};

int variable = x[0];    // accessing

int totalNumberOfBytes = sizeof(x);    // = 16 (4 elements * 4 bytes)

*x = 7;    // goes to the address x points to and sets it to 7

*(x + 2) = 5;    // in Assembly, x + 2 would be represented as 0xDD + 8
```
 ![[Screen Shot 2024-04-03 at 6.31.57 PM.png | center | 500]]
**Array Accesses Examples**
![[Screen Shot 2024-03-28 at 2.10.34 PM.png | center | 450]]

**Array Nuances**
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

**Two-Dimensional Arrays**
- arrays must be stored in 1-dimension
- row-major ordering: rows are stored stacked one after the next
![[Screen Shot 2024-04-02 at 12.45.45 PM.png | center | 400]]
##### Strings
**Char Array**
```C
// the string is stored in the code section, so it is not writable
// message is a pointer -> message and &message are NOT the same
char *message = "hello";

// a copy of the string is stored on the stack
// message is an array -> message and &message are the same
// the '\0' is a null byte used to terminate the string
char message[6] = {'h', 'e', 'l', 'l', 'o', '\0'};
```

**String Helper Functions**
```C
// size_t is a flexible type that stores the int size of the pointer (32 or 64)
// size_t is unsigned, ssize_t is signed
// const keyword defines immutable variables
size_t strlen(const char *str)
```

**Array of Strings**
![[Screen Shot 2024-04-02 at 12.33.00 PM.png | center | 400]]
![[Screen Shot 2024-04-02 at 12.34.20 PM.png]]
![[Screen Shot 2024-04-02 at 12.34.58 PM.png | center | 400]]

**String Array Access**
```C
// accesses the letter at index 2 of the word at index 1
strings[1][2] <-> (*(strings + 1))[2] <-> *((*(strings + 1)) + 2)

OR

char **x = strings;
x[1][2] <-> (*(x + 1))[2] <-> *((*(x + 1)) + 2)
```
##### Command Line Arguments
- the first element in the `argv` array is the name of the program itself
- when you call `./a.out Hello` it will print `a.out`
```C
int main(int argc, char **argv){
	if (argc > 0){
		printf("argument was %s", *argv);
	}
}
```

- to print `Hello`:
```C
int main(int argc, char **argv){
	if (argc > 0){
		printf("argument was %s", *(argv + 1));    // or argv[1]
	}
}
```
##### typedef, struct, and union
**typedef**
- allows you to provide an alias for a type
- `typedef [type_info] [new_name];`

**typedef Example**
```C
typedef char* string;

string name = "Daniel";    // improves readability!
string AI = "maybe";

printf("%s\n, name");
```

**struct**
- composite data type that allows you to group variables of different data types under a single name

**struct Example**
```C
struct student {    // the struct name (in this case "student") is optional
	int year;    // members of the struct...
	float grade;
};    // semicolon at the end!!

struct student daniel;    // OR use typedef
// typedef struct student studentType
daniel.year = 4;
daniel.graded = 77.7;
```

**Combining typedef and struct**
```C
typedef struct student {
	int year;
	float grade;
} studentType;

// further optimized to:

typedef struct {
	int year;
	float grade;
} studentType;
```

**Structs and Pointers**
- `(*pointer).member` can be written as `pointer->member`
- more flexibility than dot notation

```C
typedef struct {
	char name[50];
	float grade;
} studentType;

studentType daniel;
studentType *pointer = &daniel;

pointer->grade = 77.7;
float grade = pointer->grade;
printf("grade %0.2f", grade);
```

**Structs in Memory**
- structs are represented as a block of memory big enough to hold all fields
- fields are ordered according to the order they appear in code
- type information is lost
![[Screen Shot 2024-04-02 at 1.12.18 PM.png]]

**union**
```C
int main(){
	union {       // similar to structs but
		int x;    // x and c both access the same space in memory
		char c;
	} ascii;
	
	ascii.x = 65;
	prinft("%d\n", ascii.x);    // prints 65
	prinft("%c\n", ascii.x);    // prints A

	return 0;
}
```
##### The Heap
- the heap is used for dynamic memory allocation
- it can be explicitly managed using the functions `malloc`, `calloc`, `realloc`, and `free`

**malloc** (memory allocation)
```C
// allocates a block of a specified size
// args: # of bytes to allocate
void* malloc(size_t size);

// since the turn type is a void pointer, it must be cast when called
// memory is simply allocated, not set
int *a = (int *)malloc(sizeof(int) * 8);
```
![[Screen Shot 2024-04-02 at 1.41.50 PM.png]]

**calloc** (contiguous allocation)
```C
// allocates a block of memory for an array of elements
// args: # of elements and the size of each element
// sets memory to 0
void* calloc(size_t nmemb, size_t size);
```
![[Screen Shot 2024-04-02 at 1.42.06 PM.png]]

**realloc** (reallocation)
```C
// changes the size of the previously allocated memory block
// args: pointer to the memory to resize, new size in bytes
// memory in newly reserved space is not set
void* realloc(void *ptr, size_t size);
```
![[Screen Shot 2024-04-02 at 1.42.20 PM.png]]

**free**
```C
// disassociates a pointer from a region of memory
// dangerous because the disassociated pointer still holds its value
void free(void *ptr);

// TO FIX THIS: set the pointer to null once freed
free(p);
p = NULL;
```