
# React `useState`: Concepts from the Counter Lab

This document explains the core concepts introduced in the `useState` Counter + Theme lab. The focus is on how React handles events and UI updates, and why state is the mechanism used to make the UI respond to user actions.

## Learning objectives (what you should be able to explain)

- How events work in vanilla JavaScript vs React
- How to attach event handlers using `onClick` and `onChange`
- Why normal variables do not update the UI in React
- How to use the `useState` hook to manage component state
- How to toggle state values
- How to update state safely using callback (functional) updates
- The difference between imperative and declarative programming

---

## 1) Events in web development

An **event** is a signal that something happened in the browser (for example, a user clicks a button, types into an input, or submits a form). You can attach code that runs when that event occurs.

### Vanilla JavaScript events

There are multiple ways to attach events in vanilla JavaScript.

**A) HTML attributes (older style)**

```html
<input type="button" value="Click me" onclick="alert('Clicked!')" />
```

Characteristics:

- The handler is written as a string in HTML.
- HTML and JavaScript are tightly coupled.
- It becomes difficult to organize and reuse logic as the UI grows.

**B) `addEventListener` (modern and recommended)**

```html
<button id="btn">Click</button>

<script>
  const btn = document.querySelector('#btn');
  btn.addEventListener('click', () => {
    console.log('Clicked');
  });
</script>
```

Characteristics:

- JavaScript logic stays in JavaScript, not inside HTML.
- You explicitly select DOM elements and attach listeners.
- You often manually update the DOM after the event (for example, changing classes, text, or styles).

### React events

In React, you still handle browser events (clicks, input changes, etc.), but you attach them through JSX props:

- Event names use **camelCase**: `onClick`, `onChange`, `onSubmit`, …
- You pass a **function**, not a string.
- In most cases you update **state**, and React updates the UI.

Example:

```jsx
<button onClick={handleClick}>Click</button>
```

React uses a consistent event system (often referred to as “synthetic events”) so the handler receives an event object in a predictable way across browsers.

---

## 2) Attaching event handlers with `onClick` and `onChange`

### `onClick`

`onClick` runs when the user clicks an element (commonly a button).

```jsx
const handleClick = () => {
  console.log('Button clicked');
};

<button onClick={handleClick}>Increment</button>
```

Important rule: pass the **function reference**, do not call the function.

❌ Incorrect (runs immediately during render):

```jsx
<button onClick={handleClick()}>Click</button>
```

✅ Correct (runs only on click):

```jsx
<button onClick={handleClick}>Click</button>
```

### `onChange`

`onChange` is commonly used with inputs. In React, `onChange` fires as the user types (for text inputs).

```jsx
const handleNameChange = event => {
  console.log('New value:', event.target.value);
};

<input type="text" onChange={handleNameChange} />
```

In practice, `onChange` is often used to store the input value in state (this is the typical “controlled input” pattern):

```jsx
const [name, setName] = useState('');

<input
  type="text"
  value={name}
  onChange={event => setName(event.target.value)}
/>
```

This makes the input’s displayed value come from React state, and changes flow through the state update.

---

## 3) Why normal variables do not update the UI in React

In React, a component’s UI is produced by running the component function and returning JSX. React updates the screen when it decides the component should **re-render**.

If you write:

```js
let theme = 'light';
```

and later do:

```js
theme = 'dark';
```

React does not automatically know that it should re-render. A normal variable changing does not trigger a re-render.

Two practical consequences:

- The UI will not update just because a normal variable changed.
- Even if the component re-renders for some other reason, normal variables inside the component can reset because the function runs again from the top.

React is designed around the idea that **state and props** are the values that drive rendering.

---

## 4) What “state” is and why it solves the problem

**State** is component-owned data that can change over time. When you update state with the provided setter function, React schedules a re-render so the UI can be recalculated.

In other words:

- **State changes → React re-renders → UI updates**

This is the central reason `useState` exists.

---

## 5) The `useState` hook

`useState` is a React Hook that lets a function component store and update state.

Syntax:

```jsx
const [value, setValue] = useState(initialValue);
```

Meaning:

- `value` is the current state value.
- `setValue` is the function you call to request an update.
- `initialValue` is the starting value used on the first render.

Example (theme):

```jsx
const [theme, setTheme] = useState('light');
```

When you call `setTheme('dark')`, React updates the state and re-renders the component. On the next render, `theme` will be `'dark'`, and any JSX that uses `theme` will reflect that.

---

## 6) Toggling state values

Toggling means switching between two states based on the current value.

Common examples:

- `'light'` ↔ `'dark'`
- `true` ↔ `false`

Theme toggle can be written in two common ways.

**A) Direct update (simple and readable)**

```jsx
const toggleTheme = () => {
  setTheme(theme === 'light' ? 'dark' : 'light');
};
```

This is often fine when:

- you only do one toggle per event handler, and
- you are not scheduling multiple updates that depend on the same value.

**B) Functional update (safer when the next value depends on the previous)**

```jsx
const toggleTheme = () => {
  setTheme(prevTheme => (prevTheme === 'light' ? 'dark' : 'light'));
};
```

The functional update form becomes important when multiple updates can happen close together (React may batch updates), because it always calculates from the most recent previous value.

---

## 7) Updating state safely with callback (functional) updates

When the next state depends on the previous state, the safest pattern is the **functional update** form.

First, here is the direct form (often works, but can be fragile in some cases):

```jsx
setCount(count + 1);
```

Then, here is the functional update form (recommended when the next value depends on the previous value):

```jsx
setCount(prevCount => prevCount + 1);
```

Why this matters:

- React may batch multiple state updates together.
- If you read `count` directly in your handler, you might read a value that is not the final “latest” value at the time React applies updates.

Example of where functional updates help:

```jsx
const addThree = () => {
  setCount(prev => prev + 1);
  setCount(prev => prev + 1);
  setCount(prev => prev + 1);
};
```

This reliably adds 3 because each update is computed from the latest previous value.

Naming convention:

- Prefer descriptive names like `prevCount` / `prevTheme` for clarity.
- Very short names like `c` or `t` are valid, but they reduce readability (especially for beginners).

---

## 8) Imperative vs declarative programming

### Imperative (describe how)

In an imperative style, you describe step-by-step DOM instructions.

Example (vanilla JavaScript theme toggle):

```js
const root = document.querySelector('.content');
root.classList.remove('light');
root.classList.add('dark');
```

This approach can work, but as the UI grows it becomes easier to miss an update or create inconsistent UI state.

### Declarative (describe what)

In React, you describe what the UI should look like for a given state:

```jsx
<div className={`content ${theme}`}></div>
```

Then you update state:

```jsx
setTheme('dark');
```

React determines how to update the DOM to match the new UI description.

---

## Key takeaways

- React events use JSX props like `onClick` and `onChange` and expect function values.
- Normal variables do not trigger re-renders, so they do not reliably update the UI.
- `useState` stores values that should drive rendering; calling the setter triggers re-render.
- When computing next state from previous state, prefer functional updates like `setCount(prev => prev + 1)`.
- React is primarily declarative: describe UI from state instead of manually manipulating the DOM.

## Final mental model

In React, the most reliable workflow is:

1. User triggers an event (`onClick`, `onChange`, …)
2. Event handler updates state (`setTheme(...)`, `setCount(...)`)
3. React re-renders the component
4. The UI updates to match the new state


---
## Links

- [Introduction to Events](https://javascript.info/introduction-browser-events)
- [Responding to Events](https://react.dev/learn/responding-to-events)
- [State: A Component's Memory](https://react.dev/learn/state-a-components-memory)
- [Render and Commit](https://react.dev/learn/render-and-commit)
- [State as a Snapshot](https://react.dev/learn/state-as-a-snapshot)
- [Updating Objects in State](https://react.dev/learn/updating-objects-in-state)
- [Updating Arrays in State](https://react.dev/learn/updating-arrays-in-state)

