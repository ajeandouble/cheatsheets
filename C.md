# C cheatsheet and random shit...

## Resources 

[C-Faq](http://c-faq.com/)
[How I program C - Eskil Steenberg](https://youtu.be/443UNeGrFoM)

[Harder,Better, Faster, Stronger code](https://hbfs.wordpress.com/)
[Crafting interpreters](https://craftinginterpreters.com/)
[Linux Container in 500 lines](https://blog.lizzie.io/linux-containers-in-500-loc.html
)
[Simple memory alocator](https://arjunsreedharan.org/post/148675821737/write-a-simple-memory-allocator)
[Learning C projects ideas](https://arjunsreedharan.org/post/148675821737/write-a-simple-memory-allocator)

### Bookz

[https://freecomputerbooks.com/](https://freecomputerbooks.com/)
C in depth

## Random things to investigate

https://cellperformance.beyond3d.com/articles/2006/06/understanding-strict-aliasing.html

https://stackoverflow.com/questions/98650/what-is-the-strict-aliasing-rule

[Compression algorithms - Michael Dipperstein's Page O'Stuff](http://michael.dipperstein.com/index.html)

Strict aliasing rule
https://stackoverflow.com/questions/98650/what-is-the-strict-aliasing-rule

*How to continue execution after a SIGSEGV*
https://stackoverflow.com/questions/3291382/coming-back-to-life-after-segmentation-violation

Unit testing, Unit testing macros

## Notes on C

### Scope

You can have a scope without anything to isolate variables from their outer scope.

```
int main() { int i = 2; printf("%d", i); { int i = 4; printf("%d", i) } printf("%d", i); } // 242\0
```

>C language has the concept of variable scope. Ina a nutshell, each pair of { and } introduce new scope, and variables are bound to those scopes. You can declare variables with the same name, as long they are in different scopes.

[Redeclaring variables in C - Stack Oveflow](https://stackoverflow.com/questions/41993585/redeclaring-variables-in-c)

### Storage classes

| Specifier | Storage       | Initial Value | Scope      | Life         |
|-----------|---------------|---------------|------------|--------------|
| auto      | Stack         | Garbage        | In block   | End of block |
| extern    | Data Segment  | Zero          | Global     | Program life |
| static    | Data segment  | Zero          | In block   | Program life |
| register  | CPU Register? | Garbage       | In block   | End of block |

#### Extern

[Use of extern to share variables between source files - Stack Overflow](https://stackoverflow.com/questions/1433204/how-do-i-use-extern-to-share-variables-between-source-files)
[How to correctly use the extern keyword in C - Stack Overflow](https://stackoverflow.com/questions/496448/how-to-correctly-use-the-extern-keyword-in-c)

Extern keyword can be used inside a function. It informs the compiler the variable is not in the same file. We usually declare extern variables in the .h so we don't need to use that keyword.

```
/* main.c
** gcc main.c 2.c -o extern
*/
int main() { extern int a; a = 5; f();}
```

```
// 2.c
int a; f() { printf("%d", a); }
```

>Since functions are visible throughout the program by default, the use of extern is not needed in function declarations or definitions. Its use is implicit. When extern is used with a variable, it's only declared, not defined.

>When extern is used with a variable, it’s only declared, not defined.
As an exception, when an extern variable is declared with initialization, it is taken as the definition of the variable as well.


#### Automatic

Variables in function scope are implicitly declared as automatic (*auto*).

#### Static

```
static inline int pow(int n) { return n * n; }
```

Don't confuse static used in function scope with static used in the global scope. It means the variable can only be accessed from that file.

### Memory

#### Virtual addresses

>In all modern OSes (Windows, Linux, BSD, etc), all addresses in a userspace application are virtual addresses. The exceptions to this are certain RTOSes or other custom bare-metal applications.


#### Segments


[Do pointers refer to physical or virtual memories](https://stackoverflow.com/questions/55415778/do-pointers-refer-to-physical-or-to-virtual-memories)

Ld is responsible for making the segments mapping and setting rwx permissions.

| Segment  | Description                                                 |
|----------|-------------------------------------------------------------|
| Text     | Executable instructions                                     |
| Data     | Global and static variables with predefined values          |
| BSS      | Undefined global and static                                 |
| Stack    | LIFO. Converges to Heap.                                    |
| Heap     | Dynamically alocated variables. Converges to Stack          |

```
char *a = "ABCD"; // .rodata (modifying causes SIGSEGV)
char b[] = "ABCD"; // Data

int c; // BSS

int main() {
        static int d; // BSS
        char *d = "ABCD"; // .rodata (modifying causes SIGSEGV)
        char e[] = "ABCD"; // Stack
        char *f = strdup("ABCD"); // Heap
        // <- code instructions in Text
```

#### .rodata

Some compilers also use a data segment called .rodata as in read-only data to store string literals and sometimes const.

#### How to see segments mapping

```
(gdb) info proc
process 8596
cmdline = '/home/guy/blog/string_elf/a.out'
cwd = '/home/guy/blog/string_elf'
exe = '/home/guy/blog/string_elf/a.out'

(gdb) shell cat /proc/8596/maps
00400000-00401000 r-xp 00000000 fd:02 134817229 ...
00600000-00601000 r--p 00000000 fd:02 134817229 ...
00601000-00602000 rw-p 00001000 fd:02 134817229 ...
```

[From Rodata to RwData - https://guyonbits.com/from-rodata-to-rwdata-introduction-to-memory-mapping-and-ld-scripts/]

#### Symbols

Without adres randomization (ASLR), the variable address is exactly the same as the one found in the symbol table.

```shell
$ gcc code.c -no-pie -o executable
$ objdump --syms executable | grep variable
0804a020 g     O .bss	00000004              variable
```

```
printf("%p", &variable); // 0x804a020
```

#### Executable stack

*-z execstack* marks the object as requiring executable stack.

*-fstack-protector* allocates a little more space on the stack and adds a stack guard (canary) to protect against buffer overflows.

### Preprocessor

```
#define FORTYTWO 42
int main() { int i = FORTYTWO; } // gcc -E fortytwo.c
```

[Can gcc output code after preprocessing? - Stack Overflow]

#### Macros

We need to protect macro with parenthesis otherwise we can get non-desired results such as :

```
#define abs(x) x<0?-x:x // abs(2-3) translates to 2-3<0-2-3:2-3 -> -5
```

#### Debug Macro

```
#define DEBUG(fmt, ...) do { fprintf(stderr, fmt) } while(0) 
#### Offset Macro
```

```
#define offsetof(st, m) \
    ((size_t)&(((st *)0)->m))
```

[Ofsetof - Wikipedia](https://en.wikipedia.org/wiki/Offsetof)

### Types

```
printf("%d", sizeof('A')); // 4
```

#### Integers promotions

#### Type conversions

#### Floats

[What every programmer needs to know about floats - Oracle](https://docs.oracle.com/cd/E19957-01/806-3568/ncg_goldberg.html)

### Arrays

>Plain *array* decays to a pointer to its first element, it's equal to *&array[0]*.

[Why are arrays and array pointing to the same address?](https://stackoverflow.com/questions/54807208/why-are-array-and-array-pointing-to-the-same-address)

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

### Restrict

```
void f(int *restrict a, int *restrict b) {
    *a += *b;
    *b += *a;
}

// ...
int a = 2;
f(&a, &a); // returns 6
```
> gcc -O3 restrict.c -o restrict

[https://cellperformance.beyond3d.com/articles/2006/05/demystifying-the-restrict-keyword.html](Desmitifying the restrict keyword)

### Branchless programming

[Branchless programming examples](https://hbfs.wordpress.com/2008/08/05/branchless-equivalents-of-simple-functions/)

### Threads

### I/O

### Unit testing

#### The assert Macro

https://stackoverflow.com/questions/2486386/why-do-i-see-throw-in-a-c-library
assert.h source code from glibc

### GCC

### Misc

#### Coma operator

```
    if (1, 2, a = b) printf("Wow?");
```

(The Comma Operator - Wikipedia)[https://en.wikipedia.org/wiki/Comma_operator]