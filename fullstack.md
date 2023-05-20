# Dev fullstack cheat-sheet


## Resources

[Stackshare](https://stackshare.io/)

[Stackblitz](https://stackblitz.com/)


## Deployment

### Git

[How does git store files? - Stack Overflow](https://stackoverflow.com/questions/8198105/how-does-git-store-files#:~:text=Git%20doesn't%20think%20of,a%20reference%20to%20that%20snapshot.)
[Git objects - Git Objects](https://book.git-scm.com/book/en/v2/Git-Internals-Git-Objects)

#### Emulating Git Flow
[Without Git Flow](https://skoch.github.io/Git-Workflow/without-gitflow.html)

NPM vs NPX

Resources:
https://hackernoon.com/19-things-i-learnt-reading-the-nodejs-docs-8a2dcc7f307f
https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop

### Express

>Middleware functions are functions that have access to the request object ( req ), the response object ( res ), and the next function in the application's request-response cycle. The next function is a function in the Express router which, when invoked, executes the middleware succeeding the current middleware.
Middleware is a function put in the midle who does work on teh request and pass

#### Reading request data

[Differences between req.params, req.query and req.body](https://dev.to/gathoni/express-req-params-req-query-and-req-body-4lpc)

#### Passing data to the next middleware


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



### Same-Origin policy

>Two URLs have the same origin if the protocol, port (if specified), and host are the same for both.

>Scripts executed from pages with an about:blank or javascript: URL inherit the origin of the document containing that URL, since these types of URLs do not contain information about an origin server.

>A page may change its own origin, with some limitations. A script can set the value of document.domain to its current domain or a superdomain of its current domain. If set to a superdomain of the current domain, the shorter superdomain is used for same-origin checks.

[Same Origin Policy - MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)


#### Allowed cross origins access list

- Javascript with <script src="..."></script>
- CSS applied with <link rel="stylesheet" href="..."> (with correct content-type header for the css file)
- Images displayed with <img>
- Media played by <video> and <audio>


### CORS

>Use **CORS** to allow cross-origin access. CORS is a part of HTTP that lets servers specify any other hosts from which a browser should permit loading of content.

[Same-Origin Policy - MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)

**CORS** is not a security measure but a way to allow cross-origin accesses.

>The server is responsible for reporting the allowed origins. The web browser is responsible for enforcing that requests are only sent from allowed domains.

[Stackoverflow: Cors, is it a client-side thing, a server-sde thing or a transport-level thing?](https://stackoverflow.com/questions/36958999/cors-is-it-a-client-side-thing-a-server-side-thing-or-a-transport-level-thin)

***CORS is not security***. The browser is responsible for setting the Origin Header. It avoids attacks such as click jacking.

>Browsers are in control of setting the Origin header, and users can't override this value. So you won't see the Origin header spoofed from a browser. A malicious user could craft a curl request that manually sets the Origin header, but this request would come from outside a browser, and may not have browser-specific info (such as cookies).

[What stop malicious code from spoofing the origin header to exploit CORS?](https://stackoverflow.com/questions/21058183/whats-to-stop-malicious-code-from-spoofing-the-origin-header-to-exploit-cors)


### Cookies

[Difference between session storage, local storage and session cookies](https://stackoverflow.com/questions/19867599/what-is-the-difference-between-localstorage-sessionstorage-session-and-cookies)


#### Session cookies are cookies set without an expiration date

>Not putting an expires part in will create a session cookie, whether it is created in JavaScript or on the server.

[Javascript cookie with no expiration date](https://stackoverflow.com/questions/532635/javascript-cookie-with-no-expiration-date/532660#532660)


#### Third party cookie

[Chrome's Changes Could Break Your App - Chrome's Changes Could Break Your App: Prepare for SameSite Cookie Updates](https://blog.heroku.com/chrome-changes-samesite-cookie)


### Local Storage

[Is it safe to store a JWT inside local storage? - Stack Overflow](https://stackoverflow.com/questions/44133536/is-it-safe-to-store-a-jwt-in-localstorage-with-reactjs)


#### Heroku

>herokuapp.app is listed in Public suffix List which means cookies are blocked from bein set to the domain "herokuapp.com"

[How to set a domain Cookie with Heroku](https://stackoverflow.com/questions/57747704/how-to-set-a-same-domain-cookie-with-heroku-subdomains?rq=1)

https://en.wikipedia.org/wiki/Public_Suffix_List


## Databases


#### SQL


#### SQL Joins


### MongoDB

>In terms of Node.js, mongodb is the native driver for interacting with a mongodb instance and mongoose is an Object modeling tool for MongoDB.
Mongoose is built on top of the MongoDB driver to provide programmers with a way to model their data.

[Difference between mongoDB and mongoose](https://stackoverflow.com/questions/28712248/difference-between-mongodb-and-mongoose#:~:text=In%20terms%20of%20Node.,way%20to%20model%20their%20data.)


### Misc

For loop weirdness - See google devs vids


## ReactJS

[React Under The Hood](https://github.com/Bogdan-Lyashenko/Under-the-hood-ReactJS/blob/master/fiber/book/Intro.md)

[ReactJS - Blog](https://blog.logrocket.com/author/gladchinda/)

[Read React source code](https://github.com/numbbbbb/read-react-source-code/blob/master/02-how-render-works.md)

[React - Storybooks](https://storybook.js.org)


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


### JSX

[JSX in depth - ReactJS tutorial](https://reactjs.org/docs/jsx-in-depth.html)


#### How an element is created

```
createElement()
React.createElement(
  type,
  [props],
  [...children]
)
```

#### Examples of Js to JSX conversion by Babel

**Nested components**
```
<>
<MyButton color="blue" >
  Click Me
</MyButton>
  <p>Test<b>bold</b></p>
</>
```
*becomes:*
```
"use strict";

/*#__PURE__*/
React.createElement(React.Fragment, null, /*#__PURE__*/React.createElement(MyButton, {
  color: "blue"
}, "Click Me"), /*#__PURE__*/React.createElement("p", null, "Test", /*#__PURE__*/React.createElement("b", null, "bold")));
```
[Babel online compiler](https://babeljs.io/)

**Handlers**
```
var mouseOverHandler = function mouseOverHandler() {
    console.log('you moused over');
  };
var clickhandler = function clickhandler() {
    console.log('you clicked');
  };
var reactNode = React.createElement(
    'div',
    { onClick: clickhandler, onMouseOver: mouseOverHandler },
    'click or mouse over'
  );

ReactDOM.render(reactNode, document.getElementById('app'));
```
[JSX - Understanding in the context of ReactJS](https://rohan-paul.github.io/javascript/2017/08/13/JSX_Understanding_In_The_Context_Of_Reactjs/#:~:text=So%2C%20if%20JavaScript%20files%20contains,representation%20of%20a%20DOM%20node.)


### React Fiber

[React Fiber](https://www.youtube.com/watch?v=GHPkhjOvBe0)

### Context

[Context](https://reactjs.org/docs/context.html)

### Class components

[How does React tell a Class from a Function - Overracted](https://overreacted.io/how-does-react-tell-a-class-from-a-function/#:~:text=If%20your%20component%20is%20defined,use%20new%20when%20calling%20it.)

#### Binding this

>In an event, this refers to the element that received the event.

So you have to bind this like so:


```
constructor(props) {
	super(props);
	this.handleClick = this.handleClick.bind(this);
}

handleClick() {	this.setState(state => ({isToggleOn: !state.isToggleOn })); }
```

or use arrow function so this get lexically bound:

### React Lifecycle

**Mounting**:
1. **constructor()**
2. static getDerivedStateFromProps()
>This method exists for rare use cases where the state depends on changes in props over time. For example, it might be handy for implementing a <Transition> component that compares its previous and next children to decide which of them to animate in and out.
3. **render()**
4. **componentDidMount()**
>componentDidMount() is invoked immediately after a component is mounted (inserted into the tree). Initialization that requires DOM nodes should go here. If you need to load data from a remote endpoint, this is a good place to instantiate the network request.

**Updating** (changes in props or state):
1. static getDerivedStateFromProps()
2. shouldComponentUpdate()
3. **render()**
4. getSnapshotBeforeUpdate()
5. **componentDidUpdate()**

#### Custom event listeners

[Add custom event listener to component - Stack Overflow](https://stackoverflow.com/questions/36180414/reactjs-add-custom-event-listener-to-component)

[Why should I remove event listeners](https://stackoverflow.com/questions/53256662/react-why-should-i-remove-event-listeners#:~:text=The%20event%20listeners%20need%20to,which%20will%20create%20memory%20leaks.)

### Hooks

[Hooks under the Hood](http                                                                   s://medium.com/the-guild/under-the-hood-of-reacts-hooks-system-eb59638c9dba)

[Usestate implementation](https://www.newline.co/@CarlMungazi/a-journey-through-the-usestate-hook--a4983397)

You can pass a function to the state setting function by useState instead of a value. So the value is not bound to whatever current value.

[How does React Hooks re-renders a functional component](https://medium.com/swlh/how-does-react-hooks-re-renders-a-function-component-cc9b531ae7f0#:~:text=already%20aware%20of%20%3A-,The%20render%20function%20accepts%20a%20Component%20and%20renders%20it.,the%20component%20automatically%20when%20invoked.)


#### How setters trigger re-render

**Setters** and **useEfect** use **Object.is** algorithm to check for updated value.

```
function Component() {
	const [clicked, setClicked] = useState({value: false});
	return (
		<><button onClick={() => { clicked.value = true; value.setClicked(clicked); }}>Click me!</button></>
	)
} // Clicking on the button won't trigger a re-render due to Object comparaison being true

// onClick={ () => { const newClicked = Object.assign({}, clicked); newClicked.value = true; setClicked(newClicked); } }
// => will trigger a re-render
//  onClick={ () => setClicked(prev => whatever_new_state) }
// => will trigger a re-render
```

>A function which is being used to compare objects is practically a polyfill of Object.is method.

[What comparaison process does the react useEffect hook use](https://stackoverflow.com/questions/55089560/what-comparison-process-does-the-useeffect-react-hook-use)

[The React UseRef Hook explained with examples](https://medium.com/javascript-in-plain-english/the-react-useref-hook-explained-with-examples-3bc759c0b105)

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


#### UseRef

>The hook useRef allows you to access DOM elements directly, and persist data between renders without causing a component to re-render infinitely when changes.

```
const Reference = ()=> {
  const [name, setName] = useState('Mehdi')
  const previousName = useRef(null)

  useEffect(() => {
    previousName.current = name;
  }, [name])

  return (
    <>
      <input value={name} onChange={e => setName(e.target.value)} />
      <div>{previousName.current} => {name}</div>
    </>
  )
}
```

### Context


>Unpopular opinion: All that junk you're putting in React context should just be props. Legit uses for context are rare, and mostly for library code, not your app.

[Mjackson - Twitter](https://twitter.com/mjackson/status/1195431511417208834)

```
const things = useContext(ThingsContext)
```

[Using React Context with functional components](https://medium.com/@danfyfe/using-react-context-with-functional-components-153cbd9ba214)

### Prop drilling and composition

We can avoid using **React.Context** by using composition.

[Thinking in React component composition](https://dev.to/bouhm/thinking-in-react-component-composition-fp5)

### React-Redux

[Understanding how reducers are used in redux - CSS-Tricks](https://css-tricks.com/understanding-how-reducers-are-used-in-redux/#:~:text=A%20reducer%20is%20a%20function,receives%20to%20determine%20this%20change.&text=Redux%20relies%20heavily%20on%20reducer,reducers%20is%20in%20this%20post.)

### React-router-dom

[Understanding the fundamentals of React Router](https://medium.com/the-andela-way/understanding-the-fundamentals-of-routing-in-react-b29f806b157e)

#### Private route

```
export const PrivateRoute = ({component: Component, ...rest}) => {
	return (
 		<Route {...rest} render={props => (
		    isLoading() ?
		    <Loading /> :
		        isAuth ?
		            <Component {...props} />
		        : <Redirect to="/" />
       	 	     )} />
		);
}
```

### Lazy loading

```
const SomeComponent = React.lazy(() => import('./SomeComponent'));
```

>React.lazy() lets you define a component that is loaded dynamically. This helps reduce the bundle size to delay loading components that aren’t used during the initial render.

```
const OtherComponent = React.lazy(() => import('./OtherComponent'));
function MyComponent() {
  return (
    // Displays <Spinner> until OtherComponent loads
    <React.Suspense fallback={<Spinner />}>
      <div>
        <OtherComponent />
      </div>
    </React.Suspense>
  );
}
```
>Rendering lazy components requires that there’s a <React.Suspense> component higher in the rendering tree. This is how you specify a loading indicator.

[Lazy - React docs](https://reactjs.org/docs/react-api.html#reactlazy)


### Composition in React

>
[Using composition to avoid 'props drilling' - Youtube](https://www.youtube.com/watch?v=3XaXKiXtNjw)

[Composition vs Inheritance - React docs](https://reactjs.org/docs/composition-vs-inheritance.html)

### Babel and Webpack

>The old versions of JavaScript had no import, include, or require, so many different approaches to this problem have been developed.
But since 2015 (ES6), JavaScript has had the ES6 modules standard to import modules in Node.js, which is also supported by most modern browsers.
For compatibility with older browsers, build tools like Webpack and Rollup and/or transpilation tools like Babel can be used.

**does react need webpack?**

[Building a simplified Webpack clone](https://lihautan.com/building-a-simplified-webpack-clone/)

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
## Regex

[Training puzzles](https://www.hackerrank.com/domains/regex)

### Basic Regex
```
var regex = /hello/
regex.test('a') // false
regex.test('helloW') // true
regex = new RegExp('hello', 'i') // equivalent with case-insensitive test
regex.test('Hello') // true
regex = /[bt]ear/
regex.test('tear') // true
regex.test('bear') // true
regex.test('dear') // false
var regex = /[^bt]ear/; // negated character set
console.log(regex.test('bear')); // false
console.log(regex.test('fear')); // true
regex = /[A-Z]/ // range
regex = /\d/ // digit, equivalent to [0-9]
regex = /\w/ // equivalent to [a-zA-Z0-9_]
regex = /\d+/ // matches preceding expression one or more time
regex = /Aa*/ // matches the preceding expression 0 or more times.
regex = /goo?d/ // matches the preceding expression 0 or 1 time
regex = /^good/ // beginning of the string
regex = /end\.$/ // end of the string with 'end.'. Escaping the '.' with '\.'
// return true

regex.match('
```

## Databases

>Object-relational mapping (ORM, O/RM, and O/R mapping tool) in computer science is a programming technique for converting data between incompatible type systems using object-oriented programming languages. This creates, in effect, a "virtual object database" that can be used from within the programming language.

>**ORM**: Object Relational Mapping
>**ODM**: Object Document Mapping

## API Design

### Resources

[Rest API - Best Practices - Youtube](https://www.youtube.com/watch?v=VsSBnLGM340)
[Best Practices for API Design - Stackoverflow blog](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)

#### Books

- RESTFUL Web APIs - Leonard Richardson & Mike Amundsen
- Principes of Web API Design James Higginbotham

### Notes

>When designing endpoints, it makes sense to group those that contain associated information. That is, if one object can contain another object, you should design the endpoint to reflect that. This is good practice regardless of whether your data is structured like this in your database. In fact, it may be advisable to avoid mirroring your database structure in your endpoints to avoid giving attackers unnecessary information.

>However, nesting can go too far. After about the second or third level, nested endpoints can get unwieldy. Consider, instead, returning the URL to those resources instead, especially if that data is not necessarily contained within the top level object.

## CSS

### Ressources

[CSS Battles](https://cssbattle.dev/)

## Misc

### Encoding

[Base64](https://en.wikipedia.org/wiki/Base64)
[Mime type](https://en.wikipedia.org/wiki/MIME)

## Transpiling

## Webpack


#### AJAX

>Asynchronous JavaScript and XML, while not a technology in itself, is a term coined in 2005 by Jesse James Garrett, that describes a "new" approach to using a number of existing technologies together, including HTML or XHTML, CSS, JavaScript, DOM, XML, XSLT, and most importantly the XMLHttpRequest object.

[Using XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)

### DOM

## Nodejs

Nodejs is a runtime JS environment based on the V8 engine (google Chrome engine).
calling nodejs in a shell spawns nodejs **REPL** ( Read-Eval-Print-Loop ).
NodeJS use asynchronous I/O API (libuv) to make non-blocking I/O and sockets calls.

### Require()

Require loads the code of the module and wrap it in a function then executes the code using v8 *vm.runInThisContext*.

```js
Module.wrap = function(script) {
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
  ```
[Require and the module system](http://fredkschott.com/post/2014/06/require-and-the-module-system)





