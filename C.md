# C cheatsheet and random shit...

## Resources 

[C-Faq](http://c-faq.com/)
[How I program C - Eskil Steenberg](https://youtu.be/443UNeGrFoM)

### Bookz

[https://freecomputerbooks.com/](https://freecomputerbooks.com/)
C in depth

## Random things

https://cellperformance.beyond3d.com/articles/2006/06/understanding-strict-aliasing.html

https://stackoverflow.com/questions/98650/what-is-the-strict-aliasing-rule

[Compression algorithms - Michael Dipperstein's Page O'Stuff](http://michael.dipperstein.com/index.html)

Strict aliasing rule
https://stackoverflow.com/questions/98650/what-is-the-strict-aliasing-rule

### Storage classes

| Specifier | Storage       | Initial Value | Scope      | Life         |
|-----------|---------------|---------------|------------|--------------|
| auto      | Stack         | Garabge       | In block   | End of block |
| extern    | Data Segment  | Zero          | Global     | Program life |
| static    | Data segment  | Zero          | In block   | Program life |
| register  | CPU Register? | Garbage       | In block   | End of block |

**Extern**

[Use of extern to share variables between source files - Stack Overflow](https://stackoverflow.com/questions/1433204/how-do-i-use-extern-to-share-variables-between-source-files)
[How to correctly use the extern keyword in C - Stack Overflow](https://stackoverflow.com/questions/496448/how-to-correctly-use-the-extern-keyword-in-c)

**??? -> int main() { extern int i; } // what does it do?**


**Automatic**

Variables in function scope are implicitly declared.



### Arrays

### Array initialization

```
int array[] = {1, 2, 3, 4, 5 }; 						// 1, 2, 3, 4, 5
int array2[5] = {1, 2};         						// 1, 2, 0, 0, 0
int array3[5] = {1, };          						// 1, 0, 0, 0, 0
int array4[5] = { [0 ... 1] = 1, [2 ... 3] = 2 };   				// 1, 1, 2, 2, 0
int array5[] = { [0 ... 2] = 1, [2 ... 3] = 3, [ 1 ... 4 ] = 5 }; 		// 1, 5, 5, 5, 5
int array6[] = { [4] = 1, [1 ... 2] = 1, [2 ... 3] = 2, [1] = 8, [1] = 9 }; 	// 0, 9, 2, 1
```

#### String literals VS Arrays

```
char *s_array[] = "ABC"; // equivalent to char s_array = {'A', 'B', 'C', '\0'}. On stack if automatic variable.
char *str = "ABC"; // .rodata if compiled with gcc (read-only memory)
```
[String Literals. Where do they go? - StackOverflow](https://stackoverflow.com/questions/2589949/string-literals-where-do-they-go)

#### Variable Length Array

VAL were introduced in C99 standard.

```
scanf( "%d", &numElements);
if(numElements <= 0) return ;
double data[numElements];
```

[VLA Gnu Extension](https://gcc.gnu.org/onlinedocs/gcc/Variable-Length.html)


### Struct


#### Many ways to declare a struct


#### Anonymous struct


### Unions

The memory occupied by a union will be large enough to hold the largest member of the union.



### Functions



#### Variable arguments list

[How Variable arguments list work in C](https://blog.aaronballman.com/2012/06/how-variable-argument-lists-work-in-c/)



### Threads

### I/O

### Unit testing

#### The assert Macro

https://stackoverflow.com/questions/2486386/why-do-i-see-throw-in-a-c-library
assert.h source code from glibc

