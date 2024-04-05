
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

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/bb84a837-2cf8-4050-9be7-1ab3d9e1ae4d/781175cb-a029-48d3-916c-81e31df8a426/Untitled.png)



<br> 

