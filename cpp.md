# Fast-learning C++11 cheatsheet

## Resources

> Piscine CPP - 42

[Effective Modern C++](https://github.com/myluco/books-2/blob/master/Effective-Modern-C%2B%2B.pdf)
[The C++ - Bjarne Stroustrup](https://github.com/boydfd/books/blob/master/seeing/stalled/2013%20Stroustrup%20-%20The%20C%2B%2B%20Programming%20Language%204th%20Edition.pdf)
[C++ notes for professionals](https://github.com/AzatAI/cs_books/raw/master/CPlusPlusNotesForProfessionals.pdf)
[CopperSpice - Youtube](https://www.youtube.com/c/CopperSpice/videos)

## References

## Basics

### Most notable differences between C and C++

* Reference variables
* OOP
* Inheritance
* Data hiding
* New and delete operator for memory allocation/de-allocation
* Exceptions
* Lambdas (C++11)
* constexpr (C++11)
* ...

### Values semantics

[What are rvalues, lvalues... - Stackoverflow](https://stackoverflow.com/questions/3601602/what-are-rvalues-lvalues-xvalues-glvalues-and-prvalues)

## OOP

### Differences between C++ classes and C structures

* A class can contain methods
* Operators overloading
* Inheritance

### Differences between C++ classes and *C++* structures

> The only difference between a struct and class in C++ is the default accessibility of member variables and methods. In a struct they are public; in a class they are private.

[struct vs classes in C++](https://blogs.sw.siemens.com/embedded-software/2014/06/02/struct-vs-class-in-c/)

### Constructors/Destructors

[Rule of Three - Wikipedia](https://en.wikipedia.org/wiki/Rule_of_three_%28C++_programming%29)

#### **Copy constructors**

### Members

There are three access specifiers in C++
>***Public*** - members are accessible from outside the class
>***Private*** - members cannot be accessed (or viewed) from outside the class
>***Protected*** - members cannot be accessed from outside the class, however, they can be accessed in inherited classes.

### Access specifiers

> ***Public*** - members accessible outside the class through the instancied object
>
> ***Private*** - members not accessible outside the class
>
> ***Protected*** - members not accessible outside the class but can be accessed

### **Inheritance**

[Multiple inheritance - same variable name - StackOverflow](https://stackoverflow.com/questions/19763903/multiple-inheritance-same-variable-name)

[Struct inheritance in C++ - Stackoverflow](https://stackoverflow.com/questions/979211/struct-inheritance-in-c)

##### Inheritance access specifier

**Public inheritance**

>***Public*** → ***Public***
>
>***Protected*** → ***Protected***
>
>***Private*** → ***Private***

**Protected inheritance**

>***Public*** → ***Protected***
>
>***Protected*** → ***Protected***
>
>***Private*** → *********Not herited*** (not accessible from instance of derived class)

**Private inheritance**

> ***Public*** → ***Private***
>
> ***Protected*** → ***Private***
>
> ***Private*** → *********Not herited*** (not accessible from instance of derived class)

### Virtual base classes

[Virtual Base Classes - microsoft](https://docs.microsoft.com/en-us/cpp/cpp/multiple-base-classes?view=msvc-170)


### Operators overloading

>  Watch out that if you try to use `return *this;` on a function whose return type is `Type` and not `Type&`, C++ will try to make a copy of the object and then immediately call the destructor, usually not the intended behaviour. So the return type should be a reference as in your example.
>
> 

[What does return *this means in CPP - StackOverflow](https://stackoverflow.com/questions/18162522/what-does-return-this-mean-in-c)

***Why do we use const & for assignation overloading.***

***Why we don't use this in operator= (for example. check others)***

## Typedef vs using

[What is the difference between typedef and using in C++11](https://stackoverflow.com/questions/10747810/what-is-the-difference-between-typedef-and-using-in-c11)

## Iterators

## Casting

```
Use dynamic_cast for converting pointers/references within an inheritance hierarchy.
Use static_cast for ordinary type conversions.
Use reinterpret_cast for low-level reinterpreting of bit patterns. Use with extreme caution.
Use const_cast for casting away const/volatile. Avoid this unless you are stuck using a const-incorrect API.
```
[When should static_cast, const_cast, dynamic_cast and reinterpret_cast be used](https://stackoverflow.com/a/332070/12692151)

## Smart pointers


### C++ STL

#### std::vector

#### std::map



## Shit yet to explore

* Coroutines
https://opensource.com/article/21/2/ccc-method-pointers
