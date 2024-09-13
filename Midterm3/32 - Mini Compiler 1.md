##### ToyG Syntax
- only supports integers
```C
x = 3;    // = is a valid token
y = 4;    // in y <- 4, <- is an invalid token
```

**Defining Valid Tokens**
1. \[a-z]: single lowercase can be used to represent **variables**
2. \[0]\*: any number of zeros represent the **integer** 0
3. \[1-9]\[0-9]\*: also an **integer**, a number 1-9 followed by any number of digits 0-9
5.  ( ) < > = + * / ; { }: symbols
6. \n: new line character
7. #(.\*): # followed by any character 
8. ![[Screen Shot 2024-04-17 at 1.04.45 PM.png | center | 150]]
##### Lexing/Tokenizing
- source code → lexical analyzer → tokens
- Lex: tool that uses supplied patterns to output parsing code
![[Screen Shot 2024-05-05 at 3.03.09 PM.png | center | 400]]
- everything is already implemented in `lex.l` except `printcn`
##### Backus-Naur Form
- used to specify order of tokens
![[Screen Shot 2024-04-17 at 1.26.37 PM.png | center | 550]]
- everything is already implemented in `yacc.y` except `printcn`

![[Screen Shot 2024-04-17 at 1.30.25 PM.png]]

##### Union Structure in C
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

**Support for Multiple Node Types**
![[Screen Shot 2024-04-17 at 1.35.10 PM.png | center | 400]]

![[Screen Shot 2024-04-17 at 1.38.53 PM.png]]
![[Screen Shot 2024-04-17 at 1.41.04 PM.png]]
![[Screen Shot 2024-04-17 at 1.52.15 PM.png | center | 300]]
##### Overview
![[Screen Shot 2024-05-05 at 2.43.12 PM.png | center | 500]]