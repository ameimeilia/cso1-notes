##### Bytes and Padding
```C
#include <stdio.h>
#include <stdint.h>

// Define a struct with three members shorts, char, char
typedef struct {
	short a;
	char b;
	char c;
} StructA;

typedef struct {
	char x;
	short y;
} StructB;

int main() { 
	// An array of hexadecimal values
	uint8_t hexArray[] = {0x12, 0x34, 0x56, 0x78};
	
	// Cast the array to StructA and access its members
	StructA *structA = (StructA*)hexArray;

	// Prints a = 0x3412, b = 0x56, c = 0x78
	printf("StructA: a = 0x%x, b = 0x%x, c = 0x%x\n", structA->a, structA->b, structA->c);

	// Cast the array to StructB and access its members
	StructB *structB = (StructB*)hexArray;

	// prints x = 0x12, y = 0x7856
	// 0x34 is ignored because padding is added after x
	printf("StructB: x = 0x%x, y = 0x%x\n", structB->x, structB->y);
	
	return 0;
}
```
##### Data as Code
```C
#include <stdio.h>
#include <stdint.h>

// Define a function pointer type
typedef int (*func_ptr)();

int main() {
	// puts hex instructions on the stack
	uint8_t code[] = {0xb8, 0x07, 0x00, 0x00, 0x00, 0xc3 };
	
	// Cast the array to a function pointer
	func_ptr func = (func_ptr)code;
	
	// Call the function through the pointer
	int result = func();

	// when compiled w/ special command, forces the stack to be executed
	printf("Function returned: %d\n", result);
	
	return 0;
}
```

![[Screen Shot 2024-04-30 at 4.41.09 PM.png]]

**Dangers**
- ASCII characters encoded to hex can represent instructions
![[Screen Shot 2024-04-30 at 4.46.18 PM.png]]
##### gets Function
```C
#include <stdio.h>

void vulnerable_function() {
	char buffer[7];
	printf("Enter some text:\n");

	// gets doesn't check the bounds of the buffer -> memory leaks
	gets(buffer);
	
	printf("You entered: %s\n", buffer);
}
	
int main() {
	vulnerable_function();
	return 0;
}
```

- if more than 7 chars are entered, it bleeds into the return address
- limitations: buffer needs to be long enough, stack has to be executable, address space randomization turned off
![[Screen Shot 2024-04-30 at 4.54.35 PM.png | center | 300]]
##### Socket and Buffer Overflows
- to fix the vulnerabilities with the `gets()` function, read from a socket
```C
#include <stdio.h>

void vulnerable_function(int sockfd) {
	char buffer[7];
	fgets(s);
}

int main() {
	vulnerable_function();
	return 0;
}
```

![[Screen Shot 2024-04-30 at 4.59.36 PM.png]]

**Error Practice**
```C
int copy_something(char *buf, int len) {
	char kbuf[800];

	// if we pass in -1 for len, it passes the > sizeof(kbuf) check
	if(len > sizeof(kbuf)) {
		return -1;
	}

	// 0xffffff memory is copied and the buffer gets overflowed
	memcpy(kbuf, buf, len);
	return len;
}

// size_t is unsigned, so -1 is 0xffffff
extern void * memcpy(void *dst, const void *src, size_t n);
```