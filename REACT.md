## React
### React Hooks

Hooks are available only for function-based components, so they can't be used inside a class component.

#### `useState`

The `useState` hook is a function that takes one argument, which is the initial state, and it returns two values: the current state and a function that can be used to update the state.

```js
import React, { useState } from 'react'

function UserComponent() {
  const [name, setName] = useState('Frank')
}
```
We have a state named `name` and we can update it by calling on setName() function.
```js
import React, { useState } from 'react'

function UserComponent() {
  const [name, setName] = useState('Frank')

  return <h1> Hello there! My first name is {name} </h1>
}
```
Function components don't have the setState() function, you need to use the setName() function to update it.
```js
import React, { useState } from 'react'

function UserComponent() {
  const [name, setName] = useState('Frank')

  if(name === "Frank"){
    setName("Mike")
  }

  return <h1>Hello there! My first name is {name}</h1>
}
```
You can call the useState hook as many times as you need.
```js
import React, { useState } from 'react'

function UserComponent() {
  const [name, setName] = useState('Jack')
  const [age, setAge] = useState(10)
  const [isLegal, setLegal] = useState(false)
  const [friends, setFriends] = useState(["John", "Luke"])

  return <h1> Hello there! My first name is {name} </h1>
}
```
#### `useEffect`

The useEffect hook is the combination of `componentDidMount`, `componentDidUpdate` and `componentWillUnmount` class lifecycle methods. This hook is the ideal place to set up listeners, fetching data from API and removing listeners before the component is removed from the DOM.

Example
```js
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Nathan',
    };
  }

  componentDidMount() {
    console.log(
      `didMount triggered: Hello I'm ${this.state.name}`
    );
  }

  componentDidUpdate() {
    console.log(
      `didUpdate triggered: Hello I'm ${this.state.name}`
    );
  }

  render() {
    return (
      <div>
        <p>{`Hello I'm ${this.state.name}`}</p>
        <button
          onClick={() =>
            this.setState({ name: 'Gary'})
          }
        >
          Change me
        </button>
      </div>
    );
  }
}
```
Since `componentDidMount` is run only once when the component is inserted into the DOM tree structure, subsequent render won’t trigger the method anymore. In order to do run something on each render, you need to use `componentDidUpdate` method.

Using `useEffect` hook is like having both `componentDidMount` and `componentDidUpdate` in one single method, since `useEffect` runs on every render. It accepts two arguments:

* (mandatory) A function to run on every render
* (optional) An array of state variables to watch for changes. useEffect will be skipped if none of the variables are updated.

Rewriting the above class into function component would look like this:
```js
const Example = props => {
  const [name, setName] = useState('Nathan');

  useEffect(() => {
    console.log(`Hello I'm ${name}`);
  });

  return (
    <div>
      <p>{`Hello I'm ${name}`}</p>
      <button
        onClick={() => {
          setName('Gary')
          }}>
        Change me
      </button>
    </div>
  )
}
```
The function component above will run the function inside of `useEffect` function on each render. Now this isn’t optimal because the state won’t be updated after the first click. This is where `useEffect` second argument come into play.
```js
useEffect(() => {
    console.log(`Hello I'm ${name} and I'm a ${role}`);
  }, 
  [name]);
  ```
The second argument of `useEffect` function is referred to as the "dependency array". When the variable included inside the array didn't change, the function passed as the first argument won't be executed.

#### The `componentWillUnmount` effect

If you have code that needs to run when the component will be removed from the DOM tree, you need to specify a `componentWillUnmount` effect by writing a return statement into the first argument function. Here is an example:
```js
useEffect(() => {
    console.log(`useEffect function`);

    return () => { console.log("componentWillUnmount effect"); }
  }, [name] );
  ```
  #### Running `useEffect` only once
  
  To run `useEffect` hook only once like `componentDidMount` function, you can pass an empty array into the second argument:
  ```js
  useEffect(
  () => {
    console.log(`useEffect function`);
  }, 
  [] );
  ```
The empty array indicates that the effect doesn't have any dependencies to watch for change, and without a trigger, it won't be run after the component is mounted.
