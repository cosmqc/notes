#SENG365 
![[Pasted image 20240223110723.png]]
Protocols important, if we can rely on how information is coming in / what other programs are expecting, we can build our applications on top of them reliably.
HTTP is an application level protocol (7), used by browsers for almost all functionality.

HTTP messages are how data is exchanged between a server and a client.
Two types of message:
- Requests - sent by the client to trigger an action on the server
- Responses - returned by the server in response to a request
Encoded in ASCII. HTTP/<1.1, messages were sent unencoded across the network.

**URI - Uniform Resource Identifier** - string of characters to identify a resource
>dmn.tld/page.htm, ste.org/img.png

**URL - Uniform Resource Locator** - A URI that also specifies the protocol for retrieval
> https://dmn.tld/page.htm, ftp://ste.org/img.png

The path in a URL is increasingly not actually the path to the file location, but being parsed and processed to give the file.

### Headers
General headers -> headers that must be there 
- Request URL, Request Method, Remote Address
Entity headers -> headers that apply to the body of the request, variable
- Content-Length, Content-Type, Expires etc
Cookies -> headers that establish a session of sorts
- Set-Cookie, Cookie

Forbidden headers are ones that cannot be set programmatically (i.e. can be thought of as a source of truth). They usually describe the request itself rather than something the client wants the server do to as a side-effect. Well known ones include:
- Content-Length
- Host
- Referer
- Keep-Alive
- Anything starting with `Proxy-`, i.e.
	- Proxy-Authorization
	- Proxy-Forwarded-For
- Anything starting with `Sec-` (security standard created by W3C)
	- Sec-Fetch-Mode (`navigate`, `cors`, `no-cors`, `same-origin`, `websocket`)
	- Sec-Fetch-Dest (`document`, `script`, `style`, etc.)
### HTTP verbs (request methods)
- GET
- PUT
- POST
- DELETE
- HEAD
- [lots more](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

### HTTP response codes
- 1xx -> informational, not used often anymore
- 2xx -> success
	- e.g. 200 OK, 201 created, 204 No content
- 3xx -> redirection
	- e.g. 303 See Other, 304 Not Modified
- 4xx -> client error
	- e.g. 400 Bad request, 404 Not found
- 5xx -> server error
	- e.g. 500 Internal server error, 501 Not implemented

## APIs
APIs use the same URI format, but for a different purpose (getting parameters).
Sometimes also includes the version infomation of the API.
> localhost:3000/api/v1/students/:id?key1=val1

API versioning usually takes the form major.minor.patch (i.e. version 1.2.15)
- Patch is for fixes that don't change intended functionality
- Minor is for functionality changes that doesn't remove or edit other functionality (but may deprecate it). This means software made for v1.1 will still work on v1.3
- Major is for functionality changes that may remove or edit other functionality. This usually means software made for v2.0 will not work for v3.0
## Javascript
Object-oriented language
- Not as strict as Java in its definition of objects (don't *have* to have classes)
Object -> a collection of properties
Property -> Association between a key and a value
Method -> Function accociated with an object, or a property of an object.

First-class object
- May be named by variables
- May be passed as arguments to functions
- May be returned as results of functions
- May be included in data structures

<ES6 - Undeclared variables allowed unless `use strict` used.
```js
a = 1; // before ES6, undeclared variables could be used
var b = 1; // compared to this, a declared var
```
`use strict` also:
- Prevents accidental creation of global variables
```js
function strict_function() {
  'use strict';

  x = 'I am a strict function';

  console.log(x);
}

strict_function(); // ReferenceError: x is not defined
```

ES6+ - Variables must be declared
```js
var c = 1 // var is lexically-scoped - autoadded to global scope.
let d = 2; // let is block-scoped - only accessible within its block
const e = 3; // const also block-scoped, but cannot be changed once set
```

#### Block scope
Variables defined within a block cannot be accessed from outside of it.
Used in languages like Java, C#, C, and C++.
```java
// x is only available within the if block
public void foo() {
	if (condition) {
		int x = 1;
	}
	System.out.println(x); // errors, x is undefined
}
```

#### Lexical scope
Variables are available to the parents and all the parents children.
Used in languages like Javascript and R
```js
function foo() {
	if (condition) {
		var x = 1;
	}
	console.log(x); // 1
}
```

### Anonymous functions
```js
function (a, b) { return a + b; }; // Before ES6
(a, b) => a + b; // ES6+, 
```

New 'arrow' functions don't redefine 'this'.  
```js
// Doesn't work, this refers to global object which doesn't have a color tag.
// (Even if the window does have .color, it's likely not the object intended)
this.color = 'red';
setTimeout(
	function() {
		this.color = 'green'
	}, 
	1000
	}
)

// Works as intended
this.color = 'red';
setTimeout(
	() => {this.color = 'green'}, 
	1000}
)
```

### Immediately Invoked function expression (IIFE)
```javascript
(function() {
	statements
})();
```
Outer brackets enclose an anonymous function, right side ones execute it.
This means the variables from that function aren't global and are lost after the function finishes (good :) )
### Closure
When JS executes a function it uses the variables in-scope **at the time of definition** of the function, not the time of creation. A closure is a record storing a function together with the environment it was in at definition.
Common uses of closures include:
- Encapsulation / private variables
```js
// Below shows an example of using a closure for private variables.
// The outer scope has no access/knowledge of the variable count, 
// but can still be manipulated.
function counter() {
	let count = 0;
	return function() {
		count++;
		console.log(count);
	}
}

const increment = counter();
increment(); // Output: 1
increment(); // Output: 2
increment(); // Output: 3
```
- Function factories
- Callback functions
```js
function fetchData(url, callback) {
	setTimeout(function() {
		let data = 'Data fetched from ' + url;
		callback(data);
	}, 1000);
}

let process = function(data) {
	console.log(data);
};

fetchData('https://example.com/api', process);
```
- Event handlers

### Function Chaining
```js
let result = method1().method2(args).method3();
```

Usually achieved via `return this` at the end of each function.
In above example, this may require `method1` to create the object.

Why?
- Reduces temporary variables, no need to create vars for each step of the process
- The code is expressive, reads like a sentence especially if code named as verbs.
- The code is more maintainable, requires coherent design to the chained methods
### `use strict`
A way of maintaining backwards compatibility, modifies how the code is interpretted

### Event loop
**Call stack** - a data structure to maintain a record of function calls
- Call a function to execute: push something onto the stack
- Return from a function: pop off the top of the stack
- the single thread

**Heap** - Memory allocation to variables and objects
**Queue** - a list of messages to be processed and the associated callback functions to execute. Items are taken from the front of the queue and put on the stack when the stack is empty. Not usually a lot on the stack at a time, so queue moves quickly.

![[Pasted image 20240301111057.png]]

```js
// Which will print first? 
setTimeout(() => console.log('first'), 0);
console.log('second')
```
Turns out it will log `second` first, then `first`. `setTImeout` is an external API (still within the browser, but outside Javascript), so it will send off the anonymous function to that API and tell it to send back a request immediately to run the log function. The API will do that, and the request will be added to the queue. The stack still has something in it (the `second` log call), so it will execute that first then afterwards once the stack is empty, it will execute the `first` log. 
`setInterval` is the same, but occurs repeatedly with `n`ms between the calls instead of just once.

Other browser-provided web APIs include:
- DOM events (click, load, resize etc)
- XML_HttpRequest (ajax)
- Timers (setTimeout, setInterval, etc)


Promise callback functions are given higher precedence than web API callbacks like setTimeout. Consider the task queue a priority queue that puts promise callbacks at the front (as well as other [microtasks)](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide), or a microtask queue separate from the rest of the task queue. Tasks are only taken off the regular task queue if both the call stack **and** the microtask queue are empty.

![[Pasted image 20240606165818.png]]
## Callback hell and the Pyramid of Doom
An API call from the client may under-fetch data, ie API not designed to return every bit of data the user needs, requires multiple calls. This produces a nested set of API calls (like a **pyramid**) where each call depends on the previous one succeeding, which the client must test.

To prevent this ''Pyramid of Doom", the `Promise` object was created. It's used for deferred and async computations. Promises allow for sync and async operations to be used together. A Promise represents an operation that hasn't been completed yet, but is expected in the future. Can be in one of three state
- Pending state - initial state, not fulfilled or rejected yet
- Fulfilled state - Operation completed successfully
- Rejected state - Operation failed
![[Pasted image 20240301113909.png]]

`async` flag ensures a function returns a Promise, i.e.
```js
async function f() { 
	return 1; 
}
f().then( () => { console.log(result); } );
```

`await` is its counterpart, it forces Javascript to wait for a promise to be fulfilled so other code can continue to run.

## Direct Object Model (DOM)
The DOM is the entire tree of HTML objects on a webpage. It usually starts off small, but becomes massive when you've scrolled a bit in apps like Facebook or Snapchat, leading to a performance impact.

Solution: the **Virtual DOM** (fake)!!
- An abstraction of the actual DOM
- Modify the virtual DOM, and only render it when needed
- Means you don't need to work directly with the DOM

### When should the DOM be updated?
#### Dirty Checking
Poll the data at regular intervals to check the data structure recursively
#### Observable
Observe for state change. If no change, do nothing. If change, we know exactly *what* to update.
### How should it be updated?
- Need efficient DIFF algorithms
- Batch DOM read/write operations
- Efficient update of sub-tree only

![[Pasted image 20240610213342.png]]
## Javascript Frameworks
### AngularJS
Platform for enterprise web development, written in solely Typescript.
- Complex to learn
- Two-way binding
- Dirty-checking for DOM updates
- Templating
### React
Defines reusable **components** in JSX
- JSX is JS with HTML elements as objects, compiled to HTML before running in browser
- Each component has a life cycle
- Uses a virtual DOM
- No templating
- Most popular framework, v many libraries !!
### VueJS
Designed by Google dev who thought Angular was too heavy
- Uses components with life cycles (like React)
- Virtual DOM
- Templating
### Svelte
Parses its own .svelte files and compiles into JS.
- Abstract syntax tree to generate JS and CSS
- Compiled JS mounts component, handles events, and patches DOM itself
- No framework code, v small and fast code :)