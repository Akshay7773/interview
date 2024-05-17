
  ============================================================ ## REACT OLD ## ==========================================================================================================

  ## Q.1 WHAT IS REACT AND HOW YOU CAN BEST DESCRIBES IT ? 
  React is an open-source JavaScript library developed and maintained by Facebook. It is primarily used for building user interfaces (UI) for single-page applications where the content can be dynamically updated without requiring a full page reload. React allows developers to create reusable UI components and manage the state of an application efficiently.

Key features of React include:

1. **Component-Based Architecture:** React is built around the concept of components, which are reusable and self-contained units of UI. Components can be composed together to create complex UI structures.
2. **Virtual DOM (Document Object Model):** React uses a virtual DOM to optimize the updating process. Instead of updating the entire DOM when changes occur, React compares the virtual DOM with the actual DOM and only makes the necessary updates, resulting in improved performance.
3. **Declarative Syntax:** React uses a declarative syntax, making it easier to understand and reason about the code. Developers describe what the UI should look like, and React takes care of updating the DOM to match the specified state.
4. **JSX (JavaScript XML):** JSX is a syntax extension for JavaScript that looks similar to XML or HTML. It allows developers to write HTML-like code within JavaScript, making the creation of React components more intuitive.
5. **Unidirectional Data Flow:** React follows a unidirectional data flow, where data flows in a single direction—from parent components to child components. This helps in maintaining a clear and predictable state management structure.
6. **React Native:** React can be used not only for web development but also for mobile app development through React Native. It enables the creation of cross-platform mobile applications using the same React concepts.

Overall, React simplifies the process of building interactive and dynamic user interfaces by providing a modular, efficient, and scalable framework for web development. It has gained widespread adoption in the web development community due to its flexibility, performance, and the active community support around it.


<br> 


## Q.2 React memo
Using `memo` will cause React to skip rendering a component if its props have not changed.

This can improve performance.

"Memoization in React is the process of optimizing component rendering by preventing unnecessary re-renders. In functional components, we use **`React.memo`** as a higher-order component. When a component is wrapped with **`React.memo`**, it memoizes the component so that it only re-renders if its props have changed. Specifically, it checks whether the previous props are shallowly equal to the new props. If the props remain the same, React returns the memoized version of the component, avoiding unnecessary renders and improving performance."

# Problem

In this example, the `Todos` component re-renders even when the todos have not changed.

# Example:

`index.js`:

```jsx
import { useState } from "react";
import ReactDOM from "react-dom/client";
import Todos from "./Todos";

const App = () => {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState(["todo 1", "todo 2"]);

  const increment = () => {
    setCount((c) => c + 1);
  };

  return (
    <>
      <Todos todos={todos} />
      <hr />
      <div>
        Count: {count}
        <button onClick={increment}>+</button>
      </div>
    </>);
};

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);

```

`Todos.js`:

```jsx
const Todos = ({ todos }) => {
  console.log("child render");
  return (
    <>
      <h2>My Todos</h2>
      {todos.map((todo, index) => {
        return <p key={index}>{todo}</p>;
      })}
    </>);
};

export default Todos;
```

When you click the increment button, the `Todos` component re-renders.

If this component was complex, it could cause performance issues.

# Solution

To fix this, we can use `memo`.

Use `memo`to keep the `Todos` component from needlessly re-rendering.

Wrap the `Todos` component export in `memo`:

# Example:

`index.js`:

```jsx
import { useState } from "react";
import ReactDOM from "react-dom/client";
import Todos from "./Todos";

const App = () => {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState(["todo 1", "todo 2"]);

  const increment = () => {
    setCount((c) => c + 1);
  };

  return (
    <>
      <Todos todos={todos} />
      <hr />
      <div>
        Count: {count}
        <button onClick={increment}>+</button>
      </div>
    </>);
};

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);

```

`Todos.js`:

```jsx
import { memo } from "react";

const Todos = ({ todos }) => {
  console.log("child render");
  return (
    <>
      <h2>My Todos</h2>
      {todos.map((todo, index) => {
        return <p key={index}>{todo}</p>;
      })}
    </>);
};

export default memo(Todos);
```

Now the `Todos` component only re-renders when the `todos` that are passed to it through props are updated.

<br> 



## Q.3 what is the use of event.preventDefault
The **`event.preventDefault()`** method is used in web development to prevent the default behavior of an event. Events in web browsers often have default behaviors associated with them. For example, when you submit a form, the browser typically reloads the page. Similarly, clicking on a link may navigate to a new page.

By calling **`event.preventDefault()`** within an event handler, you can stop the browser from executing the default behavior associated with that event. This allows you to implement your own custom behavior without the interference of the browser's default actions.

Here's an example of using **`event.preventDefault()`** in a React component:

```jsx

import React from 'react';

function MyForm() {
  const handleSubmit = (event) => {
    // Prevent the default form submission behavior (page reload)
    event.preventDefault();

    // Implement custom form submission logic
    // (e.g., send data to a server, update state, etc.)
    console.log('Form submitted!');
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}

```

In this example, when the form is submitted, the **`handleSubmit`** function is called. The first line of the function, **`event.preventDefault()`**, prevents the default form submission behavior. This allows you to handle the form submission in a custom way, such as making an asynchronous request to a server or updating the state in a React component, without causing a page reload.


<br> 

## Q.4 what happened if we do not import react in component? 
In a React component, if you do not import the **`React`** object from the 'react' module, you may encounter issues because the JSX syntax used in React components relies on **`React`** being in scope. When you write JSX code, it is ultimately transformed into **`React.createElement()`** calls by the React compiler.

If you omit the import statement like this:

```jsx
jsxCopy code
// Incorrect: Missing import statement for React
function MyComponent() {
  return (
    <div>
      {/* JSX code */}
    </div>
  );
}

```

You may encounter errors similar to:

```vbnet
ReferenceError: React is not defined
```

To resolve this issue, you should import **`React`** at the top of your file, even if you don't explicitly use it in your component:

```jsx
jsxCopy code
import React from 'react';

function MyComponent() {
  return (
    <div>
      {/* JSX code */}
    </div>
  );
}

```

Keep in mind that starting from React 17, the automatic import of **`React`** in each file where JSX is used is not required. You can use JSX without importing **`React`** explicitly. However, this behavior is specific to React 17 and later versions. If you are using an earlier version of React, you still need to import **`React`**.

<br> 


## Q.5 Hooks
In React, hooks are functions that enable functional components to have state and side effects. They were introduced in React version 16.8 to provide a more expressive and reusable way to manage component state and lifecycle events in functional components. Hooks allow developers to use state and other React features without writing a class.

**Hook allows us to use of state , lifecycle methods .**

---

# What is a Hook?

Hooks allow us to "hook" into React features such as state and lifecycle methods.

# Example:

Here is an example of a Hook. Don't worry if it doesn't make sense. We will go into more detail in the [next section](https://www.w3schools.com/REACT/react_usestate.asp).

```jsx
import React, { useState } from "react";
import ReactDOM from "react-dom/client";

function FavoriteColor() {
  const [color, setColor] = useState("red");

  return (
    <>
      <h1>My favorite color is {color}!</h1>
      <button
        type="button"onClick={() => setColor("blue")}>Blue</button>
      <button
        type="button"onClick={() => setColor("red")}>Red</button>
      <button
        type="button"onClick={() => setColor("pink")}>Pink</button>
      <button
        type="button"onClick={() => setColor("green")}>Green</button>
    </>);
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<FavoriteColor />);
```

[Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_hooks)

You must `import` Hooks from `react`.

Here we are using the `useState` Hook to keep track of the application state.

State generally refers to application data or properties that need to be tracked.

---

# Hook Rules

There are 3 rules for hooks:

- Hooks can only be called inside React function components.
- Hooks can only be called at the top level of a component.
- Hooks cannot be conditional

<br> 


## Q.6 usestate,  useEffect, useContext, useRef
1. useState: 

The React `useState` Hook allows us to track state in a function component.

State generally refers to data or properties that need to be tracking in an application.

---

# Import useState

To use the `useState` Hook, we first need to `import` it into our component.

# Example:

At the top of your component, `import` the `useState` Hook.

```jsx
import { useState } from "react";

```

Notice that we are destructuring `useState` from `react` as it is a named export.

To learn more about destructuring, check out the [ES6 section](https://www.w3schools.com/REACT/react_es6.asp).

---

# Initialize useState

We initialize our state by calling `useState` in our function component.

`useState` accepts an initial state and returns two values:

- The current state.
- A function that updates the state.

# Example:

Initialize state at the top of the function component.

```jsx
import { useState } from "react";

function FavoriteColor() {
  const [color, setColor] = useState("");
}

```

Notice that again, we are destructuring the returned values from `useState`.

The first value, `color`, is our current state.

The second value, `setColor`, is the function that is used to update our state.

1. useEffect: 
    
    The `useEffect` Hook allows you to perform side effects in your components.
    
    Some examples of side effects are: fetching data, directly updating the DOM, and timers.
    
    `useEffect` accepts two arguments. The second argument is optional.
    
    `useEffect(<function>, <dependency>)`
    
    ---
    
    Let's use a timer as an example.
    
    # Example:
    
    Use `setTimeout()` to count 1 second after initial render:
    
    ```jsx
    import { useState, useEffect } from "react";
    import ReactDOM from "react-dom/client";
    
    function Timer() {
      const [count, setCount] = useState(0);
    
      useEffect(() => {
        setTimeout(() => {
          setCount((count) => count + 1);
        }, 1000);
      });
    
      return <h1>I've rendered {count} times!</h1>;
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<Timer />);
    ```
    
    [Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_useeffect_settimeout)
    
    But wait!! It keeps counting even though it should only count once!
    
    `useEffect` runs on every render. That means that when the count changes, a render happens, which then triggers another effect.
    
    This is not what we want. There are several ways to control when side effects run.
    
    We should always include the second parameter which accepts an array. We can optionally pass dependencies to `useEffect` in this array.
    
    # Example
    
    1. No dependency passed:
    
    ```jsx
    useEffect(() => {
      //Runs on every render
    });
    ```
    
    # Example
    
    2. An empty array:
    
    ```jsx
    useEffect(() => {
      //Runs only on the first render
    }, []);
    ```
    
    # Example
    
    3. Props or state values:
    
    ```jsx
    useEffect(() => {
      //Runs on the first render
      //And any time any dependency value changes
    }, [prop, state]);
    ```
    
    So, to fix this issue, let's only run this effect on the initial render.
    
    # Example:
    
    Only run the effect on the initial render:
    
    ```jsx
    import { useState, useEffect } from "react";
    import ReactDOM from "react-dom/client";
    
    function Timer() {
      const [count, setCount] = useState(0);
    
      useEffect(() => {
        setTimeout(() => {
          setCount((count) => count + 1);
        }, 1000);
      }, []); // <- add empty brackets here
    
      return <h1>I've rendered {count} times!</h1>;
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<Timer />);
    ```
    
    [Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_useeffect_settimeout2)
    
    # Example:
    
    Here is an example of a `useEffect` Hook that is dependent on a variable. If the `count` variable updates, the effect will run again:
    
    ```jsx
    import { useState, useEffect } from "react";
    import ReactDOM from "react-dom/client";
    
    function Counter() {
      const [count, setCount] = useState(0);
      const [calculation, setCalculation] = useState(0);
    
      useEffect(() => {
        setCalculation(() => count * 2);
      }, [count]); // <- add the count variable here
    
      return (
        <>
          <p>Count: {count}</p>
          <button onClick={() => setCount((c) => c + 1)}>+</button>
          <p>Calculation: {calculation}</p>
        </>);
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<Counter />);
    ```
    
    [Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_useeffect_settimeout3)
    
    If there are multiple dependencies, they should be included in the `useEffect` dependency array.
    
    ---
    
    ---
    
    # Effect Cleanup
    
    Some effects require cleanup to reduce memory leaks.
    
    Timeouts, subscriptions, event listeners, and other effects that are no longer needed should be disposed.
    
    We do this by including a return function at the end of the `useEffect` Hook.
    
    # Example:
    
    Clean up the timer at the end of the `useEffect` Hook:
    
    ```jsx
    import { useState, useEffect } from "react";
    import ReactDOM from "react-dom/client";
    
    function Timer() {
      const [count, setCount] = useState(0);
    
      useEffect(() => {
        let timer = setTimeout(() => {
        setCount((count) => count + 1);
      }, 1000);
    
      return () => clearTimeout(timer)
      }, []);
    
      return <h1>I've rendered {count} times!</h1>;
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<Timer />);
    ```
    
    1. useContext:
        
        # React Context
        
        React Context is a way to manage state globally.
        
        It can be used together with the `useState` Hook to share state between deeply nested components more easily than with `useState` alone.
        
        It is used to avoid prop drilling.
        
        e.g. 
        
        suppose we have 5 components. And each component is a child of another component that means . 
        
        Component 1 is a parent of Component 2, Component 2 is a parent of Component 3 and so on….
        
        if we want to pass prop from Component1 to Component5 then we need to pass it in every component as a prop. So this is called prop drilling. So to avoid this we use useContext hook.
        
        ---
        
        # The Problem
        
        State should be held by the highest parent component in the stack that requires access to the state.
        
        To illustrate, we have many nested components. The component at the top and bottom of the stack need access to the state.
        
        To do this without Context, we will need to pass the state as "props" through each nested component. This is called "prop drilling".
        
        # Example:
        
        Passing "props" through nested components:
        
        ```jsx
        import { useState } from "react";
        import ReactDOM from "react-dom/client";
        
        function Component1() {
          const [user, setUser] = useState("Jesse Hall");
        
          return (
            <>
              <h1>{`Hello ${user}!`}</h1>
              <Component2 user={user} />
            </>);
        }
        
        function Component2({ user }) {
          return (
            <>
              <h1>Component 2</h1>
              <Component3 user={user} />
            </>);
        }
        
        function Component3({ user }) {
          return (
            <>
              <h1>Component 3</h1>
              <Component4 user={user} />
            </>);
        }
        
        function Component4({ user }) {
          return (
            <>
              <h1>Component 4</h1>
              <Component5 user={user} />
            </>);
        }
        
        function Component5({ user }) {
          return (
            <>
              <h1>Component 5</h1>
              <h2>{`Hello ${user} again!`}</h2>
            </>);
        }
        
        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<Component1 />);
        
        ```
        
        [Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_context1)
        
        Even though components 2-4 did not need the state, they had to pass the state along so that it could reach component 5.
        
        ---
        
        [w3schoolsCERTIFIED.2022](https://shop.w3schools.com/collections/course-catalog)
        
        # Get Certified!
        
        Complete the React modules, do the exercises, take the exam and become w3schools certified!!
        
        [$95 ENROLL](https://shop.w3schools.com/collections/course-catalog/products/react-js-course)
        
        ---
        
        # The Solution
        
        The solution is to create context.
        
        # Create Context
        
        To create context, you must Import `createContext` and initialize it:
        
        `import { useState, createContext } from "react";
        import ReactDOM from "react-dom/client";
        
        const UserContext = createContext()`
        
        Next we'll use the Context Provider to wrap the tree of components that need the state Context.
        
        # Context Provider
        
        Wrap child components in the Context Provider and supply the state value.
        
        `function Component1() {
          const [user, setUser] = useState("Jesse Hall");
        
          return (
            <UserContext.Provider value={user}>
              <h1>{`Hello ${user}!`}</h1>
              <Component2 user={user} />
            </UserContext.Provider>);
        }`
        
        Now, all components in this tree will have access to the user Context.
        
        # Use the useContext Hook
        
        In order to use the Context in a child component, we need to access it using the `useContext` Hook.
        
        First, include the `useContext` in the import statement:
        
        `import { useState, createContext, useContext } from "react";`
        
        Then you can access the user Context in all components:
        
        `function Component5() {
          const user = useContext(UserContext);
        
          return (
            <>
              <h1>Component 5</h1>
              <h2>{`Hello ${user} again!`}</h2>
            </>);
        }`
        
        ---
        
        # Full Example
        
        # Example:
        
        Here is the full example using React Context:
        
        ```jsx
        import { useState, createContext, useContext } from "react";
        import ReactDOM from "react-dom/client";
        
        const UserContext = createContext();
        
        function Component1() {
          const [user, setUser] = useState("Jesse Hall");
        
          return (
            <UserContext.Provider value={user}>
              <h1>{`Hello ${user}!`}</h1>
              <Component2 />
            </UserContext.Provider>);
        }
        
        function Component2() {
          return (
            <>
              <h1>Component 2</h1>
              <Component3 />
            </>);
        }
        
        function Component3() {
          return (
            <>
              <h1>Component 3</h1>
              <Component4 />
            </>);
        }
        
        function Component4() {
          return (
            <>
              <h1>Component 4</h1>
              <Component5 />
            </>);
        }
        
        function Component5() {
          const user = useContext(UserContext);
        
          return (
            <>
              <h1>Component 5</h1>
              <h2>{`Hello ${user} again!`}</h2>
            </>);
        }
        
        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<Component1 />);
        ```
        
        1. useRef 
            
            The `useRef` Hook allows you to persist values between renders.
            
            It can be used to store a mutable value that does not cause a re-render when updated.
            
            It can be used to access a DOM element directly.
            
            ---
            
            # Does Not Cause Re-renders
            
            If we tried to count how many times our application renders using the `useState` Hook, we would be caught in an infinite loop since this Hook itself causes a re-render.
            
            To avoid this, we can use the `useRef` Hook.
            
            # Example:
            
            Use `useRef` to track application renders.
            
            ```jsx
            import { useState, useEffect, useRef } from "react";
            import ReactDOM from "react-dom/client";
            
            function App() {
              const [inputValue, setInputValue] = useState("");
              const count = useRef(0);
            
              useEffect(() => {
                count.current = count.current + 1;
              });
            
              return (
                <>
                  <input
            
                    type="text"value={inputValue}onChange={(e) => setInputValue(e.target.value)}/>
                  <h1>Render Count: {count.current}</h1>
                </>);
            }
            
            const root = ReactDOM.createRoot(document.getElementById('root'));
            root.render(<App />);
            
            ```
            
            [Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_useref)
            
            `useRef()` only returns one item. It returns an Object called `current`.
            
            When we initialize `useRef` we set the initial value: `useRef(0)`.
            
            It's like doing this: `const count = {current: 0}`. We can access the count by using `count.current`.
            
            Run this on your computer and try typing in the input to see the application render count increase.
            
            ---
            
            [w3schoolsCERTIFIED.2022](https://shop.w3schools.com/collections/course-catalog)
            
            Complete the React modules, do the exercises, take the exam and become w3schools certified!!
            
            [$95 ENROLL](https://shop.w3schools.com/collections/course-catalog/products/react-js-course)
            
            ---
            
            # Accessing DOM Elements
            
            In general, we want to let React handle all DOM manipulation.
            
            But there are some instances where `useRef` can be used without causing issues.
            
            In React, we can add a `ref` attribute to an element to access it directly in the DOM.
            
            # Example:
            
            Use `useRef` to focus the input:
            
            ```jsx
            import { useRef } from "react";
            import ReactDOM from "react-dom/client";
            
            function App() {
              const inputElement = useRef();
            
              const focusInput = () => {
                inputElement.current.focus();
              };
            
              return (
                <>
                  <input type="text" ref={inputElement} />
                  <button onClick={focusInput}>Focus Input</button>
                </>);
            }
            
            const root = ReactDOM.createRoot(document.getElementById('root'));
            root.render(<App />);
            
            ```
            
            [Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_useref2)
            
            ---
            
            # Tracking State Changes
            
            The `useRef` Hook can also be used to keep track of previous state values.
            
            This is because we are able to persist `useRef` values between renders.
            
            # Example:
            
            Use `useRef` to keep track of previous state values:
            
            ```jsx
            import { useState, useEffect, useRef } from "react";
            import ReactDOM from "react-dom/client";
            
            function App() {
            	  const [inputValue, setInputValue] = useState("");
            	  const previousInputValue = useRef("");
            	
            	  useEffect(() => {
            	    previousInputValue.current = inputValue;
            	  }, [inputValue]);
            	
            	  return (
            	    <>
            	      <input
            	        type="text"value={inputValue}onChange={(e) => setInputValue(e.target.value)}/>
            	      <h2>Current Value: {inputValue}</h2>
            	      <h2>Previous Value: {previousInputValue.current}</h2>
            	    </>);
            }
            
            const root = ReactDOM.createRoot(document.getElementById('root'));
            root.render(<App />);
            
            ```
            
            [Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_useref3)
            
            This time we use a combination of `useState`, `useEffect`, and `useRef` to keep track of the previous state.
            
            In the `useEffect`, we are updating the `useRef` current value each time the `inputValue` is updated by entering text into the input field.


<br> 


## Q.7 useReducer, useCallback, useMemo, custom hooks
1. useReducer: 

The `useReducer` Hook is similar to the `useState` Hook.

It allows for custom state logic.

If you find yourself keeping track of multiple pieces of state that rely on complex logic, `useReducer` may be useful.

---

# Syntax

The useReducer Hook accepts two arguments.

useReducer(<reducer>, <initialState>)

The `reducer` function contains your custom state logic and the `initialState`can be a simple value but generally will contain an object.

The `useReducer` Hook returns the current `state`and a `dispatch`method.

Here is an example of `useReducer` in a counter app:

# Example:

```jsx
import { useReducer } from "react";
import ReactDOM from "react-dom/client";

const initialTodos = [
  {
    id: 1,
    title: "Todo 1",
    complete: false,
  },
  {
    id: 2,
    title: "Todo 2",
    complete: false,
  },
];

const reducer = (state, action) => {
  switch (action.type) {
    case "COMPLETE":
      return state.map((todo) => {
        if (todo.id === action.id) {
          return { ...todo, complete: !todo.complete };
        } else {
          return todo;
        }
      });
    default:
      return state;
  }
};

function Todos() {
  const [todos, dispatch] = useReducer(reducer, initialTodos);

  const handleComplete = (todo) => {
    dispatch({ type: "COMPLETE", id: todo.id });
  };

  return (
    <>
      {todos.map((todo) => (
        <div key={todo.id}>
          <label>
            <input
              type="checkbox"checked={todo.complete}onChange={() => handleComplete(todo)}/>
            {todo.title}
          </label>
        </div>))}
    </>);
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Todos />);

```

[Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_usereducer)

---

This is just the logic to keep track of the todo complete status.

All of the logic to add, delete, and complete a todo could be contained within a single `useReducer` Hook by adding more actions.

1. **useCallback:**
    
    The React `useCallback` Hook returns a memoized callback function.
    
    Think of memoization as caching a value so that it does not need to be recalculated.
    
    This allows us to isolate resource intensive functions so that they will not automatically run on every render.
    
    The `useCallback` Hook only runs when one of its dependencies update.
    
    This can improve performance.
    
    The `useCallback` and `useMemo` Hooks are similar. The main difference is that `useMemo` returns a memoized *value* and `useCallback` returns a memoized *function*. You can learn more about useMemo in the useMemo [chapter](https://www.w3schools.com/REACT/react_usememo.asp).
    
    ---
    
    # Problem
    
    One reason to use `useCallback` is to prevent a component from re-rendering unless its props have changed.
    
    In this example, you might think that the `Todos` component will not re-render unless the `todos` change:
    
    This is a similar example to the one in the [React.memo](https://www.w3schools.com/REACT/react_memo.asp) section.
    
    # Example:
    
    `index.js`
    
    ```jsx
    import { useState } from "react";
    import ReactDOM from "react-dom/client";
    import Todos from "./Todos";
    
    const App = () => {
      const [count, setCount] = useState(0);
      const [todos, setTodos] = useState([]);
    
      const increment = () => {
        setCount((c) => c + 1);
      };
      const addTodo = () => {
        setTodos((t) => [...t, "New Todo"]);
      };
    
      return (
        <>
          <Todos todos={todos} addTodo={addTodo} />
          <hr />
          <div>
            Count: {count}
            <button onClick={increment}>+</button>
          </div>
        </>);
    };
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<App />);
    
    ```
    
    `Todos.js`
    
    ```jsx
    import { memo } from "react";
    
    const Todos = ({ todos, addTodo }) => {
      console.log("child render");
      return (
        <>
          <h2>My Todos</h2>
          {todos.map((todo, index) => {
            return <p key={index}>{todo}</p>;
          })}
          <button onClick={addTodo}>Add Todo</button>
        </>);
    };
    
    export default memo(Todos);
    
    ```
    
    [Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_usecallback1)
    
    Try running this and click the count increment button.
    
    You will notice that the `Todos` component re-renders even when the `todos` do not change.
    
    Why does this not work? We are using `memo`, so the `Todos` component should not re-render since neither the `todos` state nor the `addTodo` function are changing when the count is incremented.
    
    This is because of something called "referential equality".
    
    Every time a component re-renders, its functions get recreated. Because of this, the `addTodo` function has actually changed.
    
    ---
    
    [w3schoolsCERTIFIED.2022](https://shop.w3schools.com/collections/course-catalog)
    
    # Get Certified!
    
    Complete the React modules, do the exercises, take the exam and become w3schools certified!!
    
    [$95 ENROLL](https://shop.w3schools.com/collections/course-catalog/products/react-js-course)
    
    ---
    
    # Solution
    
    To fix this, we can use the `useCallback` hook to prevent the function from being recreated unless necessary.
    
    Use the `useCallback` Hook to prevent the `Todos` component from re-rendering needlessly:
    
    # Example:
    
    `index.js`
    
    ```jsx
    import { useState, useCallback } from "react";
    import ReactDOM from "react-dom/client";
    import Todos from "./Todos";
    
    const App = () => {
      const [count, setCount] = useState(0);
      const [todos, setTodos] = useState([]);
    
      const increment = () => {
        setCount((c) => c + 1);
      };
      const addTodo = useCallback(() => {
        setTodos((t) => [...t, "New Todo"]);
      }, [todos]);
    
      return (
        <>
          <Todos todos={todos} addTodo={addTodo} />
          <hr />
          <div>
            Count: {count}
            <button onClick={increment}>+</button>
          </div>
        </>);
    };
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<App />);
    
    ```
    
    `Todos.js`
    
    ```jsx
    import { memo } from "react";
    
    const Todos = ({ todos, addTodo }) => {
      console.log("child render");
      return (
        <>
          <h2>My Todos</h2>
          {todos.map((todo, index) => {
            return <p key={index}>{todo}</p>;
          })}
          <button onClick={addTodo}>Add Todo</button>
        </>);
    };
    
    export default memo(Todos);
    ```
    
    1. **useMemo:** 
    
    The React `useMemo` Hook returns a memoized value.
    
    Think of memoization as caching a value so that it does not need to be recalculated.
    
    The `useMemo` Hook only runs when one of its dependencies update.
    
    This can improve performance.
    
    The `useMemo` and `useCallback` Hooks are similar. The main difference is that `useMemo` returns a memoized value and `useCallback` returns a memoized function. You can learn more about `useCallback` in the [useCallback chapter](https://www.w3schools.com/REACT/react_usecallback.asp).
    
    ---
    
    # Performance
    
    The `useMemo` Hook can be used to keep expensive, resource intensive functions from needlessly running.
    
    In this example, we have an expensive function that runs on every render.
    
    When changing the count or adding a todo, you will notice a delay in execution.
    
    # Example:
    
    A poor performing function. The `expensiveCalculation` function runs on every render:
    
    ```jsx
    import { useState } from "react";
    import ReactDOM from "react-dom/client";
    
    const App = () => {
      const [count, setCount] = useState(0);
      const [todos, setTodos] = useState([]);
      const calculation = expensiveCalculation(count);
    
      const increment = () => {
        setCount((c) => c + 1);
      };
      const addTodo = () => {
        setTodos((t) => [...t, "New Todo"]);
      };
    
      return (
        <div>
          <div>
            <h2>My Todos</h2>
            {todos.map((todo, index) => {
              return <p key={index}>{todo}</p>;
            })}
            <button onClick={addTodo}>Add Todo</button>
          </div>
          <hr />
          <div>
            Count: {count}
            <button onClick={increment}>+</button>
            <h2>Expensive Calculation</h2>
            {calculation}
          </div>
        </div>);
    };
    
    const expensiveCalculation = (num) => {
      console.log("Calculating...");
      for (let i = 0; i < 1000000000; i++) {
        num += 1;
      }
      return num;
    };
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<App />);
    
    ```
    
    ---
    
    ---
    
    # Use useMemo
    
    To fix this performance issue, we can use the `useMemo` Hook to memoize the `expensiveCalculation` function. This will cause the function to only run when needed.
    
    We can wrap the expensive function call with `useMemo`.
    
    The `useMemo`Hook accepts a second parameter to declare dependencies. The expensive function will only run when its dependencies have changed.
    
    In the following example, the expensive function will only run when `count` is changed and not when todo's are added.
    
    # Example:
    
    Performance example using the `useMemo` Hook:
    
    ```jsx
    import { useState, useMemo } from "react";
    import ReactDOM from "react-dom/client";
    
    const App = () => {
      const [count, setCount] = useState(0);
      const [todos, setTodos] = useState([]);
      const calculation = useMemo(() => expensiveCalculation(count), [count]);
    
      const increment = () => {
        setCount((c) => c + 1);
      };
      const addTodo = () => {
        setTodos((t) => [...t, "New Todo"]);
      };
    
      return (
        <div>
          <div>
            <h2>My Todos</h2>
            {todos.map((todo, index) => {
              return <p key={index}>{todo}</p>;
            })}
            <button onClick={addTodo}>Add Todo</button>
          </div>
          <hr />
          <div>
            Count: {count}
            <button onClick={increment}>+</button>
            <h2>Expensive Calculation</h2>
            {calculation}
          </div>
        </div>);
    };
    
    const expensiveCalculation = (num) => {
      console.log("Calculating...");
      for (let i = 0; i < 1000000000; i++) {
        num += 1;
      }
      return num;
    };
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<App />);
    ```
    
    1. custom hooks: 
    
    Hooks are reusable functions.
    
    When you have component logic that needs to be used by multiple components, we can extract that logic to a custom Hook.
    
    Custom Hooks start with "use". Example: `useFetch`.
    
    ---
    
    # Build a Hook
    
    In the following code, we are fetching data in our `Home` component and displaying it.
    
    We will use the [JSONPlaceholder](https://jsonplaceholder.typicode.com/) service to fetch fake data. This service is great for testing applications when there is no existing data.
    
    To learn more, check out the [JavaScript Fetch API](https://www.w3schools.com/js/js_api_fetch.asp) section.
    
    Use the JSONPlaceholder service to fetch fake "todo" items and display the titles on the page:
    
    # Example:
    
    `index.js`:
    
    ```jsx
    import { useState, useEffect } from "react";
    import ReactDOM from "react-dom/client";
    
    const Home = () => {
      const [data, setData] = useState(null);
    
      useEffect(() => {
        fetch("https://jsonplaceholder.typicode.com/todos")
          .then((res) => res.json())
          .then((data) => setData(data));
     }, []);
    
      return (
        <>
          {data &&
            data.map((item) => {
              return <p key={item.id}>{item.title}</p>;
            })}
        </>);
    };
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<Home />);
    
    ```
    
    [Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_customhook1)
    
    The fetch logic may be needed in other components as well, so we will extract that into a custom Hook.
    
    Move the fetch logic to a new file to be used as a custom Hook:
    
    # Example:
    
    `useFetch.js`:
    
    ```jsx
    import { useState, useEffect } from "react";
    
    const useFetch = (url) => {
      const [data, setData] = useState(null);
    
      useEffect(() => {
        fetch(url)
          .then((res) => res.json())
          .then((data) => setData(data));
      }, [url]);
    
      return [data];
    };
    
    export default useFetch;
    
    ```
    
    `index.js`:
    
    ```jsx
    import ReactDOM from "react-dom/client";
    import useFetch from "./useFetch";
    
    const Home = () => {
      const [data] = useFetch("https://jsonplaceholder.typicode.com/todos");
    
      return (
        <>
          {data &&
            data.map((item) => {
              return <p key={item.id}>{item.title}</p>;
            })}
        </>);
    };
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<Home />);
    
    ```
    
    [Run Example »](https://www.w3schools.com/REACT/showreact.asp?filename=demo2_react_customhook2)
    
    ---
    
    # Example Explained
    
    We have created a new file called `useFetch.js` containing a function called `useFetch` which contains all of the logic needed to fetch our data.
    
    We removed the hard-coded URL and replaced it with a `url` variable that can be passed to the custom Hook.
    
    Lastly, we are returning our data from our Hook.
    
    In `index.js`, we are importing our `useFetch` Hook and utilizing it like any other Hook. This is where we pass in the URL to fetch data from.
    
    Now we can reuse this custom Hook in any component to fetch data from any URL.



   <br> 


   ## Q.8 ES6 FEATURES
   ## WHAT IS ECMASCRIPT?

ECMAScript, also known as JavaScript, is a programming language adopted by the European Computer Manufacturer's Association as a standard for performing computations in Web applications. ECMAScript is the official client-side scripting language of VoiceXML. ECMAScript is a limited programming model for simple data manipulation.

# New Features in ES6

- [The let keyword](https://www.w3schools.com/js/js_es6.asp#mark_let)
- [The const keyword](https://www.w3schools.com/js/js_es6.asp#mark_const)
- [Arrow Functions](https://www.w3schools.com/js/js_es6.asp#mark_arrow)
- [The ... Operator](https://www.w3schools.com/js/js_es6.asp#mark_spread)
- [For/of](https://www.w3schools.com/js/js_es6.asp#mark_forof)
- [Map Objects](https://www.w3schools.com/js/js_es6.asp#mark_map)
- [Set Objects](https://www.w3schools.com/js/js_es6.asp#mark_set)
- [Classes](https://www.w3schools.com/js/js_es6.asp#mark_class)
- [Promises](https://www.w3schools.com/js/js_es6.asp#mark_promise)
- [Symbol](https://www.w3schools.com/js/js_es6.asp#mark_symbol)
- [Default Parameters](https://www.w3schools.com/js/js_es6.asp#mark_param)
- [Function Rest Parameter](https://www.w3schools.com/js/js_es6.asp#mark_rest)
- [String.includes()](https://www.w3schools.com/js/js_es6.asp#mark_includes)
- [String.startsWith()](https://www.w3schools.com/js/js_es6.asp#mark_startswith)
- [String.endsWith()](https://www.w3schools.com/js/js_es6.asp#mark_endswith)
- [Array.from()](https://www.w3schools.com/js/js_es6.asp#mark_array_from)
- [Array keys()](https://www.w3schools.com/js/js_es6.asp#mark_array_keys)
- [Array find()](https://www.w3schools.com/js/js_es6.asp#mark_array_find)
- [Array findIndex()](https://www.w3schools.com/js/js_es6.asp#mark_array_findIndex)
- [New Math Methods](https://www.w3schools.com/js/js_es6.asp#mark_math_methods)
- [New Number Properties](https://www.w3schools.com/js/js_es6.asp#mark_number_properties)
- [New Number Methods](https://www.w3schools.com/js/js_es6.asp#mark_number_methods)
- [New Global Methods](https://www.w3schools.com/js/js_es6.asp#mark_global_methods)
- [Object entries](https://www.w3schools.com/js/js_es6.asp#mark_entries)
- [JavaScript Modules](https://www.w3schools.com/js/js_es6.asp#mark_modules)


<br> 


## Q.9 Redux
Three core concepts : 

1. Store: 
    
    Holds the state of your application.
    

1. action: 
    
    describes the changes in the state of the application.
    

1. reducer: 
    
    A reducer which actually carries out the state transition depending on the action.
    
    e.g. 
    
    cake shop scenario                                        Redux                                                  Purpose
    
      Shop                                                               Store                                               Holds the state of your application
    
     Intention to buy cake                                        Action                                              Describes what happened
    
      Shopkeeper                                                     Reducer                                          Ties the store and action together 
    
    There are three main components of Redux architecture.
    
    **STORE:**
    
    The entire state of an application lists at a place called Store. It acts as a brain and manages the status of the application. It also has a dispatch(action) function.
    
    **ACTION:**
    
    An action is a pure object which is sent or dispatched from the view. It is created to store information about the user’s event such as info about the type of action, the time of occurrence, the location of occurrence, info about its coordinates, and info about the state it aims to change.
    
    **REDUCER:**
    
    Reducer is a pure function which is used to return a new state from the initial state. It reads the payloads from the actions. The reducer then updates the store via the state accordingly.
    
    Explaining Redux in a React interview requires breaking down the key concepts and highlighting how it solves specific problems in managing state in a React application. Here's a concise way to explain Redux:
    
    1. **State Management in React:**
        - Start by explaining that React components have local state, which is suitable for managing component-specific data.
        - However, when an application grows, passing state between components (especially deeply nested ones) can become complex and lead to "prop drilling."
    2. **The Need for Redux:**
        - Introduce the problem of "prop drilling" and how it can make the code harder to maintain and understand.
        - Mention that Redux provides a centralized state management solution, making it easier to manage and share state across the application.
    3. **Key Concepts:**
        - **Store:** Explain that Redux introduces a single source of truth called the "store," which holds the entire state of the application.
        - **Actions:** Discuss that changes to the state are triggered by "actions" – plain JavaScript objects with a `type` property that describes the action.
        - **Reducers:** Describe that "reducers" are pure functions that take the current state and an action, and return a new state.
    4. **Flow of Data:**
        - Elaborate on how the flow of data works in Redux: Components dispatch actions, which are processed by reducers, resulting in a new state stored in the central store.
        - Mention that components can subscribe to changes in the store, and when the state changes, React re-renders the subscribed components.
    5. **Immutable State:**
        - Emphasize the importance of immutability in Redux. Explain that state should not be mutated directly, but instead, a new state object should be created.
    6. **Middleware:**
        - Briefly mention middleware, explaining that it allows you to extend Redux's capabilities. Common middleware includes logging, handling asynchronous actions, etc.
    7. **React-Redux:**
        - Talk about the `react-redux` library, which provides a set of helper functions to connect the React components with the Redux store. Mention `Provider` for making the store available to all components, and `connect` for connecting components to the store.
    8. **Use Cases:**
        - Provide examples of scenarios where Redux shines, such as managing complex state, handling asynchronous operations, or when state needs to be shared among various components.
    9. **Drawbacks:**
        - Be honest about Redux's drawbacks, such as increased boilerplate code and potential complexity for smaller applications. Emphasize that it's beneficial for larger, more complex projects.
    
    Remember to adapt your explanation based on your interviewer's level of familiarity with Redux and React. It's essential to strike a balance between providing enough detail and avoiding unnecessary complexity.


   <br> 


## Q.10 prop drilling
Prop drilling is basically a situation when the same data is being sent at almost every level due to requirements in the final level. Here is a diagram to demonstrate it better. Data needed to be sent from *Parent* to *ChildC.* 

              Parent 
              Parent A
              Parent B
              Child
              


<br> 

## Q.11 Redux api calling 
# store.js

```jsx
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../counter/counterSlice";
export default configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

# counterSlice.js

```jsx
import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";
import axios from "axios";
export const fetchDataAsync = createAsyncThunk(
  "counter/fetchData",
  async (apiEndpoint) => {
    try {
      const response = await axios.get(apiEndpoint);
      return response.data; // Assuming the API response has a 'data' property
    } catch (error) {
      // Handle error cases if needed
      console.error("Error fetching data:", error);
      throw error;
    }
  }
);
export const counterSlice = createSlice({
  name: "counter",
  initialState: {
    value: 0,
  },
  reducers: {
    increament: (state) => {
      state.value += 1;
    },
    decreament: (state) => {
      state.value -= 1;
    },
    increamentByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchDataAsync.pending, (state) => {
        state.status = "loading";
      })
      .addCase(fetchDataAsync.fulfilled, (state, action) => {
        state.status = "succeeded";
        state.data = action.payload;
      })
      .addCase(fetchDataAsync.rejected, (state, action) => {
        state.status = "failed";
        state.error = action.error.message;
      });
  },
});

export const { increament, decreament, increamentByAmount } =
  counterSlice.actions;
export default counterSlice.reducer;
```

# First.js

```jsx
import React, { useEffect } from "react";
import { useDispatch, useSelector } from "react-redux";
import {
  fetchDataAsync,
  increament,
  decreament,
  increamentByAmount,
} from "./counter/counterSlice";

const First = () => {
  const dispatch = useDispatch();
  const data = useSelector((state) => state.counter.data);
  const status = useSelector((state) => state.counter.status);
  const error = useSelector((state) => state.counter.error);
  const counter = useSelector((state) => state.counter.value);

  useEffect(() => {
    // Example dispatch to fetch data
    dispatch(fetchDataAsync("https://fakestoreapi.com/products"));
  }, [dispatch]);

  if (status === "loading") {
    return <div>Loading...</div>;
  }

  if (status === "failed") {
    return <div>Error: {error}</div>;
  }
  console.log(data);

  return (
    <div>
      <button onClick={() => dispatch(increament())}>+</button>
      <span>{counter}</span>
      <button onClick={() => dispatch(decreament())}>-</button>
      <button onClick={() => dispatch(increamentByAmount(5))}>+5</button>
    </div>
  );
};

export default First;
```

# App.js

```jsx
import logo from "./logo.svg";
import "./App.css";
import { Provider } from "react-redux";
import store from "./components/store/store";
import First from "./components/First";
function App() {
  return (
    <Provider store={store}>
      <First />
    </Provider>
  );
}

export default App;
```


<br> 


## Q.13 OTP input boxes
```jsx
import { useState, useRef, useEffect } from "react";

import "./App.css";

function App() {
  const inputRef = useRef([]);
  const [otp, setOtp] = useState(["", "", "", ""]);

  const handleChange = (e, index) => {
    let value = e.target.value;
    if (/^\d+$/.test(value) || value === "") {
      value = e.target.value[e.target.value.length - 1];
      setOtp(otp?.map((o, i) => (i === index ? value : o)));
    }

    // move to next field if current field is filled
    if (value && index < otp.length - 1 && inputRef.current[index + 1]) {
      inputRef.current[index + 1].focus();
    }
  };
  const handleClick = (index) => {
    // moving cursor end of the input
    inputRef.current[index].setSelectionRange(1, 1);
  };
  const handleKeyDown = (e, index) => {
    if (
      e.key === "Backspace" &&
      !otp[index] &&
      index > 0 &&
      inputRef.current[index - 1]
    ) {
      inputRef.current[index - 1].focus();
    }
  };
  useEffect(() => {
    if (inputRef.current[0]) {
      inputRef.current[0].focus();
    }
  }, []);

  return (
    <>
      <div>
        {otp?.map((value, index) => (
          <input
            ref={(input) => (inputRef.current[index] = input)}
            className="otpInput"
            value={value}
            onClick={() => handleClick(index)}
            onChange={(e) => handleChange(e, index)}
            onKeyDown={(e) => handleKeyDown(e, index)}
          />
        ))}
      </div>
    </>
  );
}

export default App;
```


<br> 

## Q.14 VIRTUAL DOM REACT JS 

React JS Virtual DOM is an in-memory representation of the DOM. DOM refers to the Document Object Model that represents the content of XML or HTML documents as a tree structure so that the programs can be read, accessed and changed in the document structure, style, and content.

Table of Content

- **[Prerequisites](https://www.geeksforgeeks.org/reactjs-virtual-dom/#prerequisites)**
- **[What is DOM ?](https://www.geeksforgeeks.org/reactjs-virtual-dom/#what-is-dom-)**
- **[Disadvantages of real DOM](https://www.geeksforgeeks.org/reactjs-virtual-dom/#disadvantages-of-real-dom-)**
- **[Virtual DOM](https://www.geeksforgeeks.org/reactjs-virtual-dom/#virtual-dom)**
- **[How does virtual DOM actually make things faster?](https://www.geeksforgeeks.org/reactjs-virtual-dom/#how-does-virtual-dom-actually-make-things-faster)**
- **[How virtual DOM Helps React?](https://www.geeksforgeeks.org/reactjs-virtual-dom/#how-virtual-dom-helps-react)**
- **[Virtual DOM Key Concepts](https://www.geeksforgeeks.org/reactjs-virtual-dom/#virtual-dom-key-concepts-)**
- **[Differences between Virtual DOM and Real DOM](https://www.geeksforgeeks.org/reactjs-virtual-dom/#differences-between-virtual-dom-and-real-dom)**

# What is DOM ?

DOM stands for ‘Document Object Model’. In simple terms, it is a structured representation of the HTML elements that are present in a webpage or web app. DOM represents the entire UI of your application. The DOM is represented as a tree data structure. It contains a node for each UI element present in the web document. It is very useful as it allows web developers to modify content through JavaScript, also it being in structured format helps a lot as we can choose specific targets and all the code becomes much easier to work with.

# Disadvantages of real DOM :

Every time the DOM gets updated, the updated element and its children have to be rendered again to update the UI of our page. For this, each time there is a component update, the DOM needs to be updated and the UI components have to be re-rendered.

**Example:**

```jsx
// Simple getElementById() method
document.getElementById('some-id').innerValue = 'updated value';
```

When writing the above code in the console or in the JavaScript file, these things happen:

- The browser parses the HTML to find the node with this id.
- It removes the child element of this specific element.
- Updates the element(DOM) with the ‘updated value’.
- Recalculates the CSS for the parent and child nodes.
- Update the layout.
- Finally, traverse the tree and paint it on the screen(browser) display.

Recalculating the CSS and changing the layouts involves complex algorithms, and they do affect the performance. So React has a different approach to dealing with this, as it makes use of something known as Virtual DOM.

# Virtual DOM

React uses Virtual DOM exists which is like a lightweight copy of the actual DOM(a virtual representation of the DOM). So for every object that exists in the original DOM, there is an object for that in React Virtual DOM. It is exactly the same, but it does not have the power to directly change the layout of the document.

**Manipulating DOM is slow, but manipulating Virtual DOM is fast** as nothing gets drawn on the screen. So each time there is a change in the state of our application, the virtual DOM gets updated first instead of the real DOM.

# How does virtual DOM actually make things faster?

When anything new is added to the application, a virtual DOM is created and it is represented as a tree. Each element in the application is a node in this tree. So, whenever there is a change in the state of any element, a new Virtual DOM tree is created. This new Virtual DOM tree is then compared with the previous Virtual DOM tree and make a note of the changes. After this, it finds the best possible ways to make these changes to the real DOM. Now only the updated elements will get rendered on the page again.

# How virtual DOM Helps React?

In React, everything is treated as a component be it a **[functional component](https://www.geeksforgeeks.org/reactjs-functional-components/)** or **[class component.](https://www.geeksforgeeks.org/reactjs-class-based-components/)** A component can contain a state. Whenever the state of any component is changed react updates its Virtual DOM tree. Though it may sound like it is ineffective the cost is not much significant as updating the virtual DOM doesn’t take much time.

React maintains two Virtual DOM at each time, one contains the updated Virtual DOM and one which is just the pre-update version of this updated Virtual DOM. Now it compares the pre-update version with the updated Virtual DOM and figures out what exactly has changed in the DOM like which components have been changed. **This process of comparing the current Virtual DOM tree with the previous one is known as [‘diffing’](https://www.geeksforgeeks.org/explain-dom-diffing/).** Once React finds out what exactly has changed then it updates those objects only, on real DOM.

React uses something called batch updates to update the real DOM. It just means that the changes to the real DOM are sent in batches instead of sending any update for a single change in the state of a component.

**We have seen that the re-rendering of the UI is the most expensive part and React manages to do this most efficiently by ensuring that the Real DOM receives batch updates to re-render the UI. This entire process of transforming changes to the real DOM is called [Reconciliation](https://www.geeksforgeeks.org/reactjs-reconciliation/).**

This significantly improves the performance and is the main reason why React and its Virtual DOM are much loved by developers all around.

The diagrammatic image below briefly describes how the virtual DOM works in the real browser environment

!https://media.geeksforgeeks.org/wp-content/uploads/20230725135348/Browser-DOM-Virtual-DOM-copy.webp

*Real DOM to Virtual DOM*

# Virtual DOM Key Concepts :

- Virtual DOM is the virtual representation of Real DOM
- React update the state changes in Virtual DOM first and then it syncs with Real DOM
- Virtual DOM is just like a blueprint of a machine, can do changes in the blueprint but those changes will not directly apply to the machine.
- Virtual DOM is a programming concept where a virtual representation of a UI is kept in memory synced with “Real DOM ” by a library such as ReactDOM and this process is called reconciliation
- Virtual DOM makes the performance faster, not because the processing itself is done in less time. The reason is the amount of changed information – rather than wasting time on updating the entire page, you can dissect it into small elements and interactions
# Differences between Virtual DOM and Real DOM

| Virtual DOM | Real DOM |
| --- | --- |
| It is a lightweight copy of the original DOM | It is a tree representation of HTML elements |
| It is maintained by JavaScript libraries | It is maintained by the browser after parsing HTML elements |
| After manipulation it only re-renders changed elements | After manipulation, it re-render the entire DOM |
| Updates are lightweight | Updates are heavyweight |
| Performance is fast and UX is optimised | Performance is slow and the UX quality is low |
| Highly efficient as it performs batch updates | Less efficient due to re-rendering of DOM after each update |



<br> 


## Q.15 WHAT IS JSX? 
JSX stands for JavaScript XML, and it is a syntax extension for JavaScript commonly used with React. JSX allows developers to write XML or HTML-like code within JavaScript, making it more expressive and concise when defining React components.

Here are some key points about JSX:

1. **HTML-like Syntax:** JSX looks similar to HTML or XML, which makes it easier for developers to write and understand the structure of the UI within JavaScript code.
2. **Expressive Syntax:** JSX allows you to express UI components more declaratively. Instead of using JavaScript functions to manipulate the DOM directly, you can write JSX to describe what the UI should look like based on the current state.
3. **Embedding JavaScript Expressions:** JSX allows you to embed JavaScript expressions within curly braces **`{}`**. This feature allows you to dynamically compute values, use variables, and execute functions within the JSX code.
    
    ```jsx
    
    const name = "John";
    const element = <p>Hello, {name}!</p>;
    
    ```
    
4. **Babel Compilation:** JSX code is not directly understood by browsers. It needs to be transpiled into regular JavaScript using tools like Babel before it can be executed in a web browser.
5. **Integration with React:** React components are often written using JSX. JSX is a syntactic sugar over **`React.createElement()`** calls, making it more readable and concise.
    
    ```jsx
    jsxCopy code
    // JSX
    const element = <h1>Hello, React!</h1>;
    
    // Equivalent using React.createElement()
    const element = React.createElement('h1', null, 'Hello, React!');
    
    ```
    
6. **Component Composition:** JSX facilitates the composition of React components, allowing developers to create complex UI structures by combining and nesting components.

JSX is not required when working with React, but it has become a standard practice in the React ecosystem due to its readability and expressiveness. It simplifies the process of building and maintaining UI components in React applications.


<br> 

## Q.16 what is virtual dom and how it is used by reactjs
The Virtual DOM (Document Object Model) is a concept used by React to improve the efficiency of updating the user interface (UI) in web applications. It is a lightweight, in-memory representation of the actual DOM elements. React utilizes the Virtual DOM as an intermediary step in the process of updating the UI, making the application more efficient and responsive.

Here's how the Virtual DOM works in React:

1. **Initial Render:**
    - When a React component is first rendered or updated, it creates a virtual representation of the DOM hierarchy, known as the Virtual DOM.
2. **Virtual DOM Tree:**
    - The Virtual DOM is essentially a JavaScript object that mirrors the structure of the actual DOM but is stored in memory. Each DOM element is represented by a corresponding virtual element with properties like type, attributes, and children.
3. **Component Rendering:**
    - React components are responsible for generating the Virtual DOM elements. When a component's state or props change, a new Virtual DOM tree is created.
4. **Diffing Algorithm:**
    - Before updating the actual DOM, React performs a process called reconciliation or diffing. It compares the new Virtual DOM tree with the previous one to identify the differences (changes) between them.
5. **Minimizing DOM Operations:**
    - React identifies the minimum number of changes needed to update the actual DOM based on the differences found during the reconciliation process. This is a crucial step to optimize performance.
6. **Updating the Real DOM:**
    - Once React determines the minimal set of changes required, it updates the actual DOM to reflect these changes. This operation is more efficient than directly manipulating the entire DOM, as it targets only the specific elements that need to be updated.
7. **Batching Updates:**
    - React often batches multiple updates together to minimize the number of interactions with the actual DOM. This batching process helps to avoid unnecessary reflows and repaints, resulting in improved performance.

The use of the Virtual DOM allows React to achieve several advantages:

- **Performance Optimization:** By minimizing direct DOM manipulations and efficiently updating only the necessary parts, React reduces the performance overhead associated with frequent DOM operations.
- **Consistent API:** The Virtual DOM provides a consistent and predictable API for working with UI updates in a component-based architecture, simplifying the development process.
- **Enhanced Developer Experience:** Developers can work with a declarative programming model, describing what the UI should look like in different states, while React takes care of the efficient updates through the Virtual DOM.


<br> 


## Q.17 CONTROLLED AND UNCONTROLLED COMPONENTS IN REACTJS
# Controlled components:

Controlled components in React are a powerful tool, acting as components where React is responsible for managing and controlling the data (or state). This approach guarantees that there’s a single source of truth for the data, ensuring uniformity across the application.

### **What is a Controlled Component?**

In essence, a controlled component is one where the data, typically input form data, is handled by the React state mechanism. Rather than allowing the DOM to manage this data, React takes charge, ensuring that data handling and changes are consistent with the React paradigm.

### **How Controlled Components Work**

The underlying principles of controlled components are simple yet powerful:

- **Using `state` to store form values**: Every time a user interacts with a form element, like typing into an input field, the value is stored in the component’s local state.
- **Using `setState` or the `useState` hook**: To update the stored values in the state, one would traditionally use the **`setState`** method in class components. With the introduction of React hooks, the **`useState`** hook provides a more concise way to manage state in functional components.
- **Passing state as props to child components**: This allows child components to receive and display the data, ensuring a single source of truth and a consistent data flow.

### **Examples of Controlled Components**

Let’s delve into a few examples:

- **Controlled input text field**:
    
    ```jsx
    function TextInput() {
      const [text, setText] = useState("");
    
      return (
        <input type="text" value={text} onChange={(e) => setText(e.target.value)} />
      );
    }
    ```
    
- **Controlled checkbox**:

```jsx
function CheckBox() {
  const [checked, setChecked] = useState(false);

  return (
    <input
      type="checkbox"
      checked={checked}
      onChange={() => setChecked(!checked)}
    />
  );
}
```

## **Benefits of Controlled Components**

Adopting controlled components in your React projects brings with it a plethora of advantages:

### **Predictable Data Flow**

With controlled components, data flow is consistent and reliable. Since React maintains control over form values and their updates, there’s minimal chance for unexpected behaviors or discrepancies in data representation.

### **Integration with State Management Libraries**

Controlled components play nicely with popular state management libraries, such as **[Redux](https://redux.js.org/)**. This seamless integration ensures that application-wide state management is more intuitive and effective, allowing developers to handle complex data manipulations efficiently.

### **Enhanced Data Manipulation**

Before updating the state, developers have the luxury to intercept and manipulate the data. This means validation, formatting, or any other data transformation can be done to ensure the integrity and correctness of the data being stored.

### **User Feedback**

Controlled components, especially in forms, can offer immediate feedback to users. Whether it’s showing an error when a user types in an invalid email or displaying a character count for a text area, controlled components allow for dynamic and interactive user experiences that enhance overall usability.

# UnControlled components:

An uncontrolled component in React is one that stores its own state internally and does not control its value through the React state mechanism. Instead of being managed by React’s state system, it relies directly on the DOM to provide its current value.

### **How Uncontrolled Components Work**

Uncontrolled components have a few defining characteristics:

- **Using `ref` to get values directly from the DOM:** Instead of using an event handler to read the input’s value, you can obtain the value directly through **`ref`**.
- **Reduced reliance on React’s state:** Since these components don’t synchronize their state with React’s state mechanism, they might feel more familiar to developers who’ve worked with vanilla JavaScript.

### **Examples of Uncontrolled Components**

1. **Uncontrolled input text field using `ref`:**

```jsx
import React from "react";

const UncontrolledInput = () => {
  // Ref to store the input DOM reference
  const inputRef = React.useRef(null);

  // Function to handle the button click event
  const handleClick = () => {
    // Access the input value using the ref
    alert("Input Value: " + inputRef.current.value);
  };

  return (
    <div>
      {/* Uncontrolled input with ref */}
      <input type="text" ref={inputRef} placeholder="Type something..." />
      <button onClick={handleClick}>Get Input Value</button>
    </div>
  );
};

export default UncontrolledInput;
```

1. **Uncontrolled checkbox:**

```jsx
import React from "react";

const UncontrolledCheckbox = () => {
  // Ref to store the checkbox DOM reference
  const checkboxRef = React.useRef(null);

  // Function to handle the checkbox change event
  const handleCheckboxChange = () => {
    // Access the checkbox state using the ref
    console.log("Checkbox checked:", checkboxRef.current.checked);
  };

  return (
    <div>
      {/* Uncontrolled checkbox with ref */}
      <input
        type="checkbox"
        ref={checkboxRef}
        onChange={handleCheckboxChange}
      />
      <label>Uncontrolled Checkbox</label>
    </div>
  );
};

export default UncontrolledCheckbox;
```

## **Benefits of Uncontrolled Components**

### **Simplicity and Quick Prototyping**

For smaller projects or forms where state management might be overkill, uncontrolled components can be faster to implement. You can avoid setting up state and event handlers for every input, streamlining the development process.

### **Reduced React Re-renders**

Each time a controlled component’s value changes, it triggers a re-render in React. While this is often optimized and isn’t a concern, in some high-frequency update scenarios, uncontrolled components can offer performance advantages since they don’t tie into React’s re-render mechanism for every value change.

### **Traditional HTML Form Behavior**

For developers transitioning from vanilla JavaScript, uncontrolled components might feel more intuitive. They behave more like traditional HTML form elements.

## **When to use Controlled vs. Uncontrolled Components**

### **Project Size and Complexity**

For smaller projects with a few inputs, uncontrolled components can be more straightforward. But as projects grow and require more interactivity and data sharing among components, controlled components become more beneficial.

### **Data Validation Requirements**

Controlled components can offer more fine-grained control over input validation. If real-time validation or feedback is a requirement, controlled components are typically more suited.

### **State Management Preferences**

If you’re comfortable with React’s state and prefer a single source of truth for form values, controlled components are the way to go. But if you want a more direct approach that’s closer to traditional HTML, uncontrolled components have their merits.

### **Performance Considerations**

While uncontrolled components might lead to fewer re-renders in specific scenarios, controlled components, when used correctly, are optimized and shouldn’t pose performance issues for most use cases.


<br> 

## Q.18 WHY REACT USES SINGLE WAY DATA BINDING? 
React is often associated with one-way data binding because of its unidirectional data flow architecture. In React, data flows in a single direction, from parent components to child components. This means that changes in the parent component's state can propagate down to its child components, but the child components cannot directly modify the state of their parent components.

<br> 



## Q.19 WHAT IS BABEL?
When it comes to React, Babel is used to transpile modern JavaScript syntax into code that can run in all environments when writing React components. This allows developers to use the latest language features when writing React components and ensures compatibility with older browsers.

**Babel** in react is a crucial tool for React developers because it allows them to write code using the latest syntax and features while still ensuring that their code is compatible with all environments. This is particularly important because not all browsers support the latest JavaScript syntax, which could cause compatibility issues if developers tried to write React components using the latest syntax.

NOTE:  

it converts the JSX to Javascript.


<br> 


## Q.20 HIGHER ORDER COMPONENTS IN REACT
Higher-order components (HOCs) are a powerful feature of the React library. They allow you to reuse component logic across multiple components.

In React, a higher-order component is a function that takes a component as an argument and returns a new component that wraps the original component.

HOCs allow you to add additional functionality to a component without modifying the component's code. For example, you can use a HOC to add authentication or routing capabilities to a component or to apply a specific style or behavior to multiple components.

E.G. 

```jsx
import logo from "./logo.svg";
import "./App.css";
import { useState } from "react";

function App() {
  return (
    <div className="App">
      <HOCRed comp={Counter} />
      <HOCGreen comp={Counter} />
    </div>
  );
}

function HOCRed(props) {
  return (
    <h2 style={{ backgroundColor: "red" }}>
      <props.comp />
    </h2>
  );
}
function HOCGreen(props) {
  return (
    <h2 style={{ backgroundColor: "green" }}>
      <props.comp />
    </h2>
  );
}

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <span>{count}</span>
      <br />
      <button onClick={() => setCount(count + 1)}>Update</button>
    </div>
  );
}

export default App;

NOTE : 
	here we changed the background style of the 
```


<br> 



## Q.21 PRIVATE ROUTES IN REACT JS
**In React.js, private routes are routes that require authentication or authorization before allowing a user to access certain pages or components within a web application. These routes are typically used in applications where certain content or functionality should only be accessible to authenticated users.**

Here's a basic example of how private routes can be implemented in React.js using React Router:

```jsx
import React from 'react';
import { Route, Redirect } from 'react-router-dom';

const PrivateRoute = ({ component: Component, isAuthenticated, ...rest }) => (
  <Route
    {...rest}
    render={props =>
      isAuthenticated ? (
        <Component {...props} />
      ) : (
        <Redirect to={{ pathname: '/login', state: { from: props.location } }} />
      )
    }
  />
);

export default PrivateRoute;

```

In this example:

- `PrivateRoute` is a custom component that takes props such as `component`, `isAuthenticated`, and `rest` (which includes any additional props passed to it).
- It uses the `Route` component from `react-router-dom` to define a route.
- The `render` prop of `Route` is used to conditionally render either the specified component if the user is authenticated or redirect the user to the login page if they are not authenticated.
- The `isAuthenticated` prop is typically provided by a higher-level component, such as the one managing user authentication state.
- If the user is not authenticated, they are redirected to the login page. The `from` prop in the `Redirect` component is used to remember the original location the user attempted to access, so they can be redirected back after successful authentication.

Private routes are an essential part of building secure web applications, ensuring that sensitive content or functionality is only accessible to authorized users.



## Q.22 zustand library 

## Used to manage the states, as like react redux

```jsx
import React from "react";
import { create } from "zustand";
const useStore = create((set) => ({
  count: 0,
  incCount: () => set((state) => ({ count: (state.count += 1) })),
}));
function Counter() {
  const { count, incCount } = useStore();
  return (
    <div>
      {count} <button onClick={() => incCount()}>inc</button>
    </div>
  );
}

export default Counter;

```


<br> 

## Q.23 Why we cant use useref instead Usestate in reactjs
In React, `useState` and `useRef` serve different purposes. 
`useState` is used to manage state in functional components, allowing them to re-render when the state changes. It returns an array with the current state value and a function to update it.
On the other hand, `useRef` is primarily used to persist values across renders without triggering re-renders. It returns a mutable object (`{ current: ... }`) which can hold a value that persists between renders, but changing the value doesn't trigger a re-render.
So, if you want to manage and update state that triggers re-renders, you use `useState`. If you need to persist a value without causing re-renders, you use `useRef`. They have distinct use cases and are not interchangeable.


<br> 

## Q.24 which one is better to use. usecontext or redux
### **When to Use Which:**

- **Small to Medium-sized Apps:**
    - For smaller apps with relatively simple state management needs, **`useContext`** may be sufficient.
- **Medium to Large-sized Apps:**
    - For larger applications with complex state requirements, multiple components needing access to global state, and a need for predictability and debugging tools, Redux might be a better choice.
- **Mixed Approach:**
    - In some cases, a combination of both can be used. Use **`useContext`** for local state within components and Redux for managing global state that needs to be shared across different parts of the application.

Ultimately, the decision depends on your specific use case and the scale of your application. Consider the complexity of your state management requirements and choose the solution that best fits your needs.


<br> 


## Q.25 In react keys must be needs to be unique in? 
**Keys Must Only Be Unique Among Siblings**

**Keys used within arrays should be unique among their siblings**

. However, they don't need to be globally unique. In conclusion, since they are siblings (disregarding component type), each key prop should be unique.


<br> 


## Q.26 WHAT IS REACT.FRAGMENT? 
## **What is React Fragment?[](https://refine.dev/blog/how-react-fragments-is-works/#what-is-react-fragment)**

React Fragment is a feature in React that allows you to return multiple elements from a React component by allowing you to group a list of children without adding extra nodes to the DOM.

To return multiple elements from a React component, you'll need to wrap the element in a root element. This approach has not been efficient and may cause issues in some cases. Eg.

```jsx
function TableData() {
  return (
    <div>
      {' '}
      <td>Eat</td> <td>Learn</td> <td>Code</td>{' '}
    </div>
  );
}
function Table() {
  return (
    <table>
      {' '}
      <tr>
        {' '}
        <TableData />{' '}
      </tr>{' '}
    </table>
  );
}

```

The above code will produce the HTML equivalent below.

`<table>  <tr>    <div>       <td>Eat</td>      <td>Learn</td>      <td>Code</td>    </div>  </tr></table>`

So as you can see that wrapping the `<td>` tags in a `div` element breaks the table parent-child relationship. For things to work as expected, the `<td>` tags have to be rendered individually without wrapping them in a `div` element. In scenarios like this, it's better to use React Fragment.

## **React Fragment vs Div Element[](https://refine.dev/blog/how-react-fragments-is-works/#react-fragment-vs-div-element)**

In React, "Fragment" and "Div" are used interchangeably. The main difference between the two is that "Fragment" clears out all extra divs from a DOM tree while "Div" adds a div to the DOM tree.

With React Fragments, we can create code that is cleaner and easier to read. It renders components more quickly and uses less memory. Every element is rendered as intended. While Div expands the DOM due to the long nested nodes that occur when there are too many HTML tags on your website.

The `div` element has more methods and properties, which causes it to consume more memory which can make the page slow load time; the prototype chain is like HTMLDivElement -> HTMLElement -> Element -> Node -> EventTarget, whereas the React fragment has fewer methods with the prototype chain DocumentFragment -> Node -> EventTarget.

Using fragments, you can reuse parts of your application. But, like in the table example we used in the previous section, div makes it challenging to do so. However, there are situations where using div instead of a fragment is necessary.

For instance, utilizing fragments does not allow you to design a component since you must wrap the target elements in a div. Additionally, you must use a div if you are adding keys to the components' elements. In light of this, you can use the two interchangeably depending on what you want your React application to accomplish.

## **Problem with using div[](https://refine.dev/blog/how-react-fragments-is-works/#problem-with-using-div)**

Let's look at some of the problems in using div in detail.

- The div element expands the HTML DOM, causing the browser to consume more resources than expected.
- When the DOM is too large, it consumes a lot of memory, causing the pages to load slowly in the browser.
- Debugging and tracing the origin of the extra nodes becomes more difficult as the DOM grows larger and more nested.
- Using div to render components may cause performance issues by clogging your HTML.

## **Advantages of Fragment[](https://refine.dev/blog/how-react-fragments-is-works/#advantages-of-fragment)**

React Fragment replaces the `<div>` element, which can cause issues with invalid HTML, with the following advantages.

- The code readability of React Fragment is higher.
- Because React fragments have a smaller DOM, they render faster and use less memory.
- React Fragment allows React components to be rendered as intended without causing any parent-child relationship issues.
- Fragments allow the return of multiple JSX elements, which addresses the issue of invalid HTML markups within react applications that were caused by the must-have constraint of only one element returning per component.

## **Using the key prop with React fragments[](https://refine.dev/blog/how-react-fragments-is-works/#using-the-key-prop-with-react-fragments)**

In some cases, the key prop is required in a React application. In react, the key props are typically used to control component instances. React uses the key prop in scenarios like this to identify which items changed, removed, or added. Using the key props in a React application with fragments will be like the code snippet below.

`function TableData () {  return  (       {data.map(rec=>        <React.Fragment key={rec.id}>           <td>{rec.hobby}</td>        </React.Fragment>      )}  );}`

## **Using shortcut version[](https://refine.dev/blog/how-react-fragments-is-works/#using-shortcut-version)**

Aside from using React Fragment, React also provides a shorthand notation `<></>` to wrap multiple elements together that works similarly to React Fragment but with a lower memory load. In a react application, the shorthand notation `<></>` is implemented as follows.

```jsx
function TableData() {
  return (
    <>
      <td>Eat</td>
      <td>Learn</td>
      <td>Code</td>{" "}
    </>
  );
}

```

The above code will produce the expected HTML equivalent below.

`<table>  <tr>    <div>       <td>Eat</td>      <td>Learn</td>      <td>Code</td>    </div>  </tr></table>`

However, there are some drawbacks to this approach. For example, implementing the key props is impossible because the shorthand notation `<></>` will not work here. After all, it cannot take an attribute.

## **Fragment in Action[](https://refine.dev/blog/how-react-fragments-is-works/#fragment-in-action)**

Now let's see how fragments are used in a React application. In the example below, we'll use the React Fragment to render a list of items in a table.

```
import "./App.css";
import React from "react";
const Table = ({ children, style }) => {
  return <div>{children}</div>;
};

const TableData = () => {
  return (
    <React.Fragment>
      <td>John Doe</td>
      <td>16</td>
      <td>Developer</td>;
    </React.Fragment>
  );
};

function App() {
  return (
    <Table>
      {" "}
      <tr>
        {" "}
        <th>Name</th> <th>Age</th> <th>Occupation</th>{" "}
      </tr>{" "}
      <TableData />{" "}
    </Table>
  );
}
export default App;

```

In the above code snippet, we created two components that we to be rendered in our application. In the render method, we used React Fragment instead of wrapping the elements in the TableData components in a div. This way, our table data will be rendered as expected.

**What is React Fragment?**  

React Fragment is a feature in React that **allows you to return multiple elements from a React component by allowing you to group a list of children without adding extra nodes to the DOM**. To return multiple elements from a React component, you'll need to wrap the element in a root element.



<br> 


## Q.27 memo, useMemo, useCallback (differences)

In the context of React, `memo`, `useMemo`, and `useCallback` are all related to performance optimization, but they serve different purposes.

1. **`memo`**:
    - `memo` is a higher-order component (HOC) that you can use to memoize the rendering of a functional component.
    - It prevents a functional component from re-rendering if its props or state haven't changed. It's useful when the rendering of the component is expensive and you want to avoid unnecessary re-renders.
    
    Example:
    
    ```jsx
    const MyComponent = React.memo((props) => {
      // Component logic
    });
    
    ```
    
2. **`useMemo`**:
    - `useMemo` is a hook that helps memoize the result of a computation. It takes a function and an array of dependencies and returns a memoized version of the value.
    - It is useful when you have a computationally expensive operation inside your component that depends on certain values, and you want to avoid re-computing it on every render.
    - it returns memoized value.
    
    Example:
    
    ```jsx
    const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
    
    ```
    
3. **`useCallback`**:
    - `useCallback` is a hook that memoizes a callback function. It is particularly useful when you need to pass a callback to child components and you want to avoid unnecessary re-creations of the callback on each render.
    - It takes a callback function and an array of dependencies, and it returns a memoized version of the callback.
    - it returns memoized callback function.
    
    Example:
    
    ```jsx
    const memoizedCallback = useCallback(() => {
      // Callback logic
    }, [dependency1, dependency2]);
    
    ```
    

In summary, `memo` is used to memoize the rendering of a component, `useMemo` is used to memoize the result of a computation, and `useCallback` is used to memoize a callback function. All three are tools to optimize performance in React applications by avoiding unnecessary re-renders or re-computations.


<br> 


## Q.28 Difference between useMemo and useCallback
`useCallback` and `useMemo` are both hooks in React that help with performance optimization, but they serve different purposes.

1. **`useCallback`**:
    
    `useCallback` is used to memoize a callback function. It is particularly useful when passing a callback to child components, as it helps in preventing unnecessary re-rendering of those components. It returns a memoized version of the callback function.
    
    ```jsx
    const memoizedCallback = useCallback(
      () => {
        doSomething();
      },
      [dependency1, dependency2]
    );
    ```
    
    The second argument to `useCallback` is an array of dependencies. The memoized callback will only be re-created if one of the dependencies changes. This is helpful to avoid recreating the callback on every render if the dependencies haven't changed.
    
2. **`useMemo`**:
    
    `useMemo` is used to memoize the result of a computation. It memoizes the value itself rather than a function. It takes a function and an array of dependencies, and it only recomputes the memoized value when one of the dependencies has changed.
    
    ```jsx
    const memoizedValue = useMemo(
      () => computeExpensiveValue(a, b),
      [a, b]
    );
    
    ```
    
    Similar to `useCallback`, the second argument is an array of dependencies. If any of these dependencies change, `useMemo` will re-run the provided function and return the memoized result.
    

In summary, `useCallback` is used for memoizing callback functions, while `useMemo` is used for memoizing the result of a computation. Both are helpful in preventing unnecessary recalculations and re-renders in React components.


<br> 


## Difference between useState and useRef hook.
`useState` and `useRef` are both hooks provided by React, but they serve different purposes.

1. **useState**:
   - `useState` is used to add state variables to functional components in React. 
   - When you call `useState`, it returns a stateful value (the current state) and a function to update it. 
   - It's typically used when you need to store and update state within a component, such as input values, toggles, counters, etc.
   - Every time the state is updated using `useState`, the component re-renders to reflect the new state.

Example:
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

2. **useRef**:
   - `useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument (initial value).
   - The `current` property of the ref object can be updated independently and it does not cause re-rendering of the component.
   - It's commonly used to persist values across renders without causing re-renders or to access DOM nodes directly.

Example:
```jsx
import React, { useRef, useEffect } from 'react';

function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  
  const focusInput = () => {
    inputEl.current.focus();
  };

  useEffect(() => {
    focusInput(); // Focuses the input on component mount
  }, []);

  return (
    <div>
      <input ref={inputEl} type="text" />
      <button onClick={focusInput}>Focus the input</button>
    </div>
  );
}
```

In summary, `useState` is for managing stateful values within a component, causing re-renders when the state updates, while `useRef` is for persisting values across renders without causing re-renders and accessing DOM nodes directly.


<br>

## Q. Difference between useState and useReducer hook ?  

`useState` and `useReducer` are both hooks provided by React for managing state in functional components, but they have some differences in terms of usage and complexity.

1. **useState**:
   - `useState` is a basic hook for managing state in functional components.
   - It returns an array with two elements: the current state value and a function to update it.
   - This function updates the state by replacing the old state with the new one. It does not provide any way to compute the next state based on the previous state.
   - It's simple and easy to use for managing independent state values or state that can be updated directly.

Example:
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

2. **useReducer**:
   - `useReducer` is a more advanced hook for managing state in functional components, especially when state logic is complex and involves multiple sub-values or when the next state depends on the previous one.
   - It takes a reducer function and an initial state, similar to the `useReducer` function in traditional React class components.
   - The reducer function receives the current state and an action, and returns the new state based on the action.
   - It's useful when the state logic involves multiple actions or when the state needs to be updated based on its previous value.

Example:
```jsx
import React, { useReducer } from 'react';

// Reducer function
const reducer = (state, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
};

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>Decrement</button>
    </div>
  );
}
```

In summary, `useState` is simpler and more suitable for basic state management, while `useReducer` is more powerful and suitable for managing complex state logic or state that depends on its previous value.

<br> 

## Q.29 PURE AND IMPURE COMPONENTS IN REACTJS  

**Pure components are stateless and do not have any internal state.** **Impure components can have internal state and manage their own data**. Pure components are primarily used for rendering UI based on props only. Impure components can perform side effects, such as making API calls or modifying global state.

In React, components are often categorized as either "pure" or "impure" based on their behavior with respect to rendering and state changes.

1. **Pure Components:**
    
    In React.js, a "Pure Component" is a class component that extends React.PureComponent instead of React.Component. The primary difference between a regular component and a pure component lies in how they handle updates and re-renders.
    
    When you use a pure component, React automatically performs a shallow comparison of the current props and state with the next props and state. If there are no differences in the shallow comparison, React prevents the component from re-rendering. This can lead to performance optimizations in scenarios where a component's render output is solely determined by its props and state.
    
    The shallow comparison involves checking if the values of props and state have changed by comparing the previous and current values of each property at the top level. It doesn't perform a deep comparison of nested objects or arrays. If you need to handle complex data structures with nested objects or arrays, you might need to implement additional logic or consider using immutability techniques to ensure proper updates.
    
    Here's an example of a pure component:
    
    ```jsx
    import React, { PureComponent } from 'react';
    
    class MyPureComponent extends PureComponent {
      render() {
        return (
          <div>
            {/* Render component content based on props and state */}
          </div>
        );
      }
    }
    
    ```
    
    It's important to note that using pure components can be beneficial for performance optimization, but it's crucial to understand their limitations and use them appropriately. In some cases, a regular component may be more suitable, especially if you need to implement custom shouldComponentUpdate logic or if your component relies on mutable data structures.
    
2. **Impure Components:**
    - **Definition:** Impure components may have internal state, and their rendering behavior might depend on changes within their internal state.
    - **Characteristics:**
        - Impure components might re-render even if the props and state remain the same because their internal logic might trigger a re-render.
        - They may have side effects, such as asynchronous operations, that can cause the component to re-render when the operation is complete.
    - **Example:**
        
        ```jsx
        class ImpureExample extends React.Component {
          constructor(props) {
            super(props);
            this.state = {
              count: 0,
            };
          }
        
          handleClick = () => {
            this.setState((prevState) => ({ count: prevState.count + 1 }));
          };
        
          render() {
            return (
              <div>
                <p>Count: {this.state.count}</p>
                <button onClick={this.handleClick}>Increment</button>
              </div>
            );
          }
        }
        
        ```
        

Understanding the difference between pure and impure components is important for optimizing performance in React applications. Pure components are more predictable and easier to reason about, especially when working with optimizations like memoization. Impure components, while necessary in certain scenarios, may require extra attention to avoid unnecessary re-renders and performance bottlenecks.

 In these components, React will re-render whenever the component's state or props change, regardless of whether the actual content to be rendered has changed


 <br> 

 ## Q. 30 WHAT IS PROPS IN REACTJS ? 
 In React.js, "props" is short for "properties," and it is a mechanism for passing data from a parent component to a child component. Props are a way for components to communicate and share information with each other in a React application.

Here are the key points about props in React:

1. **Passing Data:**
    - Props are used to pass data from a parent component to a child component.
    - They allow the parent component to share information with its children.
2. **Immutable:**
    - Props are immutable, meaning they cannot be modified by the child component. They are read-only.
    - A child component cannot modify the values of the props it receives from its parent.
3. **Function Parameters:**
    - In functional components, props are received as an argument to the functional component.
    - In class components, props are accessed via the `this.props` object.
4. **Example:**
    - Here's a simple example of a parent component passing a prop to a child component:
        
        ```jsx
        // ParentComponent.js
        import React from 'react';
        import ChildComponent from './ChildComponent';
        
        const ParentComponent = () => {
          const message = "Hello from parent!";
          return <ChildComponent greeting={message} />;
        };
        
        // ChildComponent.js
        import React from 'react';
        
        const ChildComponent = (props) => {
          return <p>{props.greeting}</p>;
        };
        
        export default ChildComponent;
        
        ```
        
5. **Default Values:**
    - You can provide default values for props using defaultProps to handle cases where a parent component does not pass a particular prop.
        
        ```jsx
        // ChildComponent.js
        import React from 'react';
        
        const ChildComponent = (props) => {
          return <p>{props.greeting}</p>;
        };
        
        ChildComponent.defaultProps = {
          greeting: "Default Greeting",
        };
        
        export default ChildComponent;
        
        ```
        

Props play a crucial role in creating reusable and modular components in React, allowing for a clear flow of data and communication between different parts of the application. They help in building a component-based architecture where components can be composed and reused in various parts of the application.


<br> 

## Q.31 What is the difference between state and props?
In React, both `state` and `props` are plain JavaScript objects and used to manage the data of a component, but they are used in different ways and have different characteristics. `state` is managed by the component itself and can be updated using the `setState()` function. Unlike props, state can be modified by the component and is used to manage the internal state of the component. Changes in the state trigger a re-render of the component and its children. 

`props` (short for "properties") are passed to a component by its parent component and are `read-only`, meaning that they cannot be modified by the component itself. props can be used to configure the behavior of a component and to pass data between components.



<br> 

## Q.32 What are synthetic events in React?
`SyntheticEvent` is a cross-browser wrapper around the browser's native event. Its API is same as the browser's native event, including `stopPropagation()` and `preventDefault()`, except the events work identically across all browsers. The native events can be accessed directly from synthetic events using `nativeEvent` attribute.

Let's take an example of BookStore title search component with the ability to get all native event properties

```jsx
function BookStore() {
   handleTitleChange(e) {
    console.log("The new title is:", e.target.value);
    // 'e' represents synthetic event
    const nativeEvent = e.nativeEvent;
    console.log(nativeEvent);
    e.stopPropogation();
    e.preventDefault();
  }

  return <input name="title" onChange={handleTitleChange} />;
}
```


<br> 

## Q.33 What is "key" prop and what is the benefit of using it in arrays of elements?
A `key` is a special attribute you **should** include when mapping over arrays to render data. *Key* prop helps React identify which items have changed, are added, or are removed.

Keys should be unique among its siblings. Most often we use ID from our data as *key*:

```jsx
const todoItems = todos.map((todo) => <li key={todo.id}>{todo.text}</li>);
```

When you don't have stable IDs for rendered items, you may use the item *index* as a *key* as a last resort:

```
const todoItems = todos.map((todo, index) => <li key={index}>{todo.text}</li>);
```

**Note:**

1. Using *indexes* for *keys* is **not recommended** if the order of items may change. This can negatively impact performance and may cause issues with component state.
2. If you extract list item as separate component then apply *keys* on list component instead of `li` tag.
3. There will be a warning message in the console if the `key` prop is not present on list items.
4. The key attribute accepts either string or number and internally convert it as string type.

<br> 


## Q.34 What is the difference between createElement and cloneElement?
JSX elements will be transpiled to React.createElement() functions to create React elements which are going to be used for the object representation of UI. Whereas cloneElement is used to clone an element and pass it new props.


<br> 

## Q.35 What is Lifting State Up in React?
When several components need to share the same changing data then it is recommended to lift the shared state up to their closest common ancestor. That means if two child components share the same data from its parent, then move the state to parent instead of maintaining local state in both of the child components.


<br> 

## Q.36 What are the different phases of component lifecycle?
1. The component lifecycle has three distinct lifecycle phases:
    1. **Mounting:** The component is ready to mount in the browser DOM. This phase covers initialization from `constructor()`, `getDerivedStateFromProps()`, `render()`, and `componentDidMount()` lifecycle methods.
    2. **Updating:** In this phase, the component gets updated in two ways, sending the new props and updating the state either from `setState()` or `forceUpdate()`. This phase covers `getDerivedStateFromProps()`, `shouldComponentUpdate()`, `render()`, `getSnapshotBeforeUpdate()` and `componentDidUpdate()` lifecycle methods.
    3. **Unmounting:** In this last phase, the component is not needed and gets unmounted from the browser DOM. This phase includes `componentWillUnmount()` lifecycle method.
    
    It's worth mentioning that React internally has a concept of phases when applying changes to the DOM. They are separated as follows
    
    1. **Render** The component will render without any side effects. This applies to Pure components and in this phase, React can pause, abort, or restart the render.
    2. **Pre-commit** Before the component actually applies the changes to the DOM, there is a moment that allows React to read from the DOM through the `getSnapshotBeforeUpdate()`.
    3. **Commit** React works with the DOM and executes the final lifecycles respectively `componentDidMount()` for mounting, `componentDidUpdate()` for updating, and `componentWillUnmount()` for unmounting.
    
    React 16.3+ Phases (or an [interactive version](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/))
    
    !https://github.com/sudheerj/reactjs-interview-questions/raw/master/images/phases16.4.png
    
    Before React 16.3
    
    !https://github.com/sudheerj/reactjs-interview-questions/raw/master/images/phases.png



<br>


## Q.37 What are the lifecycle methods of React?
Before React 16.3

- **componentWillMount:** Executed before rendering and is used for App level configuration in your root component.
- **componentDidMount:** Executed after first rendering and here all AJAX requests, DOM or state updates, and set up event listeners should occur.
- **componentWillReceiveProps:** Executed when particular prop updates to trigger state transitions.
- **shouldComponentUpdate:** Determines if the component will be updated or not. By default it returns `true`. If you are sure that the component doesn't need to render after state or props are updated, you can return false value. It is a great place to improve performance as it allows you to prevent a re-render if component receives new prop.
- **componentWillUpdate:** Executed before re-rendering the component when there are props & state changes confirmed by `shouldComponentUpdate()` which returns true.
- **componentDidUpdate:** Mostly it is used to update the DOM in response to prop or state changes.
- **componentWillUnmount:** It will be used to cancel any outgoing network requests, or remove all event listeners associated with the component.

React 16.3+

- **getDerivedStateFromProps:** Invoked right before calling `render()` and is invoked on *every* render. This exists for rare use cases where you need a derived state. Worth reading [if you need derived state](https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html).
- **componentDidMount:** Executed after first rendering and where all AJAX requests, DOM or state updates, and set up event listeners should occur.
- **shouldComponentUpdate:** Determines if the component will be updated or not. By default, it returns `true`. If you are sure that the component doesn't need to render after the state or props are updated, you can return a false value. It is a great place to improve performance as it allows you to prevent a re-render if component receives a new prop.
- **getSnapshotBeforeUpdate:** Executed right before rendered output is committed to the DOM. Any value returned by this will be passed into `componentDidUpdate()`. This is useful to capture information from the DOM i.e. scroll position.
- **componentDidUpdate:** Mostly it is used to update the DOM in response to prop or state changes. This will not fire if `shouldComponentUpdate()` returns `false`.
- **componentWillUnmount** It will be used to cancel any outgoing network requests, or remove all event listeners associated with the component.



<br> 

## Q.38 What is reconciliation?
Reconciliation is the process through which React updates the Browser DOM and makes React work faster. React use a diffing algorithm so that component updates are predictable and faster. React would first calculate the difference between the real DOM and the copy of DOM (Virtual DOM) when there's an update of components. React stores a copy of Browser DOM which is called Virtual DOM. When we make changes or add data, React creates a new Virtual DOM and compares it with the previous one. This comparison is done by Diffing Algorithm. Now React compares the Virtual DOM with Real DOM. It finds out the changed nodes and updates only the changed nodes in Real DOM leaving the rest nodes as it is. This process is called Reconciliation.


<br> 

## Q.39 How to use InnerHtml in React?
The **innerHTML** is risky because it is easy to expose users to a cross-site scripting (XSS) attack. React provides **dangerouslySetInnerHTML** as a replacement for innerHTML. It allows to set HTML directly from React by using `dangerouslySetInnerHTML` and passing an object with a `__html` key that holds HTML.

**Example:**

```jsx
/**
 * InnerHtml in React
 */
import React from "react";

export default function App() {
  return (
    <div
      dangerouslySetInnerHTML={{
        __html: "<p>This text is set using <b>dangerouslySetInnerHTML</b></p>"
      }}
    ></div>
  );
}
```


<br> 

## Q.40 What is the difference between Element and Component?
**1. React Element:**

It is a simple object that describes a DOM node and its attributes or properties. It is an immutable description object and you can not apply any methods on it.

```jsx
const element = <h1>React Element Example!</h1>;
ReactDOM.render(element, document.getElementById('app'));
```

**2. React Component:**

**React component is a function or a class that can produce React elements and manage their state and lifecycle**. Components can return multiple elements, components, strings, numbers, or any other types React can render.

```jsx
function Message() {
  return <h2>React Component Example!</h2>;
}
ReactDOM.render(<Message />, document.getElementById("app"));
```



<br>

## Q.41 What is "Children" in React?

In React, **children** refer to the generic box whose contents are **unknown** until they're passed from the parent component. Children allows to pass components as data to other components, just like any other prop you use.

The special thing about children is that React provides support through its `ReactElement API` and `JSX`. XML children translate perfectly to React children!

**Example:**

```jsx
/**
 * Children in React
 */
const Picture = (props) => {
  return (
    <div>
      <img src={props.src}/>
      {props.children}
    </div>
  )
}
```

This component contains an `<img>` that is receiving some props and then it is displaying `{props.children}`. Whenever this component is invoked `{props.children}` will also be displayed and this is just a reference to what is between the opening and closing tags of the component.

```jsx
/**
 * App.js
 */

render () {
  return (
    <div className='container'>
      <Picture key={picture.id} src={picture.src}>
          {/** what is placed here is passed as props.children **/}
      </Picture>
    </div>
  )
}
```


<br> 

## Q.42 What are the different phases of React component lifecycle?
React provides several methods that notify us when certain stage of this process occurs. These methods are called the component lifecycle methods and they are invoked in a predictable order. The lifecycle of the component is divided into four phases.

!https://github.com/learning-zone/react-basics/raw/master/assets/react-lifecycle.png

**1. Mounting:**

These methods are called in the following order when an instance of a component is being created and inserted into the DOM:

- `constructor()`
- `getDerivedStateFromProps()`
- `render()`
- `componentDidMount()`

**2. Updating:**

The next phase in the lifecycle is when a component is updated. A component is updated whenever there is a change in the component's state or props.

React has five built-in methods that gets called, in this order, when a component is updated:

- `getDerivedStateFromProps()`
- `shouldComponentUpdate()`
- `render()`
- `getSnapshotBeforeUpdate()`
- `componentDidUpdate()`

**3. Unmounting:**

The next phase in the lifecycle is when a component is removed from the DOM, or unmounting as React likes to call it.

- `componentWillUnmount()`


<br> 


## Q.43 What is difference between useEffect() vs componentDidMount()?
In react when we use class based components we get access to lifecycle methods ( like `componentDidMount()`, `componentDidUpdate(), etc ). But when we want use a functional component and also we want to use lifecycle methods, then using useEffect() we can implement those lifecycle methods.

**1. componentDidMount():**

The `componentDidMount()` and `useEffect()` run after the mount. However useEffect() runs after the paint has been committed to the screen as opposed to before. This means we would get a flicker if needed to read from the DOM, then synchronously set state to make new UI.

The `useLayoutEffect()` was designed to have the same timing as componentDidMount(). So `useLayoutEffect(fn, [])` is a much closer match to componentDidMount() than useEffect(fn, []) -- at least from a timing standpoint.

```jsx
/**
 * componentDidMount() in Class Component
 */
import React, { Component } from "react";

export default class SampleComponent extends Component {
  componentDidMount() {
    // code to run on component mount
  }
  render() {
    return <>componentDidMount Example</>;
  }
}
```

**2. useEffect():**

```jsx
/**
 * useEffect() in Functional Component
 */
import React, { useEffect } from "react";

const SampleComponent = () => {
  useEffect(() => {
    // code to run on component mount
  }, []);
  return <>useEffect Example</>;
};
export default SampleComponent;
```

When `useEffect()` is used to get data from server.

- The first argument is a callback that will be fired after browser layout and paint. Therefore it does not block the painting process of the browser.
- The second argument is an array of values (usually props).
- If any of the value in the array changes, the callback will be fired after every render.
- When it is not present, the callback will always be fired after every render.
- When it is an empty list, the callback will only be fired once, similar to componentDidMount.


<br> 


## Q.44 How to create props proxy for Higher Order Component component?
Creating a props proxy for a Higher Order Component (HOC) in a functional component involves wrapping the original component and passing down additional or modified props. You can use the spread operator (`...`) to pass the existing props along with any additional ones you want to include.

Here's an example of how you can create a simple props proxy for a functional component using an HOC:

```jsx
import React from 'react';

// Higher Order Component (HOC) as a function
const withPropsProxy = (WrappedComponent) => {
  // Return a new functional component
  return (props) => {
    // Create a new set of props or modify existing ones
    const modifiedProps = {
      ...props,
      additionalProp: 'This is an additional prop',
    };

    // Render the original component with the modified props
    return <WrappedComponent {...modifiedProps} />;
  };
};

// Original functional component
const MyComponent = (props) => {
  return (
    <div>
      <p>Original Component</p>
      <p>Received Prop: {props.receivedProp}</p>
      <p>Additional Prop: {props.additionalProp}</p>
    </div>
  );
};

// Wrap the original component with the HOC
const EnhancedComponent = withPropsProxy(MyComponent);

// Usage of the enhanced component
const App = () => {
  return (
    <div>
      <EnhancedComponent receivedProp="Hello from parent" />
    </div>
  );
};

export default App;

```

In this example:

- `withPropsProxy` is a function that takes a component (`WrappedComponent`) and returns a new functional component.
- The new functional component, when rendered, passes down the existing props along with an additional prop (`additionalProp` in this case).
- `EnhancedComponent` is the result of wrapping `MyComponent` with the `withPropsProxy` HOC.

When `EnhancedComponent` is used, it will render `MyComponent` with the original props plus the additional prop provided by the HOC. This is a basic example, and you can customize the HOC to pass different props or modify existing ones based on your specific use case.


<br> 


## Q.45  what are default props in react functional component 
In React functional components, default props are default values assigned to certain props if the parent component does not provide a value for those props. Default props provide a way to ensure that a component receives a specific value for a prop, even if the parent component does not explicitly pass it.

Here's how you can define default props in a functional component:

```jsx
import React from 'react';

const MyComponent = ({ name, age }) => {
  return (
    <div>
      <p>Name: {name}</p>
      <p>Age: {age}</p>
    </div>
  );
};

// Define default values for props
MyComponent.defaultProps = {
  name: 'John Doe',
  age: 30,
};

export default MyComponent;

```

In this example:

- The `MyComponent` functional component receives `name` and `age` as props.
- `MyComponent.defaultProps` is an object where you can specify default values for each prop.
- If the parent component does not provide a value for `name` or `age`, the default values specified in `MyComponent.defaultProps` will be used.

Now, when you use `MyComponent` in another component without providing values for `name` or `age`, the default values will be used:

```jsx
import React from 'react';
import MyComponent from './MyComponent';

const App = () => {
  return (
    <div>
      {/* Default values will be used for name and age */}
      <MyComponent />
    </div>
  );
};

export default App;

```

In this case, if the parent component does not pass values for `name` or `age`, the default values specified in `MyComponent.defaultProps` (`John Doe` and `30`, respectively) will be used. If the parent component does provide values, those values will take precedence over the default ones.


<br> 

## Q.47 How are boolean props used in React?
React JSX has exactly two ways of passing true, `<MyComponent prop />` and `<MyComponent prop={true} />` and exactly one way of passing false `<MyComponent prop={false} />`.

**Example:**

```jsx
/**
 * Boolean Props
 */
const MyComponent = ({ prop1, prop2 }) => (
  <div>
    <div>Prop1: {String(prop1)}</div>
    <div>Prop2: {String(prop2)}</div>
  </div>
)

function App() {
  return (
    <div>
      <MyComponent prop1={true} prop2={false} />
      <MyComponent prop1 prop2 />
      <MyComponent prop1={false} prop2 />
    </div>
  );
}
```


<br> 

## Q. 48 What is the difference between createElement and cloneElement?
JSX elements will be transpiled to `React.createElement()` functions to create React elements which are going to be used for the object representation of UI. Whereas cloneElement is used to clone an element and pass it new props.

The `React.cloneElement()` function returns a copy of a specified element. Additional props and children can be passed on in the function. We shoul use this function when a parent component wants to add or modify the `props` of its children.

```jsx
import React from 'react'

export default class App extends React.Component {
  // rendering the parent and child component
  render() {
    return (
      <ParentComp>
        <MyButton/>
        <br/>
        <MyButton/>
      </ParentComp>
    )
		  }
}

/**
 * The parent component
 */
class ParentComp extends React.Component {
  render() {
    // The new prop to the added.
    let newProp = 'red'
      // Looping over the parent's entire children,
      // cloning each child, adding a new prop.
    return (
      <div>
        {React.Children.map(this.props.children,
          child => {
            return React.cloneElement(child,
            {newProp}, null)
        })}
      </div>
    )
  }
}

/**
 * The child component
 */
class MyButton extends React.Component {
  render() {
    return <button style =
    {{ color: this.props.newProp }}>
    Hello World!</button>
  }
}
```

<br> 

## Q.49 How to create custom Hooks?
React also allows us to create custom Hooks with unique features that extracts component logic into reusable functions.

A custom Hooks has following features:

- As a function, it takes input and returns output.
- Its name starts with **use** like useQuery, useMedia…
- Unlike functional components, custom hooks return a normal, non-jsx data.
- Unlike normal functions, custom hooks can use other hooks such as useState, useRef… and other custom hooks.

**Example:** Custom Hook - useFetch()

```jsx
/**
 * Custom Hook
 */
import { useState, useEffect } from "react";

const useFetch = (url) => {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then((data) => setData(data));
  }, [url]);

  return [data];
};

export default useFetch;
```

```jsx
/**
 * App Component
 */
import "./styles.css";
import useFetch from "./useFetch";

export default function App() {
  // custom hook
  const [data] = useFetch("https://jsonplaceholder.typicode.com/todos");
  return (
    <>
      {data &&
        data.map((item) => {
          return <p key={item.id}>{item.title}</p>;
        })}
    </>
  );
}
```


<br> 

## Q.50 Q. How to compare oldValues and newValues on React Hooks useEffect?
We can store old values in a **ref** since assigning values to them won't trigger a re-rendering of the component but the value will persist after each render cycle.

```jsx
import React, { useRef, useEffect, useState } from "react";
const usePrevious = (value) => {
  const ref = useRef();
  useEffect(() => {
    ref.current = value;
  });
  return ref.current;
};

export default function App() {
  const [count, setCount] = useState(0);
  const prevCount = usePrevious(count);

  useEffect(() => {
    console.log("prevCount: ", prevCount, "count: ", count);
  }, [prevCount, count]);

  return (
    <div>
      <button onClick={() => setCount((c) => c + 10)}>Increment</button>
      <p>{count}</p>
    </div>
  );
}

```

Here, We create the **usePrevious** hook with the value parameter which is state we want to get the previous value from, In the hook, we create a ref with the **useRef** hook to create a non-reactive property. Then we add the **useEffect** hook with a callback that sets the **ref.current** to value to set the previous value.


<br> 

## Q. What is error  boundaries in reactjs ? 

Error boundaries in React are components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of crashing the entire React application. They are a feature introduced in React 16 to help developers handle errors gracefully.

Here's how error boundaries work:

1. **Definition**: Error boundaries are regular React components that define special lifecycle methods to catch errors during rendering, in lifecycle methods, and in constructors of the components below them in the tree.

2. **Lifecycle Methods**: Error boundaries define two lifecycle methods:
   - `static getDerivedStateFromError(error)`: This method is used to update the component state when an error is caught. It returns an object to update the state, and it is called during the rendering phase.
   - `componentDidCatch(error, info)`: This method is invoked after an error has been thrown by a descendant component. It receives two arguments: `error`, which is the error that was thrown, and `info`, which is an object with a `componentStack` key containing information about which component in the tree threw the error.

3. **Usage**: To use an error boundary in your application, you simply wrap the component tree that you want to protect with the error boundary component. Any errors thrown within the error boundary's subtree will be caught by the error boundary.

4. **Fallback UI**: Inside the `componentDidCatch` method, you can implement logic to display a fallback UI, such as an error message or a custom error component, instead of rendering the component tree that caused the error.

5. **Error Propagation**: Error boundaries catch errors in their child component tree, but not in the component itself or in other error boundary components higher in the tree. If an error occurs within an error boundary itself, it will propagate up to the next error boundary in the tree.

Error boundaries are useful for building more robust React applications by preventing errors from crashing the entire UI and providing a better user experience by displaying informative error messages or fallback UIs instead.

we can not use it in : 
	1. Evet handlers
 	2. Asynchronouse code 
  	3. server side rendering
   	4. Error thrown in error boundary itself






<br> 


## Q. What is lazy loading in reactjs ? 

Lazy loading in React refers to the technique of delaying the loading of certain components or assets until they are needed. This is particularly useful for improving the performance of your application by reducing the initial bundle size and speeding up the initial load time.

In React, lazy loading is typically achieved using dynamic imports and React's `React.lazy()` function, along with `Suspense` for handling loading states. Here's how it works:

1. **Dynamic Imports**: Instead of importing a component directly at the top of your file, you import it dynamically using the `import()` function, which returns a Promise.

2. **React.lazy()**: You wrap the dynamic import inside the `React.lazy()` function, which allows React to lazily load the component when it's needed.

3. **Suspense**: You use the `Suspense` component from React to handle the loading state while the component is being fetched. This allows you to display a loading spinner or any other UI until the component is ready.

Here's an example of how you can implement lazy loading in React:

```jsx
import React, { Suspense } from 'react';

const LazyComponent = React.lazy(() => import('./LazyComponent'));

function App() {
  return (
    <div>
      <h1>My App</h1>
      <Suspense fallback={<div>Loading...</div>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}

export default App;
```

In this example:

- `LazyComponent` is the component that you want to lazy load.
- We use `React.lazy()` to dynamically import `LazyComponent` only when it's needed.
- The `Suspense` component is used to handle the loading state while `LazyComponent` is being fetched. The `fallback` prop specifies the UI to display during loading.

Lazy loading is especially beneficial for large applications with many components, as it allows you to split your code into smaller, more manageable chunks and load them only when necessary, improving the overall performance of your application.






<br> 



## Difference between grid and flex ? 

Both CSS Grid and Flexbox are layout models in CSS, but they have different use cases and functionalities:

1. **Flexbox**:
   - Primarily designed for one-dimensional layouts (either rows or columns).
   - It works along a single axis at a time.
   - Ideal for laying out items within a container in a single direction, allowing them to flex and fill available space.
   - Great for aligning items horizontally or vertically.
   - Useful for creating responsive layouts, navigation menus, and aligning items within a container.
   - Best suited for smaller-scale layouts and components.

2. **CSS Grid**:
   - Designed for two-dimensional layouts with both rows and columns.
   - It allows you to define both row and column layouts simultaneously.
   - Offers more control over the placement and alignment of items in both axes.
   - Enables you to create complex grid-based layouts with ease, such as grids with fixed or flexible widths and heights.
   - Supports alignment, spacing, and sizing of grid tracks (rows and columns) independently.
   - Suitable for larger-scale layouts like entire page layouts, grids with intricate designs, and complex user interfaces.

In summary, Flexbox is best for one-dimensional layouts where you're primarily concerned with arranging items along a single axis, while CSS Grid is ideal for two-dimensional layouts where you need precise control over both rows and columns, making it suitable for creating complex grid-based designs. Depending on your layout requirements, you may choose to use one or both of these layout models in combination to achieve your desired design.




<br>


## Q.51  How can I force a component to re-render with hooks in React?
The **useState()** or **useReducer()** hooks can be used to force a React component to rerender.

The example below is equivalent to **forceUpdate()** method in class-based components. This hook works in the following way:

- The `useState()` hook returns an array with two elements, a value and an updater function.
- Here, we are instantly calling the updater function, which in this case is called with `undefined`, so it is the same as calling `updater(undefined)`.

**Example:**

```jsx
import React, { useState } from "react";

const useForceUpdate = () => useState()[1];

export default function App() {
  const forceUpdate = useForceUpdate();
  console.log("Rendered");

  return <button onClick={forceUpdate}>Update Me</button>;
}
```

<br> 

## Q.52 Why do we use array destructuring in useState?
The `useState` hook allows us to make our function components stateful. When called, `useState()` returns an array of two items. The first being our state value and the second being a function for setting or updating that value. The `useState` hook takes a single argument, the initial value for the associated piece of state, which can be of any Javascript data type.

```jsx
import React, { useState } from 'react';

const Component = () => {
    const [value, setValue] = useState(initial value)
    ...
```

**Example:** State with Various Data Types

```jsx
const [count, setCount] = useState(0)
const [color, setColor] = useState('#526b2d')
const [isHidden, setIsHidden] = useState(true)
const [products, setProducts] = useState([])
const [user, setUser] = useState({
    username: '',
    avatar: '',
    email: '',
})
```


<br> 

## Q.53 Exlain is useCallback(), useMemo(), useImperativeHandle(), useLayoutEffect(), useDebugValue() in React?
**1. useCallback():**

React's `useCallback()` Hook can be used to optimize the rendering behavior of your React function components. The `useCallback` will return a memoized version of the callback that only changes if one of the dependencies has changed.

This is useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders (e.g. shouldComponentUpdate).

**Example:**

```jsx
/**
 * useCallback()
 */
import React, { useState, useCallback, useEffect } from "react";

const count = new Set();

export default function App() {
  const [counter, setCounter] = useState(0);

  const increment = useCallback(() => {
    setCounter(counter + 1);
  }, [counter]);

  useEffect(() => {
    count.add(increment);
    console.log(count.size);
  }, [increment]);

  return (
    <>
      <h1>useCallback()</h1>
      <h2>Function Call: {count.size}</h2>
      <button onClick={increment}>Increment</button>
    </>
  );
}
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-usecallback-zecshz?file=/src/App.js)**

**2. useMemo():**

The `useMemo()` is similar to `useCallback()` except it allows you to apply memoization to any value type. It does this by accepting a function which returns the value and then that function is only called when the value needs to be retrieved.

**Example:**

React application which renders a list of users and allows us to filter the users by their name. The filter happens only when a user explicitly clicks a button; not already when the user types into the input field.

```jsx
import React from 'react'

const users = [
  { id: 'a', name: 'Robin' },
  { id: 'b', name: 'Dennis' },
]

const App = () => {
  const [text, setText] = React.useState('')
  const [search, setSearch] = React.useState('')

  const handleText = (event) => {
    setText(event.target.value)
  }

  const handleSearch = () => {
    setSearch(text)
  }

  // useMemo Hooks
  const filteredUsers = React.useMemo(
    () =>
      users.filter((user) => {
        console.log('Filter function is running ...');
        return user.name.toLowerCase().includes(search.toLowerCase());
      }),
    [search]
  );

  return (
    <div>
      <input type="text" value={text} onChange={handleText} />
      <button type="button" onClick={handleSearch}>
        Search
      </button>

      <List list={filteredUsers} />
    </div>
  )
}

const List = ({ list }) => {
  return (
    <ul>
      {list.map((item) => (
        <ListItem key={item.id} item={item} />
      ))}
    </ul>
  )
}

const ListItem = ({ item }) => {
  return <li>{item.name}</li>
}

export default App
```

Here, the **filteredUsers** function is only executed once the search state changes. It doesn't run if the text state changes, because that's not a dependency for this filter function and thus not a dependency in the dependency array for the useMemo hook.

**3. useImperativeHandle():**

`useImperativeHandle()` customizes the instance value that is exposed to parent components when using `ref`. As always, imperative code using `refs` should be avoided in most cases. `useImperativeHandle` should be used with `forwardRef`.

```jsx
function FancyInput(props, ref) {
  const inputRef = useRef()
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus()
    }
  }))
  return <input ref={inputRef} ... />
}
FancyInput = forwardRef(FancyInput)
```

**4. useLayoutEffect():**

!https://github.com/learning-zone/react-basics/raw/master/assets/useLayoutEffect.png

This runs synchronously immediately after React has performed all DOM mutations. This can be useful if you need to make DOM measurements (like getting the scroll position or other styles for an element) and then make DOM mutations or trigger a synchronous re-render by updating state.

As far as scheduling, this works the same way as `componentDidMount` and `componentDidUpdate`. Your code runs immediately after the DOM has been updated, but before the browser has had a chance to "paint" those changes (the user doesn't actually see the updates until after the browser has repainted).

**Example:**

```jsx
import React, { useState, useLayoutEffect } from 'react'
import ReactDOM from 'react-dom'

const BlinkyRender = () => {
  const [value, setValue] = useState(0)

  useLayoutEffect(() => {
    if (value === 0) {
      setValue(10 + Math.random() * 200)
    }
  }, [value])

  console.log('render', value)

  return (
    <div onClick={() => setValue(0)}>
      value: {value}
    </div>
  )
}

ReactDOM.render( <BlinkyRender />, document.querySelector('#root'))
```

**useLayoutEffect vs useEffect:**

- **useLayoutEffect**: If you need to mutate the DOM and/or do need to perform measurements
- **useEffect**: If you don't need to interact with the DOM at all or your DOM changes are unobservable (seriously, most of the time you should use this).

**5. useDebugValue():**

`useDebugValue()` can be used to display a label for custom hooks in React DevTools.

**Example:**

```jsx
function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null)

  // ...

  // Show a label in DevTools next to this Hook
  // e.g. "FriendStatus: Online"
  useDebugValue(isOnline ? 'Online' : 'Offline')

  return isOnline
}
```



<br> 


## Q.54  What is the difference between useEffect() and useLayoutEffect() hooks?
The main difference between the useEffect() hook and the useLayoutEffect() hook is that the useEffect() hook serves **asynchronously**, whereas the useLayoutEffect() hook works **synchronously**.

After all DOM mutations have been completed by React, useLayoutEffect executes synchronously. If you need to measure the DOM (for example, to determine the scroll position or other styles for an element) and then modify the DOM or cause a synchronous re-render by changing the state, this can be helpful.


<br> 

# Q.55 REACT ROUTER DOM 
**Q. What are the components of react router?**

The main components of React router are

**1. BrowserRouter**:

         BrowserRouter is a router implementation that uses the HTML5 history API (pushState, replaceState and the popstate event) to keep your UI in sync with the URL. It is the parent component that is used to store all of the other components.

**2. Routes**:

         It's a new component introduced in the v6 and a upgrade of the component. The main advantages of Routes over Switch that routes are chosen based on the best match instead of being traversed in order.

**3. Route**:

        Route is the conditionally shown component that renders some UI when its path matches the current URL.

**4. Link**:

        Link component is used to create links to different routes and implement navigation around the application. It works like HTML anchor tag.

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. What is the difference between NavLink and Link?**

The `<Link>` component is used to navigate the different routes on the site. But `<NavLink>` is used to add the style attributes to the active routes.

**Link:**

```jsx
<Link to="/">Home</Link>
```

**NavLink:**

```jsx
<NavLink to="/" activeClassName="active">Home</NavLink>
```

**Example:**

index.css

```jsx
.active {
  color: blue;
}
```

Routes.js

```jsx
import ReactDOM from 'react-dom'
import './index.css'
import { Route, NavLink, BrowserRouter as Router, Switch } from 'react-router-dom'
import App from './App'
import Users from './users'
import Contact from './contact'
import Notfound from './notfound'

const Routes = (
  <Router>
    <div>
      <ul>
        <li>
          <NavLink exact activeClassName="active" to="/">
            Home
          </NavLink>
        </li>
        <li>
          <NavLink activeClassName="active" to="/users">
            Users
          </NavLink>
        </li>
        <li>
          <NavLink activeClassName="active" to="/contact">
            Contact
          </NavLink>
        </li>
      </ul>
      <hr />
      <Switch>
        <Route exact path="/" component={App} />
        <Route path="/users" component={Users} />
        <Route path="/contact" component={Contact} />
        <Route component={Notfound} />
      </Switch>
    </div>
  </Router>
)

ReactDOM.render(Routes, document.getElementById('root'))
```

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. What is withRouter for in react-router-dom?**

`withRouter()` is a higher-order component that allows to get access to the `history` object's properties and the closest `<Route>`'s match. `withRouter` will pass updated `match`, `location`, and `history` props to the wrapped component whenever it renders.

**Example:**

```jsx
import React from "react"
import PropTypes from "prop-types"
import { withRouter } from "react-router"

// A simple component that shows the pathname of the current location
class ShowTheLocation extends React.Component {
  static propTypes = {
    match: PropTypes.object.isRequired,
    location: PropTypes.object.isRequired,
    history: PropTypes.object.isRequired
  }

  render() {
    const { match, location, history } = this.props

    return <div>You are now at {location.pathname}</div>
  }
}

const ShowTheLocationWithRouter = withRouter(ShowTheLocation)
```

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. How React Router is different from history library?**

React Router is a wrapper around the history library which handles interaction with the browser's `window.history` with its browser and hash histories. React Router provides two API's

- BrowserRouter
- HashRouter

```jsx
// <BrowserRouter>
http://example.com/about

// <HashRouter>
http://example.com/#/about
```

The `<BrowserRouter>` is the more popular of the two because it uses the HTML5 History API to keep your UI in sync with the URL, whereas the `<HashRouter>` uses the hash portion of the URL (`window.location.hash`). If you need to support legacy browsers that don't support the History API, you should use `<HashRouter>`. Otherwise `<BrowserRouter>` is the better choice for most use cases.

**Example:**

```jsx
// src/index.js

import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import { BrowserRouter } from "react-router-dom";

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById("root")
);
```

The above code creates a history instance for our entire `<App>` component. Each `<Router>` component creates a history object that keeps track of the current location (`history.location`) and also the previous locations in a stack. The history object has methods such as `history.push`, `history.replace`, `history.goBack`, `history.goForward` etc.

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. How to use useNavigate() in React Router v6?**

The **useNavigate()** hook is introduced in React Router v6 to replace the `useHistory()` hook. In the earlier version, the `useHistory()` hook accesses the React Router history object and navigates to the other routers using the push() or replace() methods.

The `useNavigate()` hook returns a function that lets you navigate programmatically, for example after a form is submitted. If using `replace: true`, the navigation will replace the current entry in the history stack instead of adding a new one.

```jsx
/**
 * useNavigate()
 */
import React from "react";
import { NavLink, Link, Routes, Route,  useParams, useNavigate } from "react-router-dom";
import "./styles.css";

function Home() {
  return <h1>Home Page</h1>;
}

function Users() {
  return (
    <ul>
      <li><Link to={"/users/1"}>User 1</Link></li>
    </ul>
  );
}

function UserDetail() {
  let { id } = useParams();
  let navigate = useNavigate();

  function handleClick() {
    navigate("/users");
  }
  return (
    <>
      <h1>User Details Page: {id}</h1>
      <button onClick={handleClick}>Back</button>
    </>
  );
}

function AppRoutes() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="users" element={<Users />} />
      <Route path="users/:id" element={<UserDetail />} />
    </Routes>
  );
}

export default function App() {
  return (
    <div className="App">
      <nav>
        <ul>
          <li><NavLink to="/" end>Home Page</NavLink></li>
          <li><NavLink to="/users">Users Page</NavLink></li>
        </ul>
      </nav>
      <AppRoutes />
    </div>
  );
}
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/cool-paper-vxgn15?file=/src/App.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. How to get parameter value from query string?**

In order to get query parameters from the URL, we can use **URLSearchParams**. In simple words, URLSearchParams is a defined interface, implemented by modern browsers, that allows us to work with the query string. It does not require React Router or even React itself.

**Example:**

```jsx
// http://localhost:3000/?id=100&name=react

const queryParams = new URLSearchParams(window.location.search);

const id = queryParams.get('id');
const name = queryParams.get('name');

console.log(id, name); // 100 react
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-query-parameters-yqx7e?file=/src/ParamsExample.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. How to access history object in React Router v6?**

The **useNavigate()** hook has been added to React Router v6 to replace the `useHistory()` hook.

**Example:**

```jsx
/**
 * React Router
 */
import { BrowserRouter, Routes, NavLink, Route, useParams, useNavigate } from "react-router-dom";

export default function App() {
  return (
    <BrowserRouter>
      <div>
        <ul>
          <li><NavLink to="/">Home</NavLink></li>
          <li><NavLink to="/user/Bhavya/bhavyasingh@email.com">User Profile</NavLink></li>
        </ul>
        <Routes>
          <Route path="/user/:name/:email" element={<User />} />
          <Route path="/" element={<Home />} />
        </Routes>
        <HomeButton />
      </div>
    </BrowserRouter>
  );
}

function Home() {
  return <h2>Welcome Home</h2>;
}

function User() {
  let { name, email } = useParams();
  return (
    <h2>Name: {name} <br /> Email: {email}</h2>
  );
}

function HomeButton() {
  const history = useNavigate();

  function handleClick() {
    history("/");
  }

  return (
    <>
      <button type="button" onClick={handleClick}>Go Home</button>
    </>
  );
}
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-usenavigate-j5fkzn?file=/src/App.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. How to perform automatic redirect in React.js?**

In contrast to the Navigate component and its declarative redirect, we can perform a programmatic redirect by using React Router's **useNavigate()** Hook:

**Example:**

```jsx
/**
 * Automatic Redirect in router-v6
 */
import { NavLink, BrowserRouter, Routes, Route, Navigate } from "react-router-dom";

export default function App() {
  return (
    <BrowserRouter>
      <nav style={{ display: "flex", flexDirection: "row", gap: "1em" }}>
        <NavLink to="/" children="Home" />
        <NavLink to="/about" children="About" />
        <NavLink to="/help" children="Help" />
      </nav>
      <Routes>
        <Route index element={<Navigate replace to="home" />} />
        <Route path="home" element={<h1>Home Page</h1>} />
        <Route path="about" element={<h1>About Page</h1>} />
        <Route path="help" element={<h1>Help Page</h1>} />
      </Routes>
    </BrowserRouter>
  );
}
```

*Note: To keep the history clean, you should set `replace` prop. This will avoid extra redirects after the user click back.*

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-automatic-redirect-odw0yn?file=/src/App.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. How to pass additional data while redirecting to a route in React?**

**Using Link:**

**Example:**

```jsx
/**
 * Pass additional data while redirecting
 */
import { BrowserRouter, Link, Route, Routes, useLocation } from "react-router-dom";

/**
 * View User Component
 */
function ViewUser() {
  const location = useLocation();
  return (
    <>
      <h2>User Details</h2>
      <div>Name:{location.state.name}</div>
      <div>Email:{location.state.email}</div>
    </>
  );
}

/**
 * User Component
 */
function User() {
  return (
    <div>
      <h2>Pass additional data while redirecting</h2>
      <Link
        to="/view-user"
        state={{
          name: "Kalini Khalsa",
          email: "kalini.khalsa@email.com"
        }}
      >
        <button>View User</button>
      </Link>
    </div>
  );
}

/**
 * App Component
 */
export default function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route exact path="/" element={<User />} />
        <Route exact path="/user" element={<User />} />
        <Route exact path="/view-user" element={<ViewUser />} />
      </Routes>
    </BrowserRouter>
  );
}
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-pass-data-using-router-br5kdb?file=/src/App.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. How to pass props in React router v6?**

React Router uses a declarative, component-based approach to routing. `Route` allows you to map URL paths to different React components.

**Example:**

```jsx
/**
 * Pass props in React Router-v6
 */
import React from "react";
import { BrowserRouter, Routes, Route, NavLink } from "react-router-dom";

export function Greeting(props) {
  const { text } = props;
  return (
    <>
      <h2>Greetings Page</h2>
      <p>{text}</p>
    </>
  );
}

const RouterExample = () => <h2>Home Page</h2>;

const App = () => (
  <BrowserRouter>
    <ul>
      <li><NavLink to="/">Home</NavLink></li>
      <li><NavLink to="/greeting/pradeep">Greeting</NavLink></li>
    </ul>
    <hr />
    <Routes>
      <Route exact path="/" element={<RouterExample />} />
      <Route path="/greeting/:name" element={<Greeting text="Hello World" />} />
    </Routes>
  </BrowserRouter>
);

export default App;
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-pass-props-in-router-g9zjg4?file=/src/App.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. How to get query parameters in react routing?**

**Using `useParams()`**

**Example:**

```jsx
/**
 * useParams()
 */
import React from "react";
import { BrowserRouter, Route, Routes, Link, useParams } from "react-router-dom";

export default function App() {
  return (
    <BrowserRouter>
      <div>
        <ul>
          <li><Link to="/home">Home</Link></li>
          <li><Link to="/contact-us">Contact Us</Link></li>
          <li><Link to="/help">Help</Link></li>
        </ul>
        <Routes>
          <Route path="/:id" element={<Child />} />
        </Routes>
      </div>
    </BrowserRouter>
  );
}

function Child() {
  // `useParams` hook used here to access parameters
  let { id } = useParams();

  return <h2>Parameter: {id}</h2>;
}
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-get-query-parameters-ngsm3l?file=/src/App.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. What is the difference between HashRouter and BrowserRouter in React?**

**1. BrowserRouter:**

- The widely popular router and a router for modern browsers which user HTML5 pushState API. (i.e. `pushState`, `replaceState` and `popState` API).
- It routes as normal URL in browser, you can't differentiate whether it is server rendered page or client rendered page through the URL.
- It assumes, your server handles all the request URL (eg., `/`, `/about`) and points to root `index.html`. From there, BrowserRouter take care of routing the relevant page.
- It accepts `forceRefresh` props to support legacy browsers which doesn't support HTML5 pushState API

**Syntax:**

```jsx
/**
 * https://example.com/home
 * https://example.com/about
 */

<BrowserRouter
  basename={optionalString}
  forceRefresh={optionalBool}
  getUserConfirmation={optionalFunc}
  keyLength={optionalNumber}
>
  <App />
</BrowserRouter>
```

**Example:**

```jsx
/**
 * BrowserRouter()
 */
import { Link, BrowserRouter, Routes, Route } from "react-router-dom";

const HomePage = () => {
  return <h2>Home Page</h2>;
};

const AboutPage = () => {
  return <h2>About Page</h2>;
};

export default function App() {
  return (
    <section className="App">
      <BrowserRouter>
        <ul>
          <li><Link to="/home">Home</Link></li>
          <li><Link to="/about">About</Link></li>
        </ul>
        <Routes>
          <Route exact path="/home" element={<HomePage />} />
          <Route exact path="/about" element={<AboutPage />} />
        </Routes>
      </BrowserRouter>
    </section>
  );
}
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-browserrouter-53zjvx?file=/src/App.js)**

**2. HashRouter:**

- A router which uses client side hash routing.
- Whenever, there is a new route get rendered, it updated the browser URL with hash routes. (eg., `/#/about`)
- Hash portion of the URL won't be handled by server, server will always send the `index.html` for every request and ignore hash value. Hash value will be handled by react router.
- It is used to support legacy browsers which usually doesn't support HTML `pushState` API

**Syntax:**

```jsx
/**
 * https://example.com/#/home
 * https://example.com/#/about
 */

<HashRouter
  basename={optionalString}
  getUserConfirmation={optionalFunc}
  hashType={optionalString}
>
  <App />
</HashRouter>
```

**Example:**

```jsx
/**
 * HashRouter()
 */
import { Link, HashRouter, Routes, Route } from "react-router-dom";

const HomePage = () => {
  return <h2>Home Page</h2>;
};

const AboutPage = () => {
  return <h2>About Page</h2>;
};

export default function App() {
  return (
    <section className="App">
      <HashRouter>
        <ul>
          <li><Link to="/home">Home</Link></li>
          <li><Link to="/about">About</Link></li>
        </ul>
        <Routes>
          <Route exact path="/home" element={<HomePage />} />
          <Route exact path="/about" element={<AboutPage />} />
        </Routes>
      </HashRouter>
    </section>
  );
}
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-hashrouter-pcn4dj?file=/src/App.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics#table-of-contents)**

**Q. What is route based code splitting?**

Route based code splitting is essential during the page transitions on the web, which takes some amount of time to load. Here is an example of how to setup route-based code splitting into the app using React Router with `React.lazy`.

**Example:**

```jsx
/**
 * Lazy Loading
 */
import React, { Suspense, lazy } from "react";
import { BrowserRouter, Routes, Route } from "react-router-dom";

const Home = lazy(() => import("./Home"));
const About = lazy(() => import("./About"));

export default function App() {
  return (
    <BrowserRouter>
      <Suspense fallback={<div>Loading...</div>}>
        <Routes>
          <Route exact path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
        </Routes>
      </Suspense>
    </BrowserRouter>
  );
}
```



# Q.56 REACT REFS
**Q. What do you understand by refs in React?**

The **Refs** provide a way to access DOM nodes or React elements created in the render method. React `Refs` are a useful feature that act as a means to reference a DOM element or a class component from within a parent component.

Refs also provide some flexibility for referencing elements within a child component from a parent component, in the form of **ref forwarding**.

**Example:**

```jsx
/**
 * Refs
 */
class App extends React.Component {
    constructor(props) {
      super(props)
      // create a ref to store the textInput DOM element
      this.textInput = React.createRef()
      this.state = {
        value: ''
      }
    }

  // Set the state for the ref
  handleSubmit = e => {
    e.preventDefault()
    this.setState({ value: this.textInput.current.value })
  }

  render() {
    return (
      <div>
        <h1>React Ref - createRef</h1>
         {/** This is what will update **/}
        <h3>Value: {this.state.value}</h3>
        <form onSubmit={this.handleSubmit}>
          {/** Call the ref on <input> so we can use it to update the <h3> value **/}
          <input type="text" ref={this.textInput} />
          <button>Submit</button>
        </form>
      </div>
    )
  }
}
```

**When to Use Refs:**

- Managing focus, text selection, or media playback.
- Triggering imperative animations.
- Integrating with third-party DOM libraries.

**When not to use refs:**

- Should not be used with functional components because they dont have instances.
- Not to be used on things that can be done declaritvely.

**[↥ back to top](https://github.com/learning-zone/react-basics?tab=readme-ov-file#table-of-contents)**

**Q. How can I use multiple refs for an array of elements with hooks?**

**Example:**

```jsx
/**
 * Multiple Refs
 */
import React, { useRef } from "react";

export default function App() {
  const arr = [10, 20, 30];
  // multiple refs
  const refs = useRef([]);

  return (
    <div>
      {arr.map((item, index) => {
        return (
          <div
            key={index}
            ref={(element) => {
              refs.current[index] = element;
            }}
          >
            {item}
          </div>
        );
      })}
    </div>
  );
}
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-multiple-refs-z2wqm?file=/src/App.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics?tab=readme-ov-file#table-of-contents)**

**Q. What is the difference between useRef() and createRef()?**

**1. useRef():**

The useRef is a hook that uses the same ref throughout. It saves its value between re-renders in a functional component and doesn't create a new instance of the ref for every re-render. It persists the existing ref between re-renders.

**Example:**

```jsx
/**
 * useRef()
 */
export default function App() {
  const [count, setCount] = useState(0);
  const ref = useRef();

  useEffect(() => {
    ref.current = "SomeInitialValue";
  }, []);

  useEffect(() => {
    console.log(count, ref.current);
  }, [count]);

  return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>Increment</button>
      <p>{count}</p>
    </div>
  );
}
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-useref-44wfd?file=/src/App.js)**

**2. createRef():**

The createRef is a function that creates a new ref every time. Unlike the useRef, it does not save its value between re-renders, instead creates a new instance of the ref for every re-render. Thus implying that it does not persist the existing ref between re-renders.

**Example:**

```jsx
/**
 * createRef()
 */
export default function App() {
  const [count, setCount] = useState(0);
  const ref = createRef();

  useEffect(() => {
    ref.current = "SomeInitialValue";
  }, []);

  useEffect(() => {
    console.log(count, ref.current);
  }, [count]);

  return (
    <div className="App">
      <button onClick={() => setCount((c) => c + 1)}>Increment</button>
      <p>{count}</p>
    </div>
  );
}
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-createref-pgu2x?file=/src/App.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics?tab=readme-ov-file#table-of-contents)**

**Q. Why are inline ref callback or function not recommended?**

If **ref callback** is defined as an inline function, it will get called twice during updates, first with `null` and then again with the DOM element. This is because a new instance of the function is created with each render, so React needs to clear the old ref and set up the new one.

**Example:**

```jsx
/**
 * Inline Ref Callback()
 */
import React from "react";

export default class App extends React.Component {
  handleSubmit = (e) => {
    e.preventDefault();
    console.log("Input Value is: " + this.input.value);
  };
  render() {
    return (
      <form onSubmit={(e) => this.handleSubmit(e)}>
        <input type="text" ref={(input) => (this.input = input)} />
        <button type="submit">Submit</button>
      </form>
    );
  }
}
```

Here, When the `<input>` element is rendered, React calls the function defined in the ref attribute, passing that function the `<input>` element as an argument.

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-ref-callback-6ry5o?file=/src/App.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics?tab=readme-ov-file#table-of-contents)**

**Q. Which is the preferred option callback refs or findDOMNode()?**

It is preferred to use **callback refs** over `findDOMNode()` API. Because `findDOMNode()` prevents certain improvements in React in the future.

The legacy approach of using `findDOMNode()`:

```jsx
class MyComponent extends Component {
  componentDidMount() {
    findDOMNode(this).scrollIntoView()
  }

  render() {
    return <div />
  }
}
```

The recommended approach is:

```jsx
class MyComponent extends Component {
  componentDidMount() {
    this.node.scrollIntoView()
  }

  render() {
    return <div ref={node => this.node = node} />
  }
}
```

**[↥ back to top](https://github.com/learning-zone/react-basics?tab=readme-ov-file#table-of-contents)**

**Q. How to set focus on an input field after rendering?**

Refs can be used to access DOM nodes or React components that are rendered in the render method. Refs are created with `React.createRef()` function. Refs can then be assigned to an element with ref-attribute. Following example shows a component that will focus to the text input when rendered.

```jsx
class AutoFocusTextInput extends React.Component {

  constructor(props) {
    super(props)
    this.textInput = React.createRef()
  }
  componentDidMount() {
    this.textInput.current.focus()
  }
  render() {
    return <input ref={this.textInput} />
  }
}
```

**[↥ back to top](https://github.com/learning-zone/react-basics?tab=readme-ov-file#table-of-contents)**

**Q. Why are string refs considered legacy in React?**

> Although string refs are not deprecated, they are considered legacy, and will likely be deprecated at some point in the future. Callback refs are preferred.
> 

**Callback Refs:**

Instead of passing a **ref** attribute created by `createRef()`, you pass a function. The function receives the React component instance or HTML DOM element as its argument, which can be stored and accessed elsewhere.

**Example:**

```jsx
// Ref.js

class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    this.textInput = null;

    this.setTextInputRef = (element) => {
      this.textInput = element;
    };
  }

  handleSubmit = (e) => {
    e.preventDefault();
    console.log(this.textInput.value);
  };

  render() {
    return (
      <div>
        <form onSubmit={(e) => this.handleSubmit(e)}>
          <input type="text" ref={this.setTextInputRef} />
          <button>Submit</button>
        </form>
      </div>
    );
  }
}
```

```jsx
// App.js

const App = () => (
  <div style={styles}>
    <Hello name="React Refs" />
    <CustomText />
  </div>
)
```

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-refs-hiw59?file=/src/index.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics?tab=readme-ov-file#table-of-contents)**

**Q. What is `forwardRef()` in React?**

Ref forwarding is a technique for passing a `ref` through a component to one of its children. It is very useful for cases like reusable component libraries and Higher Order Components (HOC).

We can forward a `ref` to a component by using the `React.forwardRef()` function. Ref forwarding allows components to take a ref they receive and pass it further down (in other words, "forward" it) to a child.

**Example:**

```jsx
// Ref.js
const TextInput = React.forwardRef((props, ref) => (
  <input type="text" placeholder="Hello World" ref={ref} />
))

const inputRef = React.createRef()

class CustomTextInput extends React.Component {
  handleSubmit = e => {
    e.preventDefault()
    console.log(inputRef.current.value)
  }

  render() {
    return (
      <div>
        <form onSubmit={e => this.handleSubmit(e)}>
          <TextInput ref={inputRef} />
          <button>Submit</button>
        </form>
      </div>
    )
  }
}
```

In the example above, we have a component called TextInput that has a child which is an input field. First, we start by creating a ref with the line of code below:

```jsx
const inputRef = React.createRef()
```

We pass our ref down to `<TextInput ref={inputRef}>` by specifying it as a JSX attribute. React then forwards the `ref` to the `forwardRef()` function as a second argument. Next, We forward this `ref` argument down to `<input ref={ref}>`. The value of the DOM node can now be accessed at `inputRef.current`.

**[↥ back to top](https://github.com/learning-zone/react-basics?tab=readme-ov-file#table-of-contents)**

**Q. How to debug forwardRefs() in DevTools?**

**React.forwardRef** accepts a render function as parameter and DevTools uses this function to determine what to display for the ref forwarding component.

**Problem:** If you don't name the render function or not using displayName property then it will appear as "ForwardRef" in the DevTools,

```jsx
const WrappedComponent = React.forwardRef((props, ref) => {
  return <LogProps {...props} forwardedRef={ref} />;
});
```

**Solution:** If you name the render function then it will appear as "ForwardRef(myFunction)"

```jsx
const WrappedComponent = React.forwardRef(function myFunction(props, ref) {
  return <LogProps {...props} forwardedRef={ref} />;
});
```

**Example:**

```jsx
const ForwardP = React.forwardRef(function ForwardP(props, ref) {
  return (
    <>
      <p>I'm a real component too</p>
      <p>
        Especially with <code>useImperativeMethods</code>
      </p>
      <p {...props} ref={ref} />
    </>
  );
});

function App() {
  return (
    <div className="App">
      <ForwardP style={{ opacity: 0.5 }}>
        But my props are <code>null</code> in DevTools
      </ForwardP>
    </div>
  );
}
```

!https://github.com/learning-zone/react-basics/raw/master/assets/forwardRef.png

**⚝ [Try this example on CodeSandbox](https://codesandbox.io/s/react-forwardref-ccqgu?file=/src/index.js)**

**[↥ back to top](https://github.com/learning-zone/react-basics?tab=readme-ov-file#table-of-contents)**

**Q. What is difference between useRef() and useState() in React?**

*ToDo*

**[↥ back to top](https://github.com/learning-zone/react-basics?tab=readme-ov-file#table-of-contents)**

**# 16. REACT COMPOSITION**

**Q. Explain Inheritance in React?**

Inheritance uses the keyword **extends** to allow any component to use the properties and methods of another component connected with the parent. A class that is used as the basis for inheritance is called a superclass or base class. A class that inherits from a superclass is called a subclass or derived class.

Using the **extends** keyword, it allows the current component to access all the component's properties, including the function, and trigger it from the child component.

**Example:**

```jsx
import React from "react";

/**
 * Parent Class
 */
export class ParentClass extends React.Component {
  constructor(props) {
    super(props);
    this.callMe = this.callMe.bind(this);
  }

  // ParentClass function
  callMe() {
    console.log("This is a method from parent class");
  }

  render() {
    return false;
  }
}

/**
 * Child Class
 */
export default class App extends ParentClass {
  render() {
    return <button onClick={() => this.callMe()}>Call Parent</button>;
  }
}

```


<br> 

## Q.57 what is the use of arrow functions ? 
Arrow functions are often used for event handling and callbacks in React. They provide a more concise and cleaner way to define these functions, making the code easier to manage.


<br> 

## Q.58 what is the difference between .js and .jsx file in reactjs 
In React.js, the file extension `.js` and `.jsx` are used to denote JavaScript files. The difference is mainly a convention used to distinguish regular JavaScript files from JSX (JavaScript XML) files.

1. **.js Extension:**
    - Files with a `.js` extension typically contain regular JavaScript code.
    - React components can be written in these files using regular JavaScript syntax without JSX.
    
    ```jsx
    // Example React component in a .js file
    import React from 'react';
    
    const MyComponent = () => {
      return <div>Hello, React!</div>;
    };
    
    export default MyComponent;
    
    ```
    
2. **.jsx Extension:**
    - Files with a `.jsx` extension are used when React components are written using JSX syntax.
    - JSX is a syntax extension for JavaScript that looks similar to XML or HTML and allows developers to write React components more concisely.
    
    ```jsx
    // Example React component in a .jsx file
    import React from 'react';
    
    const MyComponent = () => {
      return <div>Hello, React!</div>;
    };
    
    export default MyComponent;
    
    ```
    

In summary, the choice between `.js` and `.jsx` is mainly a matter of convention and helps developers and tools recognize files that contain JSX code. Both file types can be used to write React components, and the actual syntax within the file determines whether it is using regular JavaScript or JSX. Many projects use `.jsx` for files containing JSX to make it clear that JSX syntax is being used, but it's not strictly required by React.




<br> 

## Q.59 what is the difference between class components and functional component in reactjs 
In React.js, there are two main types of components: class components and functional components. Here are the key differences between them:

1. **Syntax:**
    - **Class Components:**
        - Defined using ES6 class syntax.
        - Extends `React.Component` or a custom base class.
        - Contains a `render` method that returns the JSX structure.
        
        ```jsx
        import React, { Component } from 'react';
        
        class MyClassComponent extends Component {
          render() {
            return <div>Hello, React!</div>;
          }
        }
        
        export default MyClassComponent;
        
        ```
        
    - **Functional Components:**
        - Defined using JavaScript functions.
        - Typically simpler and more concise.
        - Introduced with React Hooks (starting from React 16.8) to manage state and lifecycle features in functional components.
        
        ```jsx
        import React from 'react';
        
        const MyFunctionalComponent = () => {
          return <div>Hello, React!</div>;
        };
        
        export default MyFunctionalComponent;
        
        ```
        
2. **State and Lifecycle:**
    - **Class Components:**
        - Can have state using `this.state` and manage lifecycle methods (e.g., `componentDidMount`, `componentDidUpdate`, etc.).
        - Historically, class components were the primary way to use state and lifecycle methods.
    - **Functional Components:**
        - Before the introduction of Hooks, functional components were stateless.
        - With Hooks, functional components can use `useState` for local state and other hooks for managing lifecycle and side effects.
3. **Performance:**
    - **Class Components:**
        - Slightly heavier in terms of memory usage and performance.
        - React class components have some additional overhead.
    - **Functional Components:**
        - Generally considered more lightweight and easier to optimize.
        - With the introduction of Hooks, functional components can have similar capabilities to class components.
4. **Readability and Conciseness:**
    - **Class Components:**
        - May require more boilerplate code.
        - The syntax can be more verbose.
    - **Functional Components:**
        - Typically more concise and easier to read.
        - The introduction of Hooks reduced the need for class components in many cases.
5. **Usage of `this`:**
    - **Class Components:**
        - Uses `this` to access props and state within class methods.
    - **Functional Components:**
        - Accesses props directly as function parameters.
        - Uses the `useState` and other hooks to manage state without using `this`.

With the introduction of Hooks, functional components have become more powerful and are now the recommended way to write components in React. They provide a more concise and modern syntax while offering similar capabilities to class components. However, class components are still valid and supported in React. The choice between them often depends on the specific requirements of your project and your team's preferences.


<br> 


## Q.60 difference between props and state
In React.js, both props and state are fundamental concepts, but they serve different purposes.

1. **Props (Properties):**
    - **Immutable:** Props are passed from parent to child components and are immutable. Once set by the parent, they cannot be modified by the child component.
    - **Function Parameters:** You can think of props as the parameters that a parent component passes to its child components. They provide a way for the parent component to communicate with its children.
    - **Read-Only:** Child components should not modify their props; they only receive and use them.
    - **External Control:** Props are how components receive data from their parent components, making them a way to control and configure child components.
    
    Example:
    
    ```jsx
    // Parent Component
    function ParentComponent() {
      const data = "Hello from parent!";
      return <ChildComponent message={data} />;
    }
    
    // Child Component
    function ChildComponent(props) {
      return <div>{props.message}</div>;
    }
    
    ```
    
2. **State:**
    - **Mutable:** Unlike props, state is mutable and is used to represent the internal state of a component. It can be changed by the component itself using `setState`.
    - **Local to Component:** State is specific to a component and is not passed down to child components by default.
    - **Used for Interactivity:** State is commonly used to handle user interactions, input changes, and to trigger re-renders of the component when the state changes.
    - **Declared in Constructor:** State is initialized in the component's constructor.
    
    Example:
    
    ```jsx
    class Counter extends React.Component {
      constructor(props) {
        super(props);
        this.state = {
          count: 0
        };
      }
    
      increment = () => {
        this.setState({ count: this.state.count + 1 });
      };
    
      render() {
        return (
          <div>
            <p>Count: {this.state.count}</p>
            <button onClick={this.increment}>Increment</button>
          </div>
        );
      }
    }
    
    ```
    

In summary, props are used for passing data from parent to child components in a unidirectional flow, and they are immutable. State, on the other hand, is used to manage a component's internal state, and it is mutable, allowing the component to re-render based on changes to its state.


<br> 


## Q.61 In which scenario we need to write the custom hook? 
Custom hooks in React are a way to reuse stateful logic across different components. They allow you to extract and share logic in a modular and reusable way. Here are some scenarios in which you might want to write a custom hook:

1. **Reuse Logic Across Components:**
If you find yourself duplicating code in multiple components, it might be a good idea to create a custom hook to encapsulate that logic. This promotes code reuse and helps maintain a clean and DRY (Don't Repeat Yourself) codebase.
    
    ```jsx
    // Example: useLocalStorage hook
    import { useState } from 'react';
    
    function useLocalStorage(key, initialValue) {
      const [value, setValue] = useState(() => {
        const storedValue = localStorage.getItem(key);
        return storedValue !== null ? JSON.parse(storedValue) : initialValue;
      });
    
      const setStoredValue = (newValue) => {
        setValue(newValue);
        localStorage.setItem(key, JSON.stringify(newValue));
      };
    
      return [value, setStoredValue];
    }
    
    ```
    
2. **Abstract Complex Logic:**
If you have complex logic within a component, moving it to a custom hook can make your component code more readable and focused on the UI concerns.
    
    ```jsx
    // Example: useValidation hook
    import { useState } from 'react';
    
    function useValidation(initialValue, validationFn) {
      const [value, setValue] = useState(initialValue);
      const [error, setError] = useState('');
    
      const handleChange = (newValue) => {
        setValue(newValue);
        const validationResult = validationFn(newValue);
        setError(validationResult);
      };
    
      return [value, error, handleChange];
    }
    
    ```
    
3. **Handle Lifecycle Events:**
Custom hooks can encapsulate logic related to component lifecycle events, such as mounting, updating, and unmounting. This can be useful for managing subscriptions, timers, or other side effects.
    
    ```jsx
    // Example: useInterval hook
    import { useEffect, useRef } from 'react';
    
    function useInterval(callback, delay) {
      const savedCallback = useRef();
    
      useEffect(() => {
        savedCallback.current = callback;
      }, [callback]);
    
      useEffect(() => {
        function tick() {
          savedCallback.current();
        }
    
        if (delay !== null) {
          const id = setInterval(tick, delay);
          return () => clearInterval(id);
        }
      }, [delay]);
    }
    
    ```
    
4. **Accessing Context or Redux State:**
If you need to access context values or state managed by Redux, custom hooks can provide a clean abstraction for obtaining that data.
    
    ```jsx
    // Example: useAuth hook
    import { useContext } from 'react';
    import AuthContext from './AuthContext';
    
    function useAuth() {
      const authContext = useContext(AuthContext);
      return authContext;
    }
    
    ```
    

Remember that custom hooks should follow the naming convention of starting with "use" to indicate that they are hooks. Additionally, they can use other hooks if needed. Custom hooks make it easier to share and manage complex logic across different parts of your application.



<br> 


## Q.62 What is SSR ? (Server side rendering) 
SSR, short for Server-Side Rendering, is **a technique in web development where the webpage's content is rendered on the server instead of the client's browser**.

Server-Side Rendering (SSR) is a technique used in web development where the server, rather than the client's browser, generates the initial HTML for a web page. In a traditional client-side rendering (CSR) approach, the browser downloads a minimal HTML file and then JavaScript is executed to fetch data and render the page on the client side. With SSR, the server pre-renders the HTML content and sends a fully-rendered page to the client.

Here are some key aspects of Server-Side Rendering:

1. **Initial Page Load:**
    - In SSR, when a user requests a page, the server processes the request and generates the HTML content of the page on the server.
    - The fully-rendered HTML is then sent to the client's browser as part of the response.
2. **Faster Time to First Paint:**
    - SSR can lead to a faster Time to First Paint (TTFP) because the user receives a fully-rendered page from the server. This can improve the perceived performance of the web application.
3. **Improved SEO:**
    - Search engines often prefer pages with content that is readily available in the HTML source code. SSR can improve search engine optimization (SEO) as the server sends a complete HTML page containing the content.
4. **Progressive Enhancement:**
    - SSR is often used in conjunction with client-side rendering frameworks like React, Vue, or Angular. The server sends a fully-rendered page for the initial load, and then the client-side JavaScript takes over for subsequent interactions, providing a seamless and interactive user experience.
5. **Reduced Client-Side Rendering Load:**
    - SSR can offload some of the rendering responsibilities from the client's browser. This can be beneficial for devices with limited processing power, especially on the initial page load.
6. **Challenges:**
    - SSR introduces additional server-side processing, potentially increasing server load.
    - Server-side rendering can be more complex to set up and manage compared to client-side rendering.
    - Real-time updates and interactivity may require additional considerations.

Popular frameworks like Next.js (for React), Nuxt.js (for Vue), and Angular Universal (for Angular) provide built-in support for server-side rendering. These frameworks simplify the process of implementing SSR and address some of the challenges associated with it.


<br> 


## Q.62 what is composition in reactjs 
Composition in React refers to the concept of combining or nesting components to create more complex UI structures. It's one of the core principles of building React applications, and it promotes a modular and reusable approach to building user interfaces.

There are two primary forms of composition in React:

1. **Component Composition:**
    - **Definition:** Component composition involves creating new components by combining or nesting existing components.
    - **Advantages:**
        - **Reusability:** Components can be reused in different parts of the application, promoting a modular and maintainable codebase.
        - **Abstraction:** Components can encapsulate specific functionality or UI elements, allowing for better abstraction and separation of concerns.
    - **Example:**
        
        ```jsx
        // Example of Component Composition
        import React from 'react';
        
        const Button = ({ onClick, label }) => (
          <button onClick={onClick}>{label}</button>
        );
        
        const Card = ({ title, content }) => (
          <div>
            <h2>{title}</h2>
            <p>{content}</p>
          </div>
        );
        
        const App = () => (
          <div>
            <Card title="Card Title" content="Card Content" />
            <Button onClick={() => console.log('Button clicked')} label="Click me" />
          </div>
        );
        
        ```
        
2. **HOC (Higher-Order Component) Composition:**
    - **Definition:** Higher-Order Components are functions that take a component and return a new component with enhanced or additional functionality.
    - **Advantages:**
        - **Code Reusability:** Logic can be shared among multiple components without duplicating code.
        - **Abstraction:** Common functionality can be abstracted into HOCs, making components more focused on their specific responsibilities.
    - **Example:**
        
        ```jsx
        // Example of HOC Composition
        import React from 'react';
        
        // Higher-Order Component (HOC)
        const withLogging = (WrappedComponent) => {
          return class WithLogging extends React.Component {
            componentDidMount() {
              console.log('Component is mounted');
            }
        
            render() {
              return <WrappedComponent {...this.props} />;
            }
          };
        };
        
        // Original Component
        const MyComponent = ({ name }) => <div>Hello, {name}!</div>;
        
        // Component enhanced with HOC
        const EnhancedComponent = withLogging(MyComponent);
        
        // Using the enhanced component
        const App = () => <EnhancedComponent name="John" />;
        
        ```
        
    - In the example above, the `withLogging` HOC adds a `componentDidMount` lifecycle method to log a message when the component is mounted. The `EnhancedComponent` is the original `MyComponent` enhanced with this logging functionality.

Composition is a powerful concept in React that enables developers to build scalable and maintainable applications by creating reusable components and combining them to construct more complex UIs. It fosters a modular and flexible architecture.


<br> 


## Q.63 COMPONENT LIFECYCLE METHOD
# Lifecycle of Components

Each component in React has a lifecycle which you can monitor and manipulate during its three main phases.

The three phases are: **Mounting**, **Updating**, and **Unmounting**.

---

# Mounting

Mounting means putting elements into the DOM.

React has four built-in methods that gets called, in this order, when mounting a component:

1. `constructor()`
2. `getDerivedStateFromProps()`
3. `render()`
4. `componentDidMount()`

The `render()` method is required and will always be called, the others are optional and will be called if you define them.

---

# constructor

The `constructor()` method is called before anything else, when the component is initiated, and it is the natural place to set up the initial `state` and other initial values.

The `constructor()` method is called with the `props`, as arguments, and you should always start by calling the `super(props)` before anything else, this will initiate the parent's constructor method and allows the component to inherit methods from its parent (`React.Component`).

# Example:[Get your own React.js Server](https://www.w3schools.com/react/react_server.asp)

The `constructor` method is called, by React, every time you make a component:

```jsx
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  render() {
    return (
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>);
  }
}

ReactDOM.render(<Header />, document.getElementById('root'));

```

[Run Example »](https://www.w3schools.com/react/showreact.asp?filename=demo2_react_lifecycle_constructor)

---

# getDerivedStateFromProps

The `getDerivedStateFromProps()` method is called right before rendering the element(s) in the DOM.

This is the natural place to set the `state` object based on the initial `props`.

It takes `state` as an argument, and returns an object with changes to the `state`.

The example below starts with the favorite color being "red", but the `getDerivedStateFromProps()` method updates the favorite color based on the `favcol` attribute:

# Example:

The `getDerivedStateFromProps` method is called right before the render method:

```jsx
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  static getDerivedStateFromProps(props, state) {
    return {favoritecolor: props.favcol };
  }
  render() {
    return (
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>);
  }
}

ReactDOM.render(<Header favcol="yellow"/>, document.getElementById('root'));

```

[Run Example »](https://www.w3schools.com/react/showreact.asp?filename=demo2_react_lifecycle_getderivedstatefromprops)

---

# render

The `render()` method is required, and is the method that actually outputs the HTML to the DOM.

# Example:

A simple component with a simple `render()` method:

```jsx
class Header extends React.Component {
  render() {
    return (
      <h1>This is the content of the Header component</h1>);
  }
}

ReactDOM.render(<Header />, document.getElementById('root'));

```

[Run Example »](https://www.w3schools.com/react/showreact.asp?filename=demo2_react_lifecycle_render)

---

# componentDidMount

The `componentDidMount()` method is called after the component is rendered.

This is where you run statements that requires that the component is already placed in the DOM.

# Example:

At first my favorite color is red, but give me a second, and it is yellow instead:

```jsx
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  componentDidMount() {
    setTimeout(() => {
      this.setState({favoritecolor: "yellow"})
    }, 1000)
  }
  render() {
    return (
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>);
  }
}

ReactDOM.render(<Header />, document.getElementById('root'));

```

[Run Example »](https://www.w3schools.com/react/showreact.asp?filename=demo2_react_lifecycle_componentdidmount)

---

# Updating

The next phase in the lifecycle is when a component is *updated*.

A component is updated whenever there is a change in the component's `state` or `props`.

React has five built-in methods that gets called, in this order, when a component is updated:

1. `getDerivedStateFromProps()`
2. `shouldComponentUpdate()`
3. `render()`
4. `getSnapshotBeforeUpdate()`
5. `componentDidUpdate()`

The `render()` method is required and will always be called, the others are optional and will be called if you define them.

---

# getDerivedStateFromProps

Also at *updates* the `getDerivedStateFromProps` method is called. This is the first method that is called when a component gets updated.

This is still the natural place to set the `state` object based on the initial props.

The example below has a button that changes the favorite color to blue, but since the `getDerivedStateFromProps()` method is called, which updates the state with the color from the favcol attribute, the favorite color is still rendered as yellow:

# Example:

If the component gets updated, the `getDerivedStateFromProps()` method is called:

```jsx
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  static getDerivedStateFromProps(props, state) {
    return {favoritecolor: props.favcol };
  }
  changeColor = () => {
    this.setState({favoritecolor: "blue"});
  }
  render() {
    return (
      <div>
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>
      <button type="button" onClick={this.changeColor}>Change color</button>
      </div>);
  }
}

ReactDOM.render(<Header favcol="yellow"/>, document.getElementById('root'));

```

[Run Example »](https://www.w3schools.com/react/showreact.asp?filename=demo2_react_lifecycle_getderivedstatefromprops2)

---

# shouldComponentUpdate

In the `shouldComponentUpdate()` method you can return a Boolean value that specifies whether React should continue with the rendering or not.

The default value is `true`.

The example below shows what happens when the `shouldComponentUpdate()` method returns `false`:

# Example:

Stop the component from rendering at any update:

```jsx
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  shouldComponentUpdate() {
    return false;
  }
  changeColor = () => {
    this.setState({favoritecolor: "blue"});
  }
  render() {
    return (
      <div>
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>
      <button type="button" onClick={this.changeColor}>Change color</button>
      </div>);
  }
}

ReactDOM.render(<Header />, document.getElementById('root'));

```

[Run Example »](https://www.w3schools.com/react/showreact.asp?filename=demo2_react_lifecycle_shouldcomponentupdate)

# Example:

Same example as above, but this time the `shouldComponentUpdate()` method returns `true` instead:

```jsx
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  shouldComponentUpdate() {
    return true;
  }
  changeColor = () => {
    this.setState({favoritecolor: "blue"});
  }
  render() {
    return (
      <div>
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>
      <button type="button" onClick={this.changeColor}>Change color</button>
      </div>);
  }
}

ReactDOM.render(<Header />, document.getElementById('root'));

```

[Run Example »](https://www.w3schools.com/react/showreact.asp?filename=demo2_react_lifecycle_shouldcomponentupdate2)

---

# render

The `render()` method is of course called when a component gets *updated*, it has to re-render the HTML to the DOM, with the new changes.

The example below has a button that changes the favorite color to blue:

# Example:

Click the button to make a change in the component's state:

```jsx
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  changeColor = () => {
    this.setState({favoritecolor: "blue"});
  }
  render() {
    return (
      <div>
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>
      <button type="button" onClick={this.changeColor}>Change color</button>
      </div>);
  }
}

ReactDOM.render(<Header />, document.getElementById('root'));

```

[Run Example »](https://www.w3schools.com/react/showreact.asp?filename=demo2_react_lifecycle_render2)

---

# getSnapshotBeforeUpdate

In the `getSnapshotBeforeUpdate()` method you have access to the `props` and `state` *before* the update, meaning that even after the update, you can check what the values were *before* the update.

If the `getSnapshotBeforeUpdate()` method is present, you should also include the `componentDidUpdate()` method, otherwise you will get an error.

The example below might seem complicated, but all it does is this:

When the component is *mounting* it is rendered with the favorite color "red".

When the component *has been mounted,* a timer changes the state, and after one second, the favorite color becomes "yellow".

This action triggers the *update* phase, and since this component has a `getSnapshotBeforeUpdate()` method, this method is executed, and writes a message to the empty DIV1 element.

Then the `componentDidUpdate()` method is executed and writes a message in the empty DIV2 element:

# Example:

Use the `getSnapshotBeforeUpdate()` method to find out what the `state` object looked like before the update:

```jsx
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
}componentDidMount() {
    setTimeout(() => {
      this.setState({favoritecolor: "yellow"})
    }, 1000)
}getSnapshotBeforeUpdate(prevProps, prevState) {
    document.getElementById("div1").innerHTML =
    "Before the update, the favorite was " + prevState.favoritecolor;
  }
  componentDidUpdate() {
    document.getElementById("div2").innerHTML =
    "The updated favorite is " + this.state.favoritecolor;
}render() {
    return (
      <div>
        <h1>My Favorite Color is {this.state.favoritecolor}</h1>
        <div id="div1"></div>
        <div id="div2"></div>
      </div>);
}}

ReactDOM.render(<Header />, document.getElementById('root'));

```

[Run Example »](https://www.w3schools.com/react/showreact.asp?filename=demo2_react_lifecycle_getsnapshotbeforeupdate)

---

# componentDidUpdate

The `componentDidUpdate` method is called after the component is updated in the DOM.

The example below might seem complicated, but all it does is this:

When the component is *mounting* it is rendered with the favorite color "red".

When the component *has been mounted,* a timer changes the state, and the color becomes "yellow".

This action triggers the *update* phase, and since this component has a `componentDidUpdate` method, this method is executed and writes a message in the empty DIV element:

# Example:

The `componentDidUpdate` method is called after the update has been rendered in the DOM:

```jsx
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  componentDidMount() {
    setTimeout(() => {
      this.setState({favoritecolor: "yellow"})
    }, 1000)
  }
  componentDidUpdate() {
    document.getElementById("mydiv").innerHTML =
    "The updated favorite is " + this.state.favoritecolor;
  }
  render() {
    return (
      <div>
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>
      <div id="mydiv"></div>
      </div>);
  }
}

ReactDOM.render(<Header />, document.getElementById('root'));

```

[Run Example »](https://www.w3schools.com/react/showreact.asp?filename=demo2_react_lifecycle_componentdidupdate)

---

# Unmounting

The next phase in the lifecycle is when a component is removed from the DOM, or *unmounting* as React likes to call it.

React has only one built-in method that gets called when a component is unmounted:

- `componentWillUnmount()`

---

# componentWillUnmount

The `componentWillUnmount` method is called when the component is about to be removed from the DOM.

# Example:

Click the button to delete the header:

```jsx
class Container extends React.Component {
  constructor(props) {
    super(props);
    this.state = {show: true};
  }
  delHeader = () => {
    this.setState({show: false});
  }
  render() {
    let myheader;
    if (this.state.show) {
      myheader = <Child />;
    };
    return (
      <div>
      {myheader}
      <button type="button" onClick={this.delHeader}>Delete Header</button>
      </div>);
  }
}

class Child extends React.Component {
  componentWillUnmount() {
    alert("The component named Header is about to be unmounted.");
  }
  render() {
    return (
      <h1>Hello World!</h1>);
  }
}

ReactDOM.render(<Container />, document.getElementById('root'));
```



<br> 

## Q.64 REACT FORWARD REF
In React, the **`forwardRef`** function is a utility that allows you to forward a **`ref`** from a parent component to a child component, even if the child component is a functional component. This is particularly useful when you need to access or manipulate the child component's DOM node directly.

App.js 

```jsx
import logo from "./logo.svg";
import "./App.css";
import { useEffect, useRef } from "react";
import Input from "./components/Input";
function App() {
  const firstnameRef = useRef(null);
  const lastnameRef = useRef(null);
  const btnRef = useRef(null);

  useEffect(() => {
    firstnameRef.current.focus();
  }, []);
  const handleFirstname = (e) => {
    // console.log(e.key);
    if (e.key === "Enter") {
      lastnameRef.current.focus();
    }
  };
  const handleLastname = (e) => {
    // console.log(e.key);
    if (e.key === "Enter") {
      btnRef.current.focus();
    }
  };

  const handleBtn = (e) => {
    if (e.key === "Enter") {
      alert("submitted");
    }
  };
  return (
    <div className="App">
      <Input
        ref={firstnameRef}
        onKeyDown={handleFirstname}
        placeholder="enter firstname"
      />
      <br />
      <Input
        ref={lastnameRef}
        onKeyDown={handleLastname}
        placeholder="enter lastname"
      />
      <br />
      <button onKeyDown={handleBtn} ref={btnRef}>
        Submit
      </button>
    </div>
  );
}

export default App;

```

Input.js

```jsx
import React from "react";
import { forwardRef } from "react";
function Input({ onKeyDown, placeholder }, ref) {
  return (
    <div>
      <input onKeyDown={onKeyDown} placeholder={placeholder} ref={ref} />
    </div>
  );
}

const forwardedRef = forwardRef(Input);
export default forwardedRef;

```

NOTE : here we have passed ref from parent component to child component using forwardRef.



<br> 

## Q.65 WHAT IS THUNK MIDDLEWARE IN REACTJS ? 
In the context of React and Redux, a thunk is a middleware that allows you to write action creators that return functions instead of plain objects. Thunks are a way to handle asynchronous logic in Redux.

Here's a breakdown of what a thunk middleware does and why it's used:

1. **Asynchronous Actions:**
When dealing with asynchronous operations, such as fetching data from an API or performing other side effects, regular action creators in Redux return plain objects, typically with a type and payload. Thunks enable you to return functions instead.
2. **Thunk Definition:**
A thunk is a function that wraps an expression to delay its evaluation. In the context of Redux, a thunk is a function that can be dispatched to the store and has access to the `dispatch` and `getState` functions. Thunks are typically used for side effects, such as asynchronous API calls.
3. **Thunk Middleware:**
The thunk middleware intercepts actions before they reach the reducer. If an action is a function (a thunk), the middleware executes that function. This is possible because middleware sits between the dispatching of an action and the point at which the action reaches the reducer.
4. **Example Usage:**
Consider an asynchronous action to fetch data from an API. Without thunks, you might dispatch a plain object action and handle the asynchronous operation outside the action creator. With thunks, you can dispatch a function instead:
    
    ```jsx
    // Without Thunk
    const fetchData = () => {
      return {
        type: 'FETCH_DATA',
        payload: fetch('<https://api.example.com/data>')
      };
    };
    
    // With Thunk
    const fetchDataWithThunk = () => {
      return (dispatch, getState) => {
        // Access to dispatch and getState
        dispatch({ type: 'FETCH_DATA_REQUEST' });
    
        fetch('<https://api.example.com/data>')
          .then(response => response.json())
          .then(data => dispatch({ type: 'FETCH_DATA_SUCCESS', payload: data }))
          .catch(error => dispatch({ type: 'FETCH_DATA_FAILURE', payload: error }));
      };
    };
    
    ```
    
5. **Redux Thunk Library:**
To use thunks in Redux, you typically employ the `redux-thunk` middleware. You apply it when creating the Redux store:
    
    ```jsx
    import { createStore, applyMiddleware } from 'redux';
    import thunk from 'redux-thunk';
    import rootReducer from './reducers';
    
    const store = createStore(rootReducer, applyMiddleware(thunk));
    
    ```
    

By using thunks, you can keep your action creators more flexible, handling both synchronous and asynchronous logic, and effectively manage side effects in your Redux application.


<br> 


## Q.66 where we can store token in reactjs? 
In ReactJS applications, storing authentication tokens securely is crucial for maintaining the security of your application. There are several common approaches to storing authentication tokens in ReactJS:

1. **Using Local Storage or Session Storage**: You can store the authentication token in the browser's local storage or session storage. Local storage persists even after the browser is closed and reopened, while session storage persists only until the browser is closed. While this approach is simple to implement, it's important to be cautious as tokens stored in local storage are vulnerable to XSS (Cross-Site Scripting) attacks.
2. **Using Cookies**: Authentication tokens can be stored in HTTP cookies. Cookies provide a way to store data in the browser that is sent with every request to the server. Cookies can be set to be HTTP-only, meaning they can't be accessed via JavaScript, which can enhance security by mitigating some types of attacks. However, cookies also have limitations, such as size restrictions and being susceptible to CSRF (Cross-Site Request Forgery) attacks.
3. **Using React Context API**: You can use React's Context API to manage authentication state and store the authentication token within the context. This allows components throughout your application to access the authentication token without needing to pass it down through props manually. However, be cautious about using this approach for sensitive tokens, as React context is not designed specifically for security purposes.
4. **Redux or State Management Libraries**: If you're using Redux or another state management library, you can store the authentication token in the global state managed by these libraries. This allows you to access the token from any component that needs it. Make sure to follow best practices for securing sensitive data in your global state.
5. **In-memory**: For temporary storage needs, you can store the authentication token in memory (e.g., within a variable or state) during the user's session. However, this approach is not suitable for persisting authentication across page reloads or browser sessions.

When choosing where to store authentication tokens, consider factors such as security requirements, ease of implementation, and compatibility with your application's architecture. Additionally, ensure that you follow security best practices, such as encrypting sensitive data, using HTTPS, and validating input to mitigate common security vulnerabilities.


<br> 

## Q.67 how to create react auth middleware in redux?
Sure, here's a more detailed example with multiple files:

1. **authActionTypes.js**: Define action types for authentication.

```jsx
// authActionTypes.js

export const LOGIN_REQUEST = 'LOGIN_REQUEST';
export const LOGIN_SUCCESS = 'LOGIN_SUCCESS';
export const LOGIN_FAILURE = 'LOGIN_FAILURE';
export const LOGOUT = 'LOGOUT';

```

1. **authSlice.js**: Define a slice to handle authentication state and actions.

```jsx
// authSlice.js

import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
import authService from './authService';

// Thunk for handling login action asynchronously
export const loginAsync = createAsyncThunk(
  'auth/login',
  async ({ username, password }, { rejectWithValue }) => {
    try {
      const response = await authService.login(username, password);
      return response.data.token;
    } catch (error) {
      return rejectWithValue(error.message);
    }
  }
);

// Define initial state
const initialState = {
  authToken: null,
  error: null,
  loading: false
};

// Create auth slice
const authSlice = createSlice({
  name: 'auth',
  initialState,
  reducers: {
    logout: state => {
      state.authToken = null;
      state.error = null;
    }
  },
  extraReducers: builder => {
    builder.addCase(loginAsync.pending, state => {
      state.loading = true;
    });
    builder.addCase(loginAsync.fulfilled, (state, action) => {
      state.loading = false;
      state.authToken = action.payload;
      state.error = null;
    });
    builder.addCase(loginAsync.rejected, (state, action) => {
      state.loading = false;
      state.error = action.payload;
    });
  }
});

// Export actions
export const { logout } = authSlice.actions;

// Export reducer
export default authSlice.reducer;

```

1. **authService.js**: Simulate authentication API requests.

```jsx
// authService.js

const authService = {
  login: (username, password) => {
    return new Promise((resolve, reject) => {
      // Simulate API request (replace with actual API call)
      setTimeout(() => {
        if (username === 'user' && password === 'password') {
          resolve({ data: { token: 'example_token' } });
        } else {
          reject(new Error('Invalid username or password'));
        }
      }, 1000);
    });
  }
};

export default authService;

```

1. **store.js**: Configure the Redux store using Redux Toolkit.

```jsx
// store.js

import { configureStore } from '@reduxjs/toolkit';
import authReducer from './authSlice';

const store = configureStore({
  reducer: {
    auth: authReducer
  }
});

export default store;

```

1. **index.js**: Set up the application and provide Redux store.

```jsx
// index.js

import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import App from './App';
import store from './store';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

```

With this setup, you can dispatch the `loginAsync` thunk action from your components to handle login asynchronously. Redux Toolkit will take care of managing the loading state and error handling for you. Remember to replace the simulated API calls in `authService.js` with actual API requests in your application.


<br> 











   
