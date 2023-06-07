# Python3

## Resources

[Python Essential Reference - David Beazley](https://theswissbay.ch/pdf/Gentoomen%20Library/Programming/Python/Python%20Essential%20Reference%2C%20Fourth%20Edition%20%282009%29.pdf)

[cpython source code - realpython.com](https://realpython.com/cpython-source-code-guide/)


## Type and Objects

### Terminology

>***Every piece of data stored*** in a program is an **object**. Each object has an **identity**, a **type**
(which is also known as its class), and a **value**. For example, when you write a = 42, an
integer object is created with the value of 42.You can view the identity of an object as a
pointer to its location in memory. a is a name that refers to this specific location


>The type of an object, also known as the object’s class, describes the internal representation of the object as well as the methods and operations that it supports.

>An object that contains references to other objects is said to be a ***container*** or **collection**.

[Python Essential Reference - David Beazley](https://theswissbay.ch/pdf/Gentoomen%20Library/Programming/Python/Python%20Essential%20Reference%2C%20Fourth%20Edition%20%282009%29.pdf)

### Identity and Type

>The built-in function `id()` returns the identity of an object as an integer.This integer
usually corresponds to the object’s location in memory, although this is specific to the
Python implementation.

[Python Essential Reference - David Beazley](https://theswissbay.ch/pdf/Gentoomen%20Library/Programming/Python/Python%20Essential%20Reference%2C%20Fourth%20Edition%20%282009%29.pdf)

```python
import ctypes
our_var = 12
# base 10 memory address
print(f"id = {id(our_var)}") # pass by reference for id()
# hexadecimal memory address
print(f"hex id: = {hex(id(our_var))}") # pass by value for hex()
address = id(our_var)
# getting value from base 10 memory address 
print(f"Value from address {address} is {ctypes.cast(address, ctypes.py_object).value}")
```
[Memory Management in Pyton - medium](https://medium.com/analytics-vidhya/memory-management-in-python-4332fbf95cd0)

>Because the `isinstance()` function is aware of inheritance, it is the preferred way to
check the type of any Python object versus `type()`.


[Python Essential Reference - David Beazley](https://theswissbay.ch/pdf/Gentoomen%20Library/Programming/Python/Python%20Essential%20Reference%2C%20Fourth%20Edition%20%282009%29.pdf)


```python
>>> import sys
>>> a = 42
>>> sys.getrefcount(42)
1000000012
>>> b = 41
>>> sys.getrefcount(42)
1000000012
>>> b += 1
>>> sys.getrefcount(42)
1000000013
>>>
```

#### `is` operator

The is operator in Python is used to check whether two objects have the same identity, i.e., whether they refer to the **same memory location**. It compares the memory addresses of the objects.

```python3
>>> [1,2,3]==[1,2,3]
True
>>> [1,2,3] is [1,2,3]
False
>>> 42 is 42 # this is due to integer caching 42 is in range [-5, 256]
<stdin>:1: SyntaxWarning: "is" with a literal. Did you mean "=="?
True
>>>257 is 257
<stdin>:1: SyntaxWarning: "is" with a literal. Did you mean "=="?
False
```

### Mutability - Immutability

The enforcement of mutability and immutability is **built into the behavior of each object type,** and it **can not be modified or overridden** at runtime. It is a fundamental characteristic of the object type itself. It is described in the Python specifications.

When you perform operations on these objects, Python handles the details of accessing the object's value and performing the necessary computations. You don't directly access the memory addresses or low-level details of the objects in most cases. When you attempt to modify an object, **Python checks the type of the object** and determines whether it is mutable or immutable.

### Built-in types

|   Category   |     Name     |
|--------------|--------------|
| None         | `type(None)` |
| Numbers      | `int `       |
|              | `long`       |
|              | `float`      |
|              | `complex`    |
|              | `bool`       |
| Sequences    | `str`        |
|              | `unicode`    |
|              | `list`       |
|              | `tuple`      |
|              | `xrange`     |
| Mapping      | `dict`       |
| Sets         | `set`        |
|              | `frozenset`  |

#### User-defined functions

- `f._ _doc__` Documentation string
- `f.__name__` Function name
- `f.__dict__` Dictionary containing function attributes
- `f._ _code__` Byte-compiled code
- `f._ _defaults__` Tuple containing the default arguments
- `f._ _globals__` Dictionary defining the global namespace
- `f._ _closure__` Tuple containing data related to nested scopes

#### Methods

```python3
class Foo(object):
	def instance_method(self,arg): # self is the instance object
		pass
	@classmethod
	def class_method(cls,arg):	# cls is the class object
		pass
	@staticmethod
	def static_method(arg):
		pass
```

Both instance and class methods are of type `types.MethodType`

For user-defined classes, bound and unbound methods are both represented as an object of type types.MethodType, which is nothing more than a thin wrapper around an ordinary function object.The following attributes are defined for method objects:

- `__doc__` Docstring
- `__name__` Method name
- `__class__` Class in which method is defined
- `__func__` Function object implementing the method
- `__self__` Instance associated (`None` if unbound)


## Structure and control flow

### Scope

```python3
a = 42
def f():
    b = 42
    c = 42
    def nested_function():
        nonlocal c
        a = -42
        b = 41
        c = 41
        print(a, b, c) # -42 41 41

    global a
    a -= 1
    print(a, b, c) # 41 42 42
    nested_function()
    print(a, b, c) # 41 42 41

f()
```

### Closures

```python3
x = 42
def f() -> str:
    return f'x = {x}'

def callf(f: callable) -> None:
    return f

x = -42
_callf = callf(f)
print(_callf()) # -42


def f2() -> str:
    import random
    x = random.randint(0, 10000)
    print(x)
    def nested() -> str:
        return f'x = {x}'

    return nested

nested_f = f2()
nested_f_2 = f2()

print(f'nested_f={nested_f()}, nested_f_2={nested_f_2()} - {nested_f() == nested_f_2}')
# ... ... False
```

### Custom exceptions

```python3
class CustomException(Exception):
	pass
raise CustomException
```

### `with` statement

```python3
with open("file") as f:
	f.write("whatever")
	# code that might causes an exception
	f.write("something else")
# file descriptor even in case an exception was thrown
```

>The with obj statement allows the object obj to manage what happens when control-flow enters and exits the associated block of statements that follows.When the with obj statement executes, it executes the method ```obj.__enter__()`` to signal that a new context is being entered. When control flow leaves the context, the method `obj.__exit__(type,value,traceback)` executes.

>If no exception has been raised, the three arguments to __exit__() are all set to None. Otherwise, they contain the type, value, and traceback associated with the exception that has caused control-flow to leave the context.The __exit__() method returns True or False to indicate whether the raised exception was handled or not (if False is returned, any exceptions raised are propagated out of the context).

[Python - Essential Reference - David Beazley](https://theswissbay.ch/pdf/Gentoomen%20Library/Programming/Python/Python%20Essential%20Reference%2C%20Fourth%20Edition%20%282009%29.pdf)

### Coroutines

```python3
def receiver():
    print("Ready to receive")
    while True:
        n = (yield)
        ret = yield 42
        print("Got %s" % n)

r = receiver()
val = r.__next__()
print(val)
val = r.send(-42)
print(val)
```
>A function that uses yield in this manner is known as a coroutine, and it executes in response to values being sent to it. Its behavior is also very similar to a generator.

### List comprehensions

```python3
[expression for item1 in iterable1 if condition1
	for item2 in iterable2 if condition2
	... 
	for itemN in iterableN if conditionN ]
```
is equivalent to :

```python3
s = []
for item1 in iterable1:
	if condition1:
		for item2 in iterable2:
			if condition2:
			...
			for itemN in iterableN:
				if conditionN:
					s.append(expression)
```


## OOP

### Polymorphism, Dynamic Binding and Duck Typing

### `@property`

```python3
class Circle(object):
	def __init__(self,radius):
	self.radius = radius

	# Some additional properties of Circles
	@property
	def area(self):
		return 2 * math.pi * self.radius
>>> c = Circle(4.0)
>>> c.area
50.26548245743669
>>> c.area = 2
Traceback (most recent call last):
File "<stdin>", line 1, in <module> AttributeError: can't set attribute
```

### Encapsulation and private attributes

```python3
	class A(object):
		def __init__(self):
			self.__X = 3
	
		def __spam(self):
			pass
	
		def bar(self):
			self.__spam()
```

>Although this scheme provides the illusion of data hiding, there’s no strict mechanism in place to actually prevent access to the “private” attributes of a class. In particular, if the name of the class and corresponding private attribute are known, they can be accessed using the mangled name.A class can make these attributes less visible by redefining the __dir__() method, which supplies the list of names returned by the dir() function that’s used to inspect objects.

[Python Essential Reference - David Beazley](https://theswissbay.ch/pdf/Gentoomen%20Library/Programming/Python/Python%20Essential%20Reference%2C%20Fourth%20Edition%20%282009%29.pdf)

### Operator overloading

```python3
class Complex(object):
	def __init__(self,real,imag=0):
		self.real = float(real)
		self.imag = float(imag)
		
	def __repr__(self):
		return "Complex(%s,%s)" % (self.real, self.imag)
	
	def __str__(self):
		return "(%g+%gj)" % (self.real, self.imag) # self + other

	def __add__(self,other):
		return Complex(self.real + other.real, self.imag + other.imag)

	# self - other
	def __sub__(self,other):
		return Complex(self.real - other.real, self.imag - other.imag)
```

### Metaclasses

Here is an example of a metaclass that forces all methods to have a documentation string:

```python3
class DocMeta(type):
	def __init__(self,name,bases,dict):
		for key, value in dict.items():
		# Skip special and private methods
		if key.startswith("__"):
			continue
		# Skip anything not callable
		if not hasattr(value,"__call__"):
			continue # Check for a doc-string
		if not getattr(value,"__doc__"):
			raise TypeError("%s must have a docstring" % key) 			type.__init__(self,name,bases,dict)
```

```python3
class Documented:
	# In Python 3, use the syntax __metaclass__ = DocMeta # class Documented(metaclass=DocMeta)
```

#### Built-in `type` metaclass

The built-in metaclass in Python, which is `type`, is responsible for creating and defining classes. It is implicitly invoked to create the class object.

The type metaclass performs several important tasks:

- **Class Creation:** The `type` metaclass creates the class object itself. It takes three arguments: the name of the class, the bases (parent classes), and the class body (class namespace). 
- **Namespace Construction:** The `type` metaclass collects the attributes defined within the class body and constructs the namespace (dictionary) for the class. It gathers the methods, attributes, and other class members and organizes them within the class namespace.

- **Attribute Binding:** The type metaclass binds the attributes within the class namespace to the class object. This allows the class object to have access to its methods and attributes when instances of the class are created.

- **Inheritance Handling:** The type metaclass handles the inheritance hierarchy. It ensures that the appropriate method resolution order (MRO) is established based on the specified parent classes and their order of inheritance.

### Class decorators

A class decorator is a function that takes a class as input and returns a class as output. For example:

```python3
registry = { }
def register(cls):
	registry[cls.__clsid__] = cls
	return cls

@register
class Foo(object):
	pass
Foo.__cls_id__
```

## Misc

### Integer caching

```python
>>> a=256
>>> b=256
>>> a is b
True
>>> x=257
>>> y=257
>>> x is y
False
```

[3 facts of the integer caching - medium](https://medium.com/techtofreedom/3-facts-of-the-integer-caching-in-python-20ce587f09bb)
