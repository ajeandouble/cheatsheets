# React

## Resources

## Using React


### Component Lifecycle

#### Mounting

When an instance is being created and inserted into the **DOM**:

- `constructor()`
- `static getDerivedStateFromProps()`
- `render()`
- `componentDidMount()`

#### Updating

- `static getDerivedStateFromProps()`
- `shouldComponentUpdate()`
- `render()`
- `getSnapshotBeforeUpdate()`
- `componentDidUpdate()`

#### Unmounting

- `componentWillUnmount()`

#### Methods

##### `static getDerivedStateFromProps()`

The `getDerivedStateFromProps()` method can be used to preset or initialize the state of a class component based on the values of the props instead of directly setting the props as the state, you can perform additional logic or transformations.

```js
class MyComponent extends React.Component {
	static getDerivedStateFromProps(props, state) {
		return { value: props.value + 'whatever' };
	}
	state = { value: '' };
	render () { return <></> };
```

##### `render()`

It is the only required method in a class component.
`render()` will not be invoked if `shouldComponentUpdate()` returns false.


#### `componentDidMount()`

>`componentDidMount()` is invoked immediately after a component is mounted (inserted into the tree). 

>It is a good place to set up any subscriptions. If you do that, don’t forget to unsubscribe in componentWillUnmount().

[Legacy React.js doc](https://legacy.reactjs.org/docs/react-component.html#componentdidmount)

##### `shouldComponentUpdate()`

>Use `shouldComponentUpdate()` to let React know if a component’s output is not affected by the current change in state or props. The default behavior is to re-render on every state change, and in the vast majority of cases you should rely on the default behavior.

##### `componentWillUnmount()`

>`componentWillUnmount()` is invoked immediately before a component is unmounted and destroyed. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in `componentDidMount()`.

##### `componentDidUpdate()`

>`componentDidUpdate()` is invoked immediately after updating occurs. This method is not called for the initial render.

> `componentDidUpdate()` will not be invoked if `shouldComponentUpdate()` returns `false`.
 
[Legacy React.js doc](https://legacy.reactjs.org/docs/react-component.html#componentdidupdate)

It is a good place to operate on the *DOM* and perform network requests on component update.

#### `getSnapshotBeforeUpdate()`

>It is invoked right before the most recently rendered output is committed to e.g. the DOM. It enables your component to capture some information from the *DOM* (e.g. scroll position) before it is potentially changed. Any value returned by this lifecycle method will be passed as a parameter to `componentDidUpdate()`.

[Legacy React.js doc](https://legacy.reactjs.org/docs/react-component.html#getsnapshotbeforeupdate)



## Using React

[Redux in 100 seconds - youtube](https://www.youtube.com/watch?v=_shA5Xwe8_4)

It was created at facebook.