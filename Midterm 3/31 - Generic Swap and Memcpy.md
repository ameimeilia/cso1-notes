##### System Call Calling Convention
**1. Register Usage for Arguments**
1. `%rax`: system call number to tell the kernel
2. `%rdi, %rsi, %rdx, %r10, %r8, %r9`: used for passing up to 6 arguments
![[Screen Shot 2024-05-04 at 3.40.48 PM 1.png| center | 150]]

**2. Making the System Call**
1. `syscall` instruction switches into kernel mode and invokes the system call based on the value in `%rax`
![[Screen Shot 2024-05-04 at 3.25.25 PM.png | center | 300]]

 **3. Return Value**
 1. the return value is placed in `%rax`, indicates success or error code

**Example Implementation**
```C
.global _start
.text
_start:
	# write(1, message, 18)
	mov $1, %rax ;             // syscall number for write (1)
	mov $1, %rdi ;             // arg1, file descriptor 1 (stdout)
	lea message(%rip), %rsi ;  // arg2, load the address of the message
	mov $18, %rdx ;            // arg3, message length (18 bytes)
	syscall ;                  // perform the system call

.section .rodata ;             // Read-only data section
message: ;                     // Label for the message
	.ascii "Computer Systems 1" ;
```

![[Screen Shot 2024-05-04 at 3.32.11 PM 1.png]]
##### memcpy and memmove
**memcpy**
-  function in the C standard library, defined in <string.h>
- used to copy a specified number of bytes from one memory location to another
- don’t use with overlapping regions as it will result in undefined behavior
- returns a pointer to destination
```C
void *memcpy(void *dest, const void *src, size_t n);
```

**memcpy Example**
```C
#include <stdio.h>
#include <string.h>

int main() {
	char src[50] = "This is the source string.";
	char dest[50];
	
	// Copy src to dest
	// Added to make we get the null terminator
	memcpy(dest, src, strlen(src) + 1);
	printf("dest = \"%s\"\n", dest);
	return 0;
}
```

**memmove**
- safe to use when the source and destination memory regions overlap
```C
void *memmove(void *dest, const void *src, size_t n);
```

**memmove Example**
```C
#include <stdio.h>
#include <string.h>

int main() {
	char str[50] = "Hello, World!";
	
	printf("Original string: %s\n", str);
	memmove(str + 7, str + 0, 5);
	
	printf("After memmove: %s\n", str);    // prints "Hello, Hello!"
	return 0;
}
```
##### Generic Swap
```C
void swap(void *data1ptr, void *data2ptr, size_t nbytes) {
	// store a copy o fdata1 in temp storage
	void *temp = malloc(nbytes);
	memcpy(temp, data1ptr, nbytes);

	// copy data2 to the location of data1
	memcpy(data1ptr, data2ptr, nbytes);

	//copy data1 in temporary storage to the location of data2
	memcpy(data2ptr, temp, nbytes);

	free(temp);
}
```
##### strsep
```C
// stringp is a pointer to the string that we want to parse
// delim is a string that contains multiple delimiters
char *strsep(char **stringp, const char *delim);
```

![[Screen Shot 2024-05-04 at 4.25.15 PM 1.png]]

```C
#include <stdio.h>
#include <string.h>

int main() {
	char string[] = "a,b,c,d"; // The string to be tokenized
	char *token;
	char *rest = string;
	
	while ((token = strsep(&rest, ",")) != NULL) {
		printf("%s\n", token);
	}    // prints a \n b \n c \n d \n
	
	return 0;
}
```

![[Screen Shot 2024-05-04 at 4.32.02 PM 1.png| center | 200]]
