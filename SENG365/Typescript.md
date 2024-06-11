#SENG365

Typescript was created by Microsoft in response to problems with [[HTTP & Javascript#Javascript|Javascript]]. Their goal was to write safer web code quicker. Typescript is a superset of Javascript, so any JS can be run as TS, but not the other way around.

[Code playground](https://www.typescriptlang.org/play/)
#### Problems with Javascript
- Dynamically typed
```js
var container = "hello";
container = 43; // valid :(
```

- Type coercion behaves in unexpected ways ([someone made another language of it](https://jsfuck.com/))
```js
null > 0; // false
null == 0; // false
null >= 0; // true

(!+[]+[]+![]).length; // 9
```
-
- Lots of different versions supported by different browsers
#### What does Typescript add?
- Static typing - once a variable is defined, its type cannot be changed
```ts
let container: number = 3;
container = "a string!!" // ERROR: Type string is not assignable to type number
```

- Type inference - the type of the variable doesn't always need to be explicitly stated
```ts
let example = "i'm obviously a string";
console.log(typeof example); // string
```

- Strict null checking - verifies a value exists before being used
```ts
const users = [
	{ name: "Oby", age: 12 },
	{ name: "Heera", age: 32 },
];

const user = users.find((u) => u.name === "Kush");
console.log(user.name); // ERROR: user is possibly 'undefined'
```


