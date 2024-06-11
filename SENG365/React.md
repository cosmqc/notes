#SENG365
Javascript framework that defines reusable **components** in JSX
- Each component has a life cycle
- Uses a virtual DOM
- No templating
- Most popular framework, v many libraries !!

## JSX
JSX is JS with HTML elements as objects, compiled to HTML before running in browser.
- Elements must have a single top level element
- Curly braces put us back in normal JS (so can comment by going back to JS first)
- Conditional statements usually done with short circuit logic

```jsx
const singleLineElement = <h1>Welcome all!</h1>;

const containsEvaluatedJs = <h1>{20 * 20}</h1>;

const multiLineElement = (
	<ul>
		<li>Item 1</li>
		<li>Item 2</li>
		<li>Item 3</li>
		<li>Item 4</li>
		<li>Item 5</li>
	</ul>
);

{ /* I hate comments in React :( */ }

const conditional = (
	<ul>
		<li>Always here</li>
		{ !isLoggedIn && <li>Only here if not logged in</li> }
		{ isLoggedIn ? <li>Logout</li> : <li>Login</li> }
	</ul>
)
```

### JSX Compilation
JSX is syntactic sugar for React.createElement(), which takes three elements:
- Type - eg `h1`
- Properties (usually called **props**) - e.g. styling, callbacks, or `null` if no props (like below)
	- Props are read-only and cannot be modified
- Children - e.g. other elements, or just inner text

```jsx
const before = <h1>Awesome react element!</h1>;

const after = React.createElement('h1', null, 'Awesome react element!');
```

## Components
### Functional components
- they exist :)
- used in assignment 
### Class components
- Manage their own state, materialized at initialization
- `state` should not be set directly, but instead by calling `this.setState()`
	- This is a async request to change it, not updated immediately
- The object sent to setState is merged with the existing state in a batch operation
	- This is why we can't just set `state`, because it needs to be merged w other async requests.
- The state should not be updated in render, otherwise infinite renders
	- Render on state change, state change on render :(((
```jsx
class Welcome extends React.Component {
	constructor(props) {
		super(props);
		this.state = {date: new Date()};
	}

	render() {
		return <h1>Hello {this.props.name}</h1>
	}
}
```


## Event handling and hooks
Similar to HTML events (on click, onsubmit) with some key differences:
- Camel case ✨ (onClick, onSubmit)
- Pass a function as the event handler instead of just raw javascript
	- `handleSubmit` or `() => handleSubmit()`, instead of `handleSubmit()` 
	- The function can be a method of the component, but `this` must be bound

### Hooks
![[Pasted image 20240610223323.png]]

Functions given by React that we can use to do complex Class component stuff with functional components in a much simpler way.

#### Rules of hooks
- Only call at Top Level (no loops, in conditions, etc.)
- Only call from React functions or custom hooks

```jsx
const [count, setCount] = useState(0);

return (
	<div>
		<p>You clicked {count} times!</p>
		<button onClick={() => setCount(count + 1)}>
			Click me
		</button>
	</div>
)
```

```jsx
// add reducer code
```

```jsx
// useEffect: Creates side effects in code.
// something happens, something else happens

const [count, setCount] = useState(0);

useEffect(
	() => {
		document.title = `You've clicked ${count} times`;
	}, // function to execute
	[count] // dependancy array; when count changes, rerun
)

return (
	<div>
		<button onClick={() => setCount(count + 1)}
	</div>
)
```

#### How do hooks work?
- Reconciliation - tree diffing algorithm in React that's used to say what's changed (vDOM)
- Render - uses that info to change the app view

Reconcilliation is implemented using fibers. :)


## State

### Redux
Reducers - pure functions that take an action and update the state.
State is immutable so creates a new state with the changes needed and sets the state to the new object. 
![[Pasted image 20240610224921.png]]

### Zustand
Uses same principles under the hood, but less boilerplate. Used in labs + assignment
1. Create a context object
2. Wrap components in context Provider, and pass state as value
3. Child components can access state with `useContext()`