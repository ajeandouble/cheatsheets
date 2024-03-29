# Javascript

## Resources

### Documentation and courses

[Javascript Tutorial](https://javascript.info/)

[You don't know JS](https://github.com/getify/You-Dont-Know-JS)

[Secrets of the Javascript Ninja](https://github.com/sakataa/Paper/blob/master/JS/Secrets%20of%20the%20JavaScript%20Ninja%2C%202nd%20Edition.pdf)

[Javascript The Core](http://dmitrysoshnikov.com/ecmascript/javascript-the-core/)

[Eloquent Javascript](https://eloquentjavascript.net/)

[Javascript testing best practices](https://github.com/goldbergyoni/javascript-testing-best-practices)

### Practice

[Top 10 tricky javascript questions - medium](https://andreassujono.medium.com/top-10-tricky-javascript-questions-often-asked-by-interviewers-45c7dd90495e)

[Hello Javascript (JS interview questions)](https://www.hellojavascript.info/)

[nodeschool.io](https://nodeschool.io/)

## Language Essentials

### `document` vs `window` vs `global`

- `document`: In web browsers and client-side JavaScript, the `document` object represents the HTML document loaded in the browser. It provides access to the elements, styles, events, and other features of the web page. It allows manipulation and interaction with the **DOM** (Document Object Model) of the web page.

- `window`: In the browser environment, the `window` object represents the global scope in the browser window or tab. It provides access to the document object and various other browser-related functionality such as managing the history and navigation.

- `global`: In the *Node.js* environment or other server-side JavaScript environments, the global object represents the global scope. It provides access to various built-in objects, functions, and modules available in the environment.

### Automatic Semicolon Insertion (ASI)

```js
function f1() {
  return
    {
      prop: 42
    };
}
function f2() {
  return {
    prop: 42
  };
}
console.log(f1(), f2()); // undefined { prop: 42 }
```


### Strict mode vs non-Strict mode

```js
"use strict";
```

- **Variable declaration:** All variables must be explicitly declared with `let`, `const` or `var` in strict mode.
- **Undeclared variable assignation:** like `variable = 42` will throw a `ReferenceError` in strict mode. In normal mode is equivalent to a global `var variable = 42`.
- **Duplicate parameter names:** in function declarations are not allowed and will throw a `SyntaxError` in strict mode.
- **Octal literals:** syntax using `0o` is forbidden in strict-mode
- `this` **keyword:** `this` is `undefined` in functions that are not *constructors* or *methods* in strict mode but will default to `window`.
- In strict mode, **Assignments to non-writable global variables** or non-writable properties throw a `TypeError`.
- **`eval` and arguments**: In strict mode, the eval() function and the arguments object have their own scope and do not leak variables into the surrounding scope.
- In non-strict mode, it’s actually possible to assign a value to the globally provided `undefined` identifier


### Types

#### Primitive types

- undefined
- null
- number
- string
- boolean
- symbol

#### Object types

- object
- array (subtype of object, specialized array)

Functions and arrays inherit from all the behaviour of an object. An array can be subscripted with a numerical value.

Functions can be executed. Functions are first-class objects, because they can be passed to other functions, returned from functions, and assigned to variables and properties.

#### Values vs References

Primitive types (aka *scalar types*) are always assigned/passed by values while object types (aka *compound values*) are passed/assigned by reference.

#### Value Wrappers

>These object wrappers serve a very important purpose. Primitive values don’t have properties or methods, so to access `.length` or `.toString()` you need an object wrapper around the value. Thankfully, JS will automatically box (aka wrap) the primitive value to fulfill such accesses:

[You don't know JS - Kyle Simpson](https://github.com/jumaschion/You-Dont-Know-JS-1/blob/master/types%20%26%20grammar/ch3.md#boxing-wrappers)


>In the process of coercion, when the `toString()` method is called on an object, the JavaScript engine needs to determine the appropriate string representation for that object. The object's internal [[Class]] is used for that purpose.

#### Built-in constructors

The `Number()`, `Function()`, `Boolean()`, and similar functions are called constructor functions or built-in constructors in JavaScript.

#### Coercion

```js
2+"2" // 22
[1,2] + [2, 1]; // '1,22,1'
+[]; // 0
{} + []; // 0 -> equivalent of +[] ({} is interpreted as empty block-scope
val = {} + [] // '[object Object]'

```
#### Symbols

>Symbol is a built-in object whose constructor returns a symbol primitive that's **guaranteed to be unique**. Symbols are often used to add unique property keys to an object that won't collide with keys any other code might add to the object, and which are hidden from any mechanisms other code will typically use to access the object. That enables a form of weak encapsulation, or a weak form of information hiding.

```js
Symbol.iterator // iteration protocols
Symbol.asyncIterator // async iteration protocols
Symbol.hasInstance // determines if a constructor object recognizes an object as its instance
// used by instance of

```
##### (some) `Symbol` methods

>Placing the `Symbol.hasInstance` symbol in the Symbol constructor, rather than directly in the `Object` constructor, is a convention established by the *ECMAScript* specification to indicate that it has broader applicability beyond just objects.


### Iteration protocols

>**Protocols** refer to a set of conventions or rules that an object can adhere to in order to enable the iteration behavior. These protocols define the expected behavior and interfaces that an object should implement to be considered iterable.

#### Iterable protocol

>In order to be **iterable**, an object must implement the `@@iterator` method, meaning that the object (or one of the objects up its prototype chain) must have a property with a `@@iterator` key which is available via constant `Symbol.iterator`:

>The iterable protocol allows JavaScript objects to define or customize their iteration behavior, such as what values are looped over in a `for`...`of` construct.

[MDN - Iteration protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)

#### The iterator protocol

>The iterator protocol defines a standard way to produce a sequence of values (either finite or infinite), and potentially a return value when all values have been generated. An object is an iterator when it implements a next() method with the following semantics


```js
{ done: something, value: somethingElse }
```
In practice, an object without either properti returned (by `next()` method) is equivalent to returning `{ done: false, value: undefined }`

```js
const obj = {};
obj[Symbol.iterator] = function () {
	let counter = 0;
	return {
		next: () => {
			if (counter++ < 100) return { value: Math.random(), done: false };
			else return { value: undefined, done: true };
		},
	};
};

obj.length = 30;
for (let item of obj) {
	console.log(item);
}

for (let i = 0; i < obj.length; ++i) {
	console.log(obj[i]); // undefined is printed 100x (only arrays are subscritable)
}
```

##### The async iterator and async iterable protocols

>There are another pair of protocols used for async iteration, named async iterator and async iterable protocols. They have very similar interfaces compared to the iterable and iterator protocols, except that each return value from the calls to the iterator methods is wrapped in a promise.

[MDN - Iteration Protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_async_iterator_and_async_iterable_protocols)

#### Generators

>**Generators** simplify the creation of iterable objects and make it easier to work with iteration protocols by providing a more intuitive and compact syntax. Under the hood, generators still adhere to the iteration protocols and generate iterator objects that can be used with the same iteration features as manually implemented iterable objects.

```js
function *createIterator(items) {
    for (let i = 0; i < items.length; i++) {
        yield items[i];
    }
}

const iterator = createIterator([0,1]);
console.log(iterator.next); // { value: 0, done: false }
console.log(iterator.next); // { value: 1, done: false }
console.log(iterator.next); // { value: undefined, done: true }
```

```js
const iterable = { "0": 1, "1": 2, "2": 3, [Symbol.iterator]: *function() {
	for (let i = 0; i < 3; ++i)
		yield this[i];
for (let item of iterable) { console.log(item) } // { value: 0, done: false } etc.
```

#### Iterables

>By implementing the iteration protocol, an object becomes iterable and can be easily integrated with JavaScript's built-in iteration mechanisms


### Hoisting

```js
var variable = 10;
(() => {
  variable2 = 100;
  console.log(variable); // 10
  console.log(variable2); // 100
  variable = 20;
  var variable2 = 50;
  console.log(variable); // 20
})();
console.log(variable); // 20
var variable = 30
console.log(variable2); // ReferenceError

f(); // 'f function'
function f() {
  console.log('f function')
}

var f2 = () => console.log(f());

```

`let` and `const`, `var` declarations are hoisted.
`var` is **automatically** defined as `undefined` during the hoisting process contrary to `let` and `const`.
Leaving them in the *Temporary Dead Zone*.

```js
console.log(doesntExist); // Uncaught ReferenceError: doesntExist is not defined
console.log(inTdz); // ReferenceError: Cannot access 'inTdz' before initialization
setTimeout(() => console.log(inTdz), 0); // 42
const inTdz = 42;

```

```js
	console.log(studentName);
	const studentName = "John"; // ReferenceError: Cannot access 'studentName' before initialization
	console.log(doesntExist) // ReferenceError: doesntExist is not defined
```

The **declaration** is **hoisted** but **not the value**.

A declaration of a variable without `var`, `let`, or `const` is forbidden in strict-mode. In normal mode it is equivalent to a global declaration with `var` (in any scope).

Functions are hoisted first then `var`, in order of declaration in their scope.


### Map, Set, WeakSet, WeakMap

#### `WeakMap` vs `Map`, `Set` vs `WeakSet`

```js
const m = new Map();
m.set("key", "value");
const m2 = new WeakMap();
m2.set({}, "value");
m2.set("key", "value"); // Uncaught TypeError: Invalid value used as weak map key
```

#### Map

>The Map object holds key-value pairs and remembers the original insertion order of the keys. Any value (both objects and primitive values) may be used as either a key or a value.

[Global objects - Map - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)

```
new Map() – creates the map.
map.set(key, value) – stores the value by the key.
map.get(key) – returns the value by the key, undefined if key doesn’t exist in map.
map.has(key) – returns true if the key exists, false otherwise.
map.delete(key) – removes the value by the key.
map.clear() – removes everything from the map.
map.size – returns the current element count.
```

#### Set

>The Set object lets you store **unique** values of any type, whether primitive values or object references.

[Using the Set Object - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set#using_the_set_object)

```
const s = new Set([1, 2, 3]);
s // Set(3) { 1, 2, 3 }
s.add(4) // Set(4) { 1, 2, 3, 4 }
s.add(1) // Set(4) { 1, 2, 3, 4 }
s.has(1) // true
s.delete(4) // true
s // Set(3) { 1, 2, 3 }
s.delete(4) // false
```




### Statement Completion Values

```js
> const a = 3;
undefined
> const b = 6;
undefined
>a * b;
18
> { 5 * 2; } 10
```
>In node **REPL** (Read-Eval-Print-Loop)

The completion value of a block is like an implicit return of the last statement value.



### Closures

```js
function greetName(name) {
	function sayHi() {
		console.log(`Hello ${name}`);
	}
	return sayHi;
}
const sayHiToJohn = greetName('John');
const sayHiToMary = greetName('Mary');
sayHiToJohn();	// Hello John
sayHiToMary();	// Hello Mary
```

Every function actually forms a **closure** as inner-scopes can reference outer-scopes variables. But closures are particularly noteworthy when a function is defined inside another function and is returned or passed as a value.

>Closure is actually a live link, preserving access to the full variable itself. We’re not limited to merely reading a value; the closed-over variable can be updated (re-assigned) as well! By closing over a variable in a function, we can keep using that variable (read and write) as long as that function refer- ence exists in the program, and from anywhere we want to invoke that function.

[You don't Know JS - Scope and Closures](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch7.md)

>Closure is observed when a function uses vari- able(s) from outer scope(s) even while running in a scope where those variable(s) wouldn’t be accessible.
>A closure must be:
>- Must be a function involved
>- Must reference at least one variable from an outer scope
>- Must be invoked in a different branch of the scope chain
from the variable(s)

[You don't Know JS - Scope and Closures](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch7.md)

Depending on the browser optimization the closure might conserve all variables in the outercope of

### Determining `this` (You don't know JS)

1. Is the function called with `new` (**new binding**)? If so, `this` is the newly constructed object.

    `var bar = new foo()`

2. Is the function called with `call` or `apply` (**explicit binding**), even hidden inside a `bind` *hard binding*? If so, `this` is the explicitly specified object.

    `var bar = foo.call( obj2 )`

3. Is the function called with a context (**implicit binding**), otherwise known as an owning or containing object? If so, `this` is *that* context object.

    `var bar = obj1.foo()`

4. Otherwise, default the `this` (**default binding**). If in `strict mode`, pick `undefined`, otherwise pick the `global` object.

    `var bar = foo()`

[You don't know javascript - This & object]()

[Understand JavaScript more deeply by writing a bind function - Medium](https://medium.com/@adambomb/understand-javascript-more-deeply-by-writing-a-bind-function-8b619b242dcc)


### Arrow functions

>Does not have its own bindings to this or super, and should not be used as methods.
Does not have arguments, or new.target keywords.
Not suitable for call, apply and bind methods, which generally rely on establishing a scope.
Can not be used as constructors.
Can not use yield, within its body

[Arrow functions- MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)


### Rest parameter

```
function f(a, b, ...rest) { console.log(a, b, rest) }
f(1, 2) // 1 2 []
f(1, 2, 3) // 1 2 [3]
f(1, 2, 3, '42') // 1 2 [3, '42]
```


### Destructuring

```js
myObj = { favoriteNumber: 42, firstName: 'John', isDeveloper: true };
my2ndObj = { firstName: 'Mary' };
const {
	favoriteNumber,
	isDeveloper: isDev, // renaming
	defaultTo = "doesn't exist", // default value if property doesn't exist
} = myObj;

console.log(favoriteNumber, isDev, defaultTo); // 42 true "doesn't exist"
```

### Object

#### Object properties

>There is an important difference between how the in operator and the hasOwnProperty(..) method behave. The in operator will check not only the target object specified, but if not found there, it will also consult the object’s [[Prototype]] chain (covered in the next chapter). By contrast, hasOwnProperty(..) only consults the target object.

[You don't know JS - Kyle Simpson](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/objects-classes/ch1.md)

```js
const obj = { prop: 42, ' trailing spaces prop name': [] };
'prop' in obj; // true
obj.hasOwnProperty('prop'); // true
Object.hasOwn(obj, 'prop'); // true
```

>Each property on an object is internally described by what’s known as a “property descriptor”. This is, itself, an object (aka, “metaobject”) with several properties (aka “attributes”) on it, dictating how the target property behaves.

```js
const myObj = { favoriteNumber: 42 };
Object.getOwnPropertyDescriptor(myObj,"favoriteNumber");
// {
// value: 42,
//     enumerable: true,
//     writable: true,
//     configurable: true
// }

Object.defineProperty(anotherObj,"anotherProp", { value: 42, enumerable: true });
Object.defineProperty(myObj, "favoriteNumber", { enumerable: false });
for (let item in myObj) { console.log(item); } // doesn't print anything, enumerable === false
```

[You don't know JS - Kyle Simpson](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/objects-classes/ch2.md)

#### Object attributes

- The `enumerable` attribute controls whether the property will appear in various enumerations of object properties, such as `Object.keys(..)`, `Object.entries(..)`, `for..in` loops
- The `writable` attribute controls wether a value assignment (via `=`) is allowed. It's handy to make a property read-only.
- The `configurable` attribute controls whether a property’s descriptor can be re-defined/overwritten. A property that’s `configurable: false` implies that any attempt to change its descriptor with `Object.defineProperty(..)` will fail.

#### Object characteristics

- **Extensible:** `Object.preventExtensions()` prevents any further addition of properties to an object. It cannot be reverted.

- **Sealed:** `Object.seal()`prevents the addition and deletion of properties, but allows the modification of existing properties. Existing properties can still be changed, their values can be reassigned, and their attributes (such as configurable and writable) can be modified.

- **Frozen:** `Object.freeze()` prevents any change to its properties (read-only). Their attributes cannot be modified.

`Object.seal()` and `Object.freeze()` operate on the first level of an object (not on nested objects).

[Why would I need to freeze an object in Javascript](https://stackoverflow.com/questions/14791302/why-would-i-need-to-freeze-an-object-in-javascript)

#### Shallow copy vs deep copy

##### Shallow

```
const obj = {id: 42, val: {a: 'A', b: 'B'}}
const copiedObj = {...obj} // or use Object.assign({}, obj)
copiedObj.id = 43
console.log(obj.id) // id not affected
copiedObj.val.a = 'Z'
console.log(obj.val.a) // copiedObj.val and obj.val are pointing to the same object !
```

##### Deep copy

```js
JSON.parse(JSON.stringify(obj))
Object.assign({}, obj);
```


### Prototype chain

>The `[[Prototype]]` is an internal linkage that an object gets by default when its created, pointing to another object.
>The strange looking `__proto__` property has been in some JS engines for more than 20 years, but was only standardized in JS as of ES6 (in 2015).

```js
const obj = { val: 42 }
obj.__proto__ == Object.prototype
```

>The instanceof operator doesn’t just look at the current object, but rather traverses the entire class inheritance hierarchy (the `[[Prototype]]` chain) until it finds a match. Thus, anotherPoint is an instance of both Point3d and Point2d.


### Objet oriented programming

[OO relationships](https://dmitrysoshnikov.medium.com/oo-relationships-5020163ab162)<br>
[OOP general theory](http://dmitrysoshnikov.com/ecmascript/chapter-7-1-oop-general-theory/)

### Methods

>Every time you access a property on an object, that is a property access, regardless of the type of value you get back. If you happen to get a function from that property access, it's not magically a "method" at that point.

[Property vs.Method](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/this%20%26%20object%20prototypes/ch3.md)

```
function F() {
	this.method = function method() { return 'method??' }
}
F.static_method = function static_method() { return 'static_method??' }

// is equivalent to:
class G {
	constructor() {
		this.method = function method() { return 'method??' }
	}
	static static_method() {
		return 'static_method??'
	}
}

console.log(new F().method, new F().method())
// [Function: method] method??
console.log(F.static_method, F.static_method())
// [Function: static_method] static_method??
console.log(new G().method, new G().method())
[Function: method] method??
console.log(G.static_method, G.static_method())
// [Function: static_method] static_method??

```

### Classes and the new operator

>A class is technically a function, although the ECMAScript spec explicitly disallows calling a class without new. In fact, the typeof operator identifies MyClass as a function. To check whether an object is an instance of a class, you should use the instanceof operator.

[An overview of ES6 classes](https://thecodebarbarian.com/an-overview-of-es6-classes#:~:text=A%20class%20is%20technically%20a,identifies%20MyClass%20as%20a%20function.&text=To%20check%20whether%20an%20object,should%20use%20the%20instanceof%20operator.)

> **>** class F {}<br>
> **>** F()<br>
> **Uncaught TypeError: Class constructor F cannot be invoked without 'new'**

**JavaScript doesn't have real classes. It uses the world class as syntaxic sugar for a class design pattern**

>Since classes are a design pattern, you can, with quite a bit of effort (as we'll see throughout the rest of this chapter), implement approximations for much of classical class functionality. JS tries to satisfy the extremely pervasive desire to design with classes by providing seemingly class-like syntax.

```
class C {
	constructor() {
		this.a = 42
	}
	method() { console.log('method') }
	static static_method() { console.log('static_method') }
}
const Cobj = new C()

// equivalent of
function F() {
	this.a = 42;
}
F.static_method = function static_method() { console.log('static_method') }
F.prototype.method = function method() { console.log('method') }

const Fobj = Object.create(F.prototype)
F.call(Fobj)
```

```
class Point {
  a = 22 // Declare class property
}
// is just syntactic sugar to provide a shortcut for this code:

class Point {
  constructor() {
    this.a = 22;
  }
}
```

#### This

```
class Example {
    constructor() {
      const proto = Object.getPrototypeOf(this);
      console.log(Object.getOwnPropertyNames(proto));
    }
    first(){}
    second(){}
    static third(){}
}

 new Example(); // ['constructor', 'first', 'second']
```
[Getting class property outside method](https://stackoverflow.com/questions/38269083/declare-a-class-property-outside-of-a-class-method)

[Property vs.Method](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/)


There are no such thing as methods. There are properties which happen to be functions.

### Prototype

Every object as an internal property **[[prototype]]**. **\__proto\__** is a non-standard accessor (`object.__proto__ = value` has no effect).
<br>If you want to modify the **[[prototype]]** property you have to use the `Object.setPrototypeOf(object, prototype)` method. You can create an object with a **\_\_proto\_\_** property defined with **Object.create()** or **new** or you can override [[proto]] by doing const instance = { \_\_proto\_\_: something }


```
const obj = {}
obj.__proto__ === Object.prototype // true
const array = []
array.__proto__ === Array.prototype // true
array.__proto__.__proto__ === Object.prototype // true
function f() { }
f.__proto__ === Function.prototype // true
Function.__proto__ === Object.prototype // true
class C {}
C.__proto__ === Object.__proto__ // true

```

#### Prototype inheritance

>ECMAScript 2015 introduced a new set of keywords implementing classes. The new keywords include class, constructor, static, extends, and super.```

[Inheritance and the prototype chain - With the class keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#with_the_class_keyword)
[Benefits of prototypal inheritance over classical - Stackoverflow](https://stackoverflow.com/questions/2800964/benefits-of-prototypal-inheritance-over-classical)

```
class A {
	constructor() {	this.something = 42; }
	static s() { console.log('static') }
	a() { console.log('A') }
}
class B extends A {
	constructor() {	super() }
	b() { console.log('B'); }
	print_value() { console.log(this.something); }
}
new B().a(); // 'A'
new B().b(); // 'B'
new B().print_value(); // 42
A.s();
B.s();
A.__proto__ === Function.prototype // true
B.__proto__ === A.prototype // true
B.prototype.__proto__ === A.prototype // true
new B().__proto__ === A.prototype // true
```

**is equivalent to:**
```
function A() { this.something = 42; }
A.prototype.a = function a() { console.log('A') }
A.s = function s() { console.log('static') }
function B() { A.call(this) }
B.prototype.b = function b() { console.log('B') }
B.prototype.print_value = function print_value() { console.log(this.something) }
Object.setPrototypeOf(B, A); // lookup in B then A when trying to access one of the function object property (static properties and methods)
Object.setPrototypeOf(B.prototype, A.prototype); // lookup in B.prototype then A.prototype when trying to access an instancied object property
const obj = {}
B.call(obj)
Object.setPrototypeOf(obj, B.prototype);
obj.a(); // 'A'
obj.b(); // 'B'
obj.print_value();
```

See [Inheritance and the prototype chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#summary_of_methods_for_extending_the_prototype_chain

>The instanceof operator tests to see if the prototype property of a constructor appears anywhere in the prototype chain of an object. The return value is a boolean value.

[instanceof - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof)

```
function Manager() {
  Employee.call(this);
  this.reports = [];
}
Manager.prototype = Object.create(Employee.prototype);
Manager.prototype.constructor = Manager;

function WorkerBee() {
  Employee.call(this);
  this.projects = [];
}
WorkerBee.prototype = Object.create(Employee.prototype);
WorkerBee.prototype.constructor = WorkerBee;
```

### Setters and  getters

```
const obj = {
	v: undefined,
	set setV(value) { this.v = value },
	get getV() { return this.v }
}
obj // { v: undefined, setV: [Setter], getV: [Getter] }
obj.setV = 42
obj.getV // 42
obj // { v: 42, setV: [Setter], getV: [Getter] }
```

#### Defining a getter or setter on existing object

```
Object.defineProperty(obj, 'setV', { set: function(x) { this.v = x / 2; }});
Object.defineProperty(obj, 'getV', { get: function() { return this.v + 1; } });
```

### Difference between Call and Apply

```Note: While the syntax of this function is almost identical to that of call(), the fundamental difference is that call() accepts an argument list, while apply() accepts a single array of arguments.```

### Object.assign()

>The Object.assign() method copies all enumerable own properties from one or more source objects to a target object. It returns the target object.
```
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };
Object.assign(target, source);
console.log(target); // expected output: Object { a: 1, b: 4, c: 5 }
```
[Object.assign() - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

### Mixins

>Mixin – is a generic object-oriented programming term: a class that contains methods for other classes.<br>
Some other languages allow multiple inheritance. JavaScript does not support multiple inheritance, but mixins can be implemented by copying methods into prototype.

[Javascript.info - mixins](https://javascript.info/mixins)

### Promises

```Promise.resolve(obj) === obj // Testing if obj is a promise according to Ecma specs```

[How do I tell if an object is a promise?](https://stackoverflow.com/questions/27746304/how-do-i-tell-if-an-object-is-a-promise)

#### Thenables

>In JavaScript, a thenable is an object that has a `then()` function. All promises are thenables, but not all thenables are promises.
Many promise patterns, like chaining and async/await, work with any thenable. For example, you can use thenables in a promise chain:

```js
const thenable = {
  then: function(onFulfilled) {
    setTimeout(() => onFulfilled(42), 10);
  }
};

Promise.resolve().
  then(() => thenable).
  then(v => {
    v; // 42
  });
```

#### Promise implementation

[Thenables - MasteringJS](https://masteringjs.io/tutorials/fundamentals/thenable)

[Promise implementation - codepen](https://codepen.io/mayank_shubham/pen/abpEVJK?editors=0011)

### Error

>In JavaScript, you can throw any value as an exception, not just instances of the `Error` class. However, using the Error class or its subclasses provides several advantages:

It's advised to throw instance of `Error` or derived class errors. The advantages are :

- **Standardization**: Using `Error` or its subclasses helps follow established conventions and promotes code readability and consistency.
- **Stack trace**: When an error occurs and is thrown as an Error object, it captures the current stack trace. (In browsers, the `Error` object provides a stack property that contains the stack trace information. You can access it using errorObject.stack.)

#### Custom `Error` subclasses

```js
class CustomError extends Error {
	constructor(msg) {
		super(msg);
		this.name = 'CustomError';
	}
}
throw new CustomError('Custom message'); // Uncaught CustomError: Custom message
```

### Mutable/Immutable

#### split vs splice, concat etc.


### Event loop

[What the heck is the event loop ayway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

>The Event Loop in the Browser or Node is not part of V8. The Event Loop Is Part of a different application/dependency/library which is provided by the Browser or Node.

In *Chrome* uses [libevent](https://github.com/libevent/libevent) while *Node.js* uses [libuv](https://github.com/libuv/libuv)

[Microtask vs macrotasks](https://stackoverflow.com/questions/25915634/difference-between-microtask-and-macrotask-within-an-event-loop-context)

>However, certain tasks in Node.js that involve I/O operations or other blocking operations are offloaded to worker threads managed by the libuv library. These worker threads, also known as "thread pool," provide a multi-threaded environment for executing certain operations in parallel, such as file system operations, network I/O, and some cryptographic operations.

https://medium.com/preezma/node-js-event-loop-architecture-go-deeper-node-core-c96b4cec7aa4

#### Macro vs Micro tasks

- **Macrotasks:** include keyboard/mouse events, timer events (setTimeout etc.), network events, Html parsing, changing Url etc.
- **Microtasks:** include Promises, Object.observe, MutationObserver, process.nextTick etc.

#### Tasks execution

>The Event Loop is a continuous loop that checks if the call stack is empty. If it is, it takes the first task from the task queue (also known as the event queue or the callback queue) and pushes it onto the call stack, which immediately executes it.

[Sleep - Leetcode](https://leetcode.com/problems/sleep/editorial/)

The call stack executes. Then after all functions are executed, the event loop will execute at most one macrotask.
All the microtasks are executed during the event loop iteration.

>The act of adding tasks to their matching queues happens outside the event loop. The acts of detecting and adding tasks are done separately from the event loop.

>Both types of tasks are executed one at a time. When a task starts executing, it’s executed to its completion. Only the browser can stop the execution of a task (e.g. too resource intensive)

>All microtasks should be executed before the next rendering because their goal is to update the application state before rendering occurs.

[Diferrence between microtask and macrotask - Stack Overflow](https://stackoverflow.com/a/74700864/12692151)


### Reflect API


### Proxy


### DOM

### Misc

#### Local variable name `undefined`

>In both non-strict mode and strict mode, however, you can create a local variable of the name `undefined`. But again, this is a terrible idea!

[You don't know JS - Kyle Simpson](https://github.com/jumaschion/You-Dont-Know-JS-1/blob/master/types%20%26%20grammar/ch2.md)

```js
    function foo() {
        "use strict";
        var undefined = 2;
        console.log( undefined ); // 2
    }

```

#### `void` operator

```js
void 42; // undefined
```

#### Nullish coalescing operator `??`

>The nullish coalescing (`??`) operator is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand.

[Nullish Coalescing Operator - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing)

#### Numbers

```js
const nan = "hello" / 5;
Object.is(nan, NaN); // true
Object.is(0 * 5, -0); // false
```
#### Labels

```js
var counter = 0;
label: 	while (true) {
	console.log('first while');
		if (counter)
			break ;
		counter++;
		while (true) {
			continue label;
		}
	}

```

A label can apply to a nonloop block, but only break can reference such a nonloop label.

```js
label: { break label; console.log('never run!') }
```

#### Temporary Dead Zone and `typeof`

>Interestingly, while typeof has an exception to be safe for unde‐ clared variables, no such safety exception is made for TDZ references
>
{
	typeof a; // undefined
	typeof b; // Uncaught ReferenceError: Cannot access 'uuu' before initialization (TDZ)1=
	let b;
}

#### `try`...`finally`

```js
function foo() {
	try {
		return 42;
	} finally {
		console.log('Hello');
	}
	console.log(foo());
	// Hello
	// 42
}
```

#### Global DOM Variables

```js
// <div id="foo></div>
if (typeof foo === "undefined) { console.log('never runs'); }
```

#### `arguments` object

The arguments object has some array-like characteristics but lacks many array methods and properties. It is not an instance of `Array` and thus doesn't inherit its methods. It also is immutable


## Functional Programming

[Functional Programming in JS - Medium](https://dev.to/mpodlasin/functional-programming-in-js-part-i-composition-currying-lodash-and-ramda-1ohb)

### Concepts

#### Pure functions

```js
function pure (x){
  return x + 2
}

var a;
function impure(x) {
	a = x + 2;
}
```

#### Immutability

Functional programming promotes the use of immutable data, where data structures cannot be modified after they are created. Instead of modifying data, functional programs create new data structures that reflect the desired changes. Immutability helps with reasoning about code, preventing unexpected mutations, and enabling efficient concurrency.

#### First-Class and High-Order functions

```js
const multiply = (a, b) => a * b;

function applyOperation(a, b, operation) {
  return operation(a, b);
}

const result = applyOperation(3, 4, multiply);
```

#### Function composition

```js
function addOne(num) {
  return num + 1;
}

function double(num) {
  return num * 2;
}

const composedFunction = (num) => double(addOne(num));

const result = composedFunction(5);
```



## DOM and Browser

### Walking the DOM

- `<html>` → `document.documentElement`
- `<head>` → `document.head`
- `<body>` → `doucment.body`

- **Children nodes** → `.childNodes`, `firstChild` and `lastChild`
- **Parent node** → `.parentNode` and `parentElement`
- **Sibling nodes** → `nextSibling` and `previousSibling` 

```js
console.log( document.documentElement.parentNode ); // document
console.log( document.documentElement.parentElement ); // null
```


### Searching and modifying element and their attributes

#### Searching

- `document.getElementById(id)`. There is also a global variable `id` automatically created (it is bad practice to access an element this way)
- `elem.querySelectorAll(css)` returns all elements inside elem matching the given CSS selector
- `elem.querySelector(css)` returns the same result as `elem.querySelectorAll(css)[0]`.
- `elem.matches(css)` checks if the element match the selector
- `elem.getElementsByTagName(tag)`, `elem.getElementsByClassName(className)`, `document.getElementsByName(name)`

>All methods `getElementsBy*` return a live collection. Such collections always reflect the current state of the document and “auto-update” when it changes.
>In contrast, `querySelectorAll` returns a static collection. It’s like a fixed array of elements.

[Searching elements - javascript.info](https://javascript.info/searching-elements-dom#live-collections)

#### Modifying the document

`document.createElement(tag)`, `elem.cloneNode(deep)`, `node.append(...nodes or strings)` etc.

#### Attributes

- `elem.hasAttribute(name)` → to check for existence.
- `elem.getAttribute(name)`
- `elem.setAttribute(name, value)`
- `elem.removeAttribute(name)`
- `elem.attributes` → a collection of all attributes.


### DOM events

- **HTML attribute:** `onclick="..."`
- **DOM property:** `elem.onclick = function(...)`
- **Methods:** `elem.addEventListener(event, handler[, phase])`, `removeEventListener`

### Other

>The DOMContentLoaded event triggers on document when the DOM is ready. We can apply JavaScript to elements at this stage.


## Misc


### Websockets

>WebSockets don’t have cross-origin limitations. They are well-supported in browsers. They can send/receive strings and binary data.

### `async` and `defer` `<script>` attributes

>The `defer` attribute tells the browser not to wait for the script. Instead, the browser will continue to process the HTML, build DOM. The script loads “in the background”, and then runs when the DOM is fully built.

>The async attribute is somewhat like defer. It also makes the script non-blocking. But it has important differences in the behavior.

The async attribute means that a script is completely independent:

[script async defer -  javascript.info](https://javascript.info/script-async-defer)

### Mysterious questions

Are array-like objects just iterables?
```js
const foo = {n:1}
foo = {n:2};
foo.x = foo;

console.log(foo); // {n: 2, x: [Circular *1]}
```
*vs*

```js
const foo = {n:1}
foo.x = foo = {n:2}
```
*while in js assignments are evaluted from right -> left?*

>forEach function is always synchronous, no matter if each loop is synchronous or asynchronous. This means that each loop will not wait for the other. If you want to execute each loop in sequence and wait for each other, use for of instead.

//Q16
if(function f(){}){ console.log(f) }
//error: ReferenceError: f is not defined


const obj1 = { }
const obj2 = { }
const obj3 = { }

obj1[obj2] = 'test'
obj1[obj3] = 'whatever'
console.log(obj2 != obj3) // true
console.log(obj1) // { [object Object]: 'whatever'} -> ??????


WEB APIs?
