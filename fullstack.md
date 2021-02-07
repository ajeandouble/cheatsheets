# Dev fullstack cheat-sheet

## Resources for fullstack development

**Track what stack and Saas solutions tech companies use:**
[Stackshare](https://stackshare.io/)

## Git

### Emulating git flow

[Without Git Flow](https://skoch.github.io/Git-Workflow/without-gitflow.html)

## Javascript

[Javascript The Core](http://dmitrysoshnikov.com/ecmascript/javascript-the-core/)

### Determining `this` (You don't know JS)

Now, we can summarize the rules for determining `this` from a function call's call-site, in their order of precedence. Ask these questions in this order, and stop when the first rule applies.

1. Is the function called with `new` (**new binding**)? If so, `this` is the newly constructed object.

    `var bar = new foo()`

2. Is the function called with `call` or `apply` (**explicit binding**), even hidden inside a `bind` *hard binding*? If so, `this` is the explicitly specified object.

    `var bar = foo.call( obj2 )`

3. Is the function called with a context (**implicit binding**), otherwise known as an owning or containing object? If so, `this` is *that* context object.

    `var bar = obj1.foo()`

4. Otherwise, default the `this` (**default binding**). If in `strict mode`, pick `undefined`, otherwise pick the `global` object.

    `var bar = foo()`

[You don't know javascript - This & object]()

### Arrow functions

>Does not have its own bindings to this or super, and should not be used as methods.
Does not have arguments, or new.target keywords.
Not suitable for call, apply and bind methods, which generally rely on establishing a scope.
Can not be used as constructors.
Can not use yield, within its body

[Arrow functions- MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

### Shallow copy vs deep copy

#### Shallow

```
const obj = {id: 42, val: {a: 'A', b: 'B'}}
const copiedObj = {...obj} // or use Object.assign({}, obj)
copiedObj.id = 43
console.log(obj.id) // id not affected
copiedObj.val.a = 'Z'
console.log(obj.val.a) // copiedObj.val and obj.val are pointing to the same object !
```

#### Deep copy
```JSON.parse(JSON.stringify(obj))```

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

>A class is technically a function, although the ECMAScript spec explicitly disallows calling a class without new . In fact, the typeof operator identifies MyClass as a function. To check whether an object is an instance of a class, you should use the instanceof operator.

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

```ECMAScript 2015 introduced a new set of keywords implementing classes. The new keywords include class, constructor, static, extends, and super.```<br>
[Inheritance and the prototype chain - With the class keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#with_the_class_keyword)
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
new B().print_value();
A.__proto__ === Function.prototype // true
B.__proto__ === A // true
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

#### Difference between Call and Apply

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

#### Thenables

>In JavaScript, a thenable is an object that has a then() function. All promises are thenables, but not all thenables are promises.
Many promise patterns, like chaining and async/await, work with any thenable. For example, you can use thenables in a promise chain:

```
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

[Thenables - MasteringJS](https://masteringjs.io/tutorials/fundamentals/thenable)
### Enumerables

### Map, Set, Array

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

### AJAX

>Asynchronous JavaScript and XML, while not a technology in itself, is a term coined in 2005 by Jesse James Garrett, that describes a "new" approach to using a number of existing technologies together, including HTML or XHTML, CSS, JavaScript, DOM, XML, XSLT, and most importantly the XMLHttpRequest object.

[Using XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)

## Nodejs

Nodejs is a runtime JS environment based on the V8 engine (google Chrome engine).
calling nodejs in a shell spawns nodejs **REPL** ( Read-Eval-Print-Loop ).
NodeJS use asynchronous I/O API (libuv) to make non-blocking I/O and sockets calls.

### Require()

Require loads the code of the module and wrap it in a function then executes the code using v8 vm.runInThisContext.

>Module.wrap = function(script) {
  return Module.wrapper[0] + script + Module.wrapper[1];
};
Module.wrapper = [
  '(function (exports, require, module, __filename, __dirname) { ',
  '\n});'
];
var wrapper = Module.wrap(content);
var compiledWrapper = vm.runInThisContext(wrapper, {
    filename: filename,
    lineOffset: 0,
    displayErrors: true
  });

[Require and the module system](http://fredkschott.com/post/2014/06/require-and-the-module-system)

### Event loop
Node is single-threaded. It works using an event loop and uses epoll for 
I/O operations to be non-blocking.
https://medium.com/preezma/node-js-event-loop-architecture-go-deeper-node-core-c96b4cec7aa4


NPM vs NPX

Resources:
https://hackernoon.com/19-things-i-learnt-reading-the-nodejs-docs-8a2dcc7f307f
https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop

### Express

>Middleware functions are functions that have access to the request object ( req ), the response object ( res ), and the next function in the application's request-response cycle. The next function is a function in the Express router which, when invoked, executes the middleware succeeding the current middleware.
Middleware is a function put in the midle who does work on teh request and pass 

### PassportJS

```
passport.serializeUser(function(user, done) {
    done(null, user.id);
});              │
                 │ 
                 │
                 └─────────────────┬──→ saved to session
                                   │    req.session.passport.user = {id: '..'}
                                   │
                                   ↓           
passport.deserializeUser(function(id, done) {
                   ┌───────────────┘
                   │
                   ↓ 
    User.findById(id, function(err, user) {
        done(err, user);
    });            └──────────────→ user object attaches to the request as req.user   
});
```
[Understanding passportJS Serialize/Deserialize - Stack Overflow](https://stackoverflow.com/questions/27637609/understanding-passport-serialize-deserialize)

## Browser

### CORS

>The server is responsible for reporting the allowed origins. The web browser is responsible for enforcing that requests are only sent from allowed domains.

[Stackoverflow: Cors, is it a client-side thing, a server-sde thing or a transport-level thing?](https://stackoverflow.com/questions/36958999/cors-is-it-a-client-side-thing-a-server-side-thing-or-a-transport-level-thin)

CORS is not security. The browser is responsive for setting the Origin Header. It avoids attacks such as click jacking.

>Browsers are in control of setting the Origin header, and users can't override this value. So you won't see the Origin header spoofed from a browser. A malicious user could craft a curl request that manually sets the Origin header, but this request would come from outside a browser, and may not have browser-specific info (such as cookies).
Remember: CORS is not security. Do not rely on CORS to secure your site. If you are serving protected data, use cookies or OAuth tokens or something other than the Origin header to secure that data. The Access-Control-Allow-Origin header in CORS only dictates which origins should be allowed to make cross-origin requests. Don't rely on it for anything more.

[What stop malicious code from spoofing the origin header to exploit CORS?](https://stackoverflow.com/questions/21058183/whats-to-stop-malicious-code-from-spoofing-the-origin-header-to-exploit-cors)

### Cookies


#### Session cookies are cookies set without an expiration date

>Not putting an expires part in will create a session cookie, whether it is created in JavaScript or on the server.

[Javascript cookie with no expiration date](https://stackoverflow.com/questions/532635/javascript-cookie-with-no-expiration-date/532660#532660)

## Databases

### MongoDB

>In terms of Node.js, mongodb is the native driver for interacting with a mongodb instance and mongoose is an Object modeling tool for MongoDB.
Mongoose is built on top of the MongoDB driver to provide programmers with a way to model their data.

[Difference between mongoDB and mongoose](https://stackoverflow.com/questions/28712248/difference-between-mongodb-and-mongoose#:~:text=In%20terms%20of%20Node.,way%20to%20model%20their%20data.)

## ReactJS

### Resources

[ReactJS - Blog](https://blog.logrocket.com/author/gladchinda/)
### Create-react-app

**create-react-app** add the following features without need to for further configuration to a a nodeJS project:

>React, JSX, ES6, and Flow syntax support.<br>
Language extras beyond ES6 like the object spread operator.<br>
Autoprefixed CSS, so you don’t need -webkit- or other prefixes.<br>
A fast interactive unit test runner with built-in support for coverage reporting.<br>
A live development server that warns about common mistakes.<br>
A build script to bundle JS, CSS, and images for production, with hashes and sourcemaps.<br>
An offline-first service worker and a web app manifest, meeting all the Progressive Web App criteria.<br>
Hassle-free updates for the above tools with a single dependency.

### React under the hood

[React Under The Hood](https://github.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/blob/master/fiber/book/Intro.md)

### React Fiber

[React Fiber](https://www.youtube.com/watch?v=GHPkhjOvBe0)

### Class components

#### 
### Hooks

[Hooks under the Hood](http                                                                   s://medium.com/the-guild/under-the-hood-of-reacts-hooks-system-eb59638c9dba)

[Usestate implementation](https://www.newline.co/@CarlMungazi/a-journey-through-the-usestate-hook--a4983397)

You can pass a function to the state setting function by useState instead of a value. So the value is not bound to whatever current value.

[How does React Hooks re-renders a functional component](https://medium.com/swlh/how-does-react-hooks-re-renders-a-function-component-cc9b531ae7f0#:~:text=already%20aware%20of%20%3A-,The%20render%20function%20accepts%20a%20Component%20and%20renders%20it.,the%20component%20automatically%20when%20invoked.)

#### Pseudo-implementation of useState()

```
let state = [];
let setters = [];
let firstRun = true;
let cursor = 0;

function createSetter(cursor) {
  return function setterWithCursor(newVal) {
    state[cursor] = newVal;
  };
}

// This is the pseudocode for the useState helper
export function useState(initVal) {
  if (firstRun) {
    state.push(initVal);
    setters.push(createSetter(cursor));
    firstRun = false;
  }

  const setter = setters[cursor];
  const value = state[cursor];

  cursor++;
  return [value, setter];
}

// Our component code that uses hooks
function RenderFunctionComponent() {
  const [firstName, setFirstName] = useState("Rudi"); // cursor: 0
  const [lastName, setLastName] = useState("Yardley"); // cursor: 1

  return (
    <div>
      <Button onClick={() => setFirstName("Richard")}>Richard</Button>
      <Button onClick={() => setFirstName("Fred")}>Fred</Button>
    </div>
  );
}

// This is sort of simulating Reacts rendering cycle
function MyComponent() {
  cursor = 0; // resetting the cursor
  return <RenderFunctionComponent />; // render
}

console.log(state); // Pre-render: []
MyComponent();
console.log(state); // First-render: ['Rudi', 'Yardley']
MyComponent();
console.log(state); // Subsequent-render: ['Rudi', 'Yardley']

// click the 'Fred' button

console.log(state); // After-click: ['Fred', 'Yardley']
```

[react hooks not magic just array](https://medium.com/@ryardley/react-hooks-not-magic-just-arrays-cd4f1857236e)

### Babel and Webpack

>The old versions of JavaScript had no import, include, or require, so many different approaches to this problem have been developed.
But since 2015 (ES6), JavaScript has had the ES6 modules standard to import modules in Node.js, which is also supported by most modern browsers.
For compatibility with older browsers, build tools like Webpack and Rollup and/or transpilation tools like Babel can be used.

**does react need webpack?**


[Usestate implementation](https://www.newline.co/@CarlMungazi/a-journey-through-the-usestate-hook--a4983397)

## Websockets

[Websockets and other Web APIs for real time requests](https://medium.com/platform-engineer/web-api-design-35df8167460)

**Websockets RFC**
[Websockets RFC](https://tools.ietf.org/html/rfc6455)

[Websockets for fun and profit](https://stackoverflow.blog/2019/12/18/websockets-for-fun-and-profit/)


### A simple websockets implementation

#### Server side
```
const WebSocket = require('ws');
const ws = new WebSocket.Server({ port: 8080 });

ws.on('connection', function connection(wsConnection) {
  wsConnection.on('message', function incoming(message) {
    console.log(`server received: ${message}`);
  });

  wsConnection.send('got your message!');
});

```

#### Client side
```
const socket = new WebSocket('ws://localhost:8080'); 
socket.addEventListener('open', function (event) { 
  socket.send('Hello Server!'); 
}); 

socket.addEventListener('message', function (event) { 
  console.log('Message from server ', event.data); 
});

socket.addEventListener('close', function (event) { 
  console.log('The connection has been closed'); 
});
```

## Databases

Relational: use 

ORM Object Relational Model
ODM Object Data Model






