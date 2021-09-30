# React Hooks

## State

### Counter

```useState``` can be used to keep track of a variable through multiple re-renders, such as in a counter application:
```jsx
import { useState } from "react";

const UseCaseCounter = props => {
    const [counter, setCounter] = useState(0);

    // Use setState function form because the new state depends on the previous one
    const clickHandlerDecrease = () => {
        // Converting the prevState to number to avoid errors
        setCounter(prevState => +prevState - 1);
    };

    const clickHandlerIncrease = () => {
        setCounter(prevState => +prevState + 1);
    };

    return (
        <>
            <hr />
            <h2>useState use case</h2>
            <h3>Counter</h3>
            <button onClick={clickHandlerDecrease}>--</button>
            <span> {counter} </span>
            <button onClick={clickHandlerIncrease}>++</button>
        </>
    );
};

export default UseCaseCounter;
```

### Conditional rendering
Use a state to conditionally render a component or part of it.
```jsx
import { useState } from "react";

const UseCaseConditionalRender = props => {
    const [condition, setCondition] = useState(false);

    const clickHandler = () => {
        setCondition(true);
    };

    return (
        <>
            <hr />
            <h2>useState use case</h2>
            <h3>Conditional Rendering</h3>
            <button onClick={clickHandler}>Set condition</button>
            {condition && <p>Hello!</p>}
        </>
    );
};

export default UseCaseConditionalRender;
```
### Toggle Values
```useState``` can be used to toggle between two values, usually ```true``` and ```false```, in order to toggle a flag, such as the display mode:
```jsx
import { useState } from 'react';
import classes from './UseCaseToggle.module.css';

const UseCaseToggle = props => {
    const [mode, setMode] = useState(false);

    // Use setState function form because the new state depends on the previous one
    const clickHandler = () => {
        setMode(prevState => !prevState);
    };

    const toggledClass = mode ? classes.light : classes.dark;

    return (
        <div className={toggledClass}>
            <hr />
            <h2>useState use case</h2>
            <h3>Toggle flags</h3>
            <button onClick={clickHandler}>Toggle display mode</button>
        </div>
    );
};

export default UseCaseToggle;
```

### Get API data and store it in state
Interact with an API. Use a state to store the response of a ```fetch()``` to the API, and the state of a spinner that will indicate if the data is being fetched.
```jsx
import { useState } from "react";

const UseCaseApi = props => {
    const [starship, setStarship] = useState('');
    const [isLoading, setIsLoading] = useState(false);

    const clickHandler = async () => {
        setIsLoading(true);

        const response = await fetch('https://swapi.dev/api/starships/10');
        const data = await response.json();
        setStarship(JSON.stringify(data, null, "\t"));

        setIsLoading(false);
    };

    let message = '';
    if (isLoading) {
        message = <p>Getting data... 🚀</p>;
    }

    return (
        <>
            <hr />
            <h2>useState use case</h2>
            <h3>Get API data and store it in state</h3>
            <button onClick={clickHandler}>Get Millennium Falcon data</button>
            <p>{message}</p>
            <pre>{starship}</pre>
        </>
    );
};

export default UseCaseApi;
```
