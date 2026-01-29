# React useState Lab: Building a Counter with Theme Toggle

## Lab Overview

In this lab, you will learn how to use the [`useState`] hook in React by building a simple Counter component step by step. The final component will:

* Change the theme between **light** and **dark**
* Increment and decrement a counter value

The lab is designed to move gradually from familiar JavaScript concepts to React-specific ideas, with explanations at each step.

---

## Learning Objectives

By the end of this lab, you should be able to:

* Understand how events work in vanilla JavaScript vs React
* Attach event handlers using `onClick` and `onChange`
* Explain why normal variables do not update the UI in React
* Use the `useState` hook to manage component state
* Toggle state values
* Update state safely using callback functions
* Understand the difference between **imperative** and **declarative** programming

---

## Step 0: Set Up Your Project (Vite + React)

Before starting the lab steps, set up a React project so you have a place to run your `Counter` component.

1. Open **VS Code** in your working folder (for example: `week3`).
2. Create a new React project using Vite (full guide: [vite.md](./vite.md)). In brief, run:

  ```bash
  npx create-vite@latest w3-fe-lab1 --template react
  cd w3-fe-lab1b
  npm install
  npm run dev
  ```

  Notes:

  - By default, Vite runs on port `5173`.
  - For files that contain JSX, prefer the `.jsx` extension.

3. Clean up the default styles so they do not interfere with the lab:

  - In `src/index.css`, remove the default CSS (you can leave it empty).
  - In `src/App.css`, remove the default CSS (you can leave it empty).

4. Create your `Counter` component files using the following starter files:

  - `src/Counter.jsx`
   ```jsx
   import './Counter.css';

   const Counter = () => {
   return (
      <div className="state">
         <h1>UseState Component</h1>
         <button>Dark</button>
         <button>Light</button>
         <h2>DISPLAY COUNT HERE</h2>
         <button>Increment</button>
         <button>Decrement</button>
      </div>
   );
   };

   export default Counter;
   ```

- `src/Counter.css`

   ```css
   button {
   font-size: 1.2em;
   margin: 10px 0;
   padding: 5px;
   width: 200px;
   height: 75px;
   border-radius: 5px;
   }

   .state {
   display: flex;
   flex-direction: column;
   justify-content: center;
   align-items: center;
   text-align: center;
   }

   .light {
   background-color: rgb(210, 247, 189);
   color: black;
   height: 100vh;
   }

   .dark {
   background-color: rgb(88, 8, 84);
   color: white;
   height: 100vh;
   }
   ```  

5. Import and render the `Counter` component in `src/App.jsx`.

  After you create `src/Counter.jsx`, your `App.jsx` can be:

  ```jsx
  import Counter from './Counter';
  import './App.css';

  function App() {
    return <Counter />;
  }

  export default App;
  ```

6. Keep the dev server running (`npm run dev`) while you work. When you save files, the browser should refresh automatically.

---

## Step 1: Events in Vanilla JavaScript vs React

### Vanilla JavaScript Events

In vanilla JavaScript, one simple way to handle events is by adding an event attribute directly in HTML.

Example:

```html
<input value="Click me" onclick="alert('Click!')" type="button" />
```

Here:

* The event handler is written directly in HTML
* The browser runs the JavaScript when the event occurs

This approach works, but it tightly couples HTML and JavaScript together.

### React Events

In React:

* Events are written in **camelCase** (e.g. `onClick`, `onChange`)
* Event handlers are passed **functions**, not strings
* Logic lives inside the component, not in the HTML

This keeps UI and behavior organized inside components.


## Clarifications (Read This Once)

- **You won’t see UI changes until state changes.** `console.log()` confirms the click happened, but it won’t change what’s rendered.
- **Where state “lives” matters.** If you use a normal variable (Step 4), React won’t re-render when it changes.
- **Using a normal variable inside the component is even trickier.** In React, the component function re-runs on re-render, so normal variables can reset to their initial value.
- **The theme works because of CSS class names.** The JSX uses ``className={`state ${theme}`}`` which relies on `.light` and `.dark` existing in `Counter.css`.
- **Hook rule (important):** `useState` must be called at the top level of the component (not inside `if`, loops, or nested functions).

---

## Step 2: Adding Event Handlers in React

Let’s start by confirming that button clicks work.

Update your `Counter.jsx`:

```jsx
const Counter = () => {
  const handleClick = () => {
    console.log('Button clicked');
  };

  return (
    <div className="state">
      <h1>UseState Component</h1>
      <button onClick={handleClick}>Dark</button>
      <button onClick={handleClick}>Light</button>
    </div>
  );
};
```

### Explanation

* `onClick` listens for click events
* We pass a **function reference** to `onClick`
* The function runs only when the user clicks

At this stage, we are not changing the UI—just confirming events work.

### Optional: Quick `onChange` demo

`onChange` is typically used with inputs. React passes an event object to your handler, so you can read the current input value from `event.target.value`.

Example:

```jsx
<input
  type="text"
  placeholder="Type here"
  onChange={event => console.log(event.target.value)}
/>
```

<details>
<summary>Complete Counter.jsx (After Step 2)</summary>

```jsx
import './Counter.css';

const Counter = () => {
  const handleClick = () => {
    console.log('Button clicked');
  };

  return (
    <div className="state">
      <h1>UseState Component</h1>
      <button onClick={handleClick}>Dark</button>
      <button onClick={handleClick}>Light</button>
    </div>
  );
};

export default Counter;
```

</details>

---

## Step 3: Two Ways to Attach Event Handlers

### Option 1: Inline Arrow Function

```jsx
<button onClick={() => console.log('Dark clicked')}>Dark</button>
```

### Option 2: Named Handler Function

```jsx
const handleDarkClick = () => {
  console.log('Dark clicked');
};

<button onClick={handleDarkClick}>Dark</button>
```

### Important Note

❌ This is incorrect:

```jsx
<button onClick={handleDarkClick()}>Dark</button>
```

This calls the function immediately instead of waiting for a click.

<details>
<summary>Complete Counter.jsx (After Step 3 — named handlers version)</summary>

```jsx
import './Counter.css';

const Counter = () => {
  const handleDarkClick = () => {
    console.log('Dark clicked');
  };

  const handleLightClick = () => {
    console.log('Light clicked');
  };

  return (
    <div className="state">
      <h1>UseState Component</h1>
      <button onClick={handleDarkClick}>Dark</button>
      <button onClick={handleLightClick}>Light</button>
    </div>
  );
};

export default Counter;
```

</details>

---

## Step 4: Trying to Change Theme Without State

Let’s try to change the theme using a normal variable.

```jsx
let theme = 'light';

const setDarkTheme = () => {
  theme = 'dark';
  console.log(theme);
};
```

Even though `theme` changes, the UI does **not** update.

### Why This Does Not Work

* React does **not** re-render when normal variables change
* React only re-renders when **state or props** change

This is why we need `useState`.

<details>
<summary>Complete Counter.jsx (After Step 4 — using a normal variable)</summary>

```jsx
import './Counter.css';

const Counter = () => {
  let theme = 'light';

  const setDarkTheme = () => {
    theme = 'dark';
    console.log(theme);
  };

  const setLightTheme = () => {
    theme = 'light';
    console.log(theme);
  };

  return (
    <div className={`state ${theme}`}>
      <h1>UseState Component</h1>
      <button onClick={setDarkTheme}>Dark</button>
      <button onClick={setLightTheme}>Light</button>
      <p>
        Current theme (logged only): <strong>{theme}</strong>
      </p>
    </div>
  );
};

export default Counter;
```

Note: The UI will usually stay on the initial theme because changing `theme` does not trigger a React re-render.

</details>

---

## Step 5: Introducing useState for Theme

Import `useState`:

```jsx
import { useState } from 'react';
```

Create theme state:

```jsx
const [theme, setTheme] = useState('light');
```

Update JSX:

```jsx
<div className={`state ${theme}`}>
```

Add handlers:

```jsx
<button onClick={() => setTheme('dark')}>Dark</button>
<button onClick={() => setTheme('light')}>Light</button>
```

### Explanation

* `theme` stores the current theme
* `setTheme` updates the state
* Updating state causes React to re-render

<details>
<summary>Complete Counter.jsx (After Step 5 — theme in state)</summary>

```jsx
import './Counter.css';
import { useState } from 'react';

const Counter = () => {
  const [theme, setTheme] = useState('light');

  return (
    <div className={`state ${theme}`}>
      <h1>UseState Component</h1>
      <button onClick={() => setTheme('dark')}>Dark</button>
      <button onClick={() => setTheme('light')}>Light</button>
    </div>
  );
};

export default Counter;
```

</details>

---

## Step 6: Toggling Theme Using Previous State

```jsx
const toggleThemeHandler = () => {
  setTheme(prevTheme => (prevTheme === 'light' ? 'dark' : 'light'));
};
```

### Explanation

* React gives access to the previous state value
* This is useful when the new state depends on the old one
* This is the **callback (functional update)** form of `setTheme` (the same idea is used again in Step 9)

<details>
<summary>Complete Counter.jsx (After Step 6 — toggle theme)</summary>

```jsx
import './Counter.css';
import { useState } from 'react';

const Counter = () => {
  const [theme, setTheme] = useState('light');

  const toggleThemeHandler = () => {
    setTheme(prevTheme => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  return (
    <div className={`state ${theme}`}>
      <h1>UseState Component</h1>
      <button onClick={() => setTheme('dark')}>Dark</button>
      <button onClick={() => setTheme('light')}>Light</button>
      <button onClick={toggleThemeHandler}>Toggle Theme</button>
    </div>
  );
};

export default Counter;
```

</details>

---

## Step 7: Imperative vs Declarative Programming

### Imperative (Vanilla JS)

You describe **how** to do something step by step:

* Select element
* Change background color
* Change text color

### Declarative (React)

You describe **what** you want:

* The theme is `dark`

React figures out how to update the UI.

### Metaphor

* **Imperative:** Giving turn-by-turn directions to a taxi driver
* **Declarative:** Telling the taxi driver the destination

<details>
<summary>Complete Counter.jsx (After Step 7 — no code changes)</summary>

```jsx
import './Counter.css';
import { useState } from 'react';

const Counter = () => {
  const [theme, setTheme] = useState('light');

  const toggleThemeHandler = () => {
    setTheme(prevTheme => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  return (
    <div className={`state ${theme}`}>
      <h1>UseState Component</h1>
      <button onClick={() => setTheme('dark')}>Dark</button>
      <button onClick={() => setTheme('light')}>Light</button>
      <button onClick={toggleThemeHandler}>Toggle Theme</button>
    </div>
  );
};

export default Counter;
```

</details>

---

## Step 8: Adding Counter State

Create count state:

```jsx
const [count, setCount] = useState(0);
```

Display count:

```jsx
<h2>{count}</h2>
```

<details>
<summary>Complete Counter.jsx (After Step 8 — added count state)</summary>

```jsx
import './Counter.css';
import { useState } from 'react';

const Counter = () => {
  const [theme, setTheme] = useState('light');
  const [count, setCount] = useState(0);

  const toggleThemeHandler = () => {
    setTheme(prevTheme => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  return (
    <div className={`state ${theme}`}>
      <h1>UseState Component</h1>
      <button onClick={() => setTheme('dark')}>Dark</button>
      <button onClick={() => setTheme('light')}>Light</button>
      <button onClick={toggleThemeHandler}>Toggle Theme</button>

      <h2>{count}</h2>

      <button>Increment</button>
      <button>Decrement</button>
    </div>
  );
};

export default Counter;
```

</details>

---

## Step 9: Updating Counter Using Callback

```jsx
const incrementHandler = () => {
  setCount(prevCount => prevCount + 1);
};

const decrementHandler = () => {
  setCount(prevCount => prevCount - 1);
};
```

### Why Use a Callback?

* This is the same pattern you used in Step 6: the next value depends on the previous value
* State updates may be batched
* Using the previous value guarantees correctness

<details>
<summary>Complete Counter.jsx (After Step 9 — increment/decrement handlers)</summary>

```jsx
import './Counter.css';
import { useState } from 'react';

const Counter = () => {
  const [theme, setTheme] = useState('light');
  const [count, setCount] = useState(0);

  const toggleThemeHandler = () => {
    setTheme(prevTheme => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  const incrementHandler = () => {
    setCount(prevCount => prevCount + 1);
  };

  const decrementHandler = () => {
    setCount(prevCount => prevCount - 1);
  };

  return (
    <div className={`state ${theme}`}>
      <h1>UseState Component</h1>
      <button onClick={() => setTheme('dark')}>Dark</button>
      <button onClick={() => setTheme('light')}>Light</button>
      <button onClick={toggleThemeHandler}>Toggle Theme</button>

      <h2>{count}</h2>

      <button onClick={incrementHandler}>Increment</button>
      <button onClick={decrementHandler}>Decrement</button>
    </div>
  );
};

export default Counter;
```

</details>

---

## Final Working Counter.jsx

```jsx
import './Counter.css';
import { useState } from 'react';

const Counter = () => {
  const [theme, setTheme] = useState('light');
  const [count, setCount] = useState(0);

  const toggleThemeHandler = () => {
    setTheme(prevTheme => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  const incrementHandler = () => {
    setCount(prevCount => prevCount + 1);
  };

  const decrementHandler = () => {
    setCount(prevCount => prevCount - 1);
  };

  return (
    <div className={`state ${theme}`}>
      <h1>UseState Component</h1>
      <button onClick={() => setTheme('dark')}>Dark</button>
      <button onClick={() => setTheme('light')}>Light</button>
      <button onClick={toggleThemeHandler}>Toggle Theme</button>
      <h2>{count}</h2>
      <button onClick={incrementHandler}>Increment</button>
      <button onClick={decrementHandler}>Decrement</button>
    </div>
  );
};

export default Counter;
```

---

## Summary

* Events in React are attached using JSX attributes
* State is required to trigger UI updates
* `useState` allows React to re-render components
* Functional updates are safer when new state depends on old state
* React encourages declarative UI design




<!-- Links -->

[`useState`]: https://react.dev/reference/react/useState
[event handler]: https://react.dev/learn/responding-to-events#adding-event-handlers

