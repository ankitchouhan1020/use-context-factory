## use-context-factory

This package provides an efficient way to create custom hooks for React Context api.


You may have used this pattern to create custom hooks for using context before and you might end up duplicating the code multiple times.

```js

const CounterContext = createContext(null);

export const CounterProvider = ({ children }) => {
    const [ count, setCount ] = useState(0);
    
    return (
        <CounterContext.Provider value={[ count, setCount ]}>
            { children }
        </CounterContext.Provider>
    );
}

export const useCounter = () => useContext(CounterContext);

```

This package provides a factory to create these custom hooks. [Code Sandbox Example](https://codesandbox.io/s/flamboyant-borg-8kh3bq?file=/src/App.js)

```js
const { createStateContext } from 'use-context-factory';

// It can be any custom hooks that return some value to pass to provider.
const useNumberState = (init) => useState(init || 0);

export const [ CounterProvider, useCount] = createStateContext(useNumberState);

///

const Parent = () => {
    return (
        <CounterProvider initialValue={1}>
            <Counter/>
        </CounterProvider>
    );
}

```

This pattern is mentioned in [Micro State Management with React Hooks](https://github.com/PacktPublishing/Micro-State-Management-with-React-Hooks).