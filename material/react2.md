
# React Forms: Core Concepts

This document explains the core React concepts of **React Forms - Intro** (Activity 2). The goal is not to memorize code, but to understand the patterns so you can build and debug forms confidently.

## Learning goals (what you should be able to do)

By the end of the forms activity, you should be able to:

- Create a React **function component** that renders a form.
- Track each form field with React state using the **`useState`** hook.
- Build **controlled inputs** using `value` + `onChange`.
- Handle form submission with **`onSubmit`** and **`event.preventDefault()`**.
- Gather state into a single object (the “submission object”).
- Reset form state after submission.

## 1) React function components: forms are just UI

In React, a form is just JSX returned from a component.

```jsx
function ContactUs() {
	return (
		<form>
			<label htmlFor='name'>Name:</label>
			<input id='name' type='text' />
			<button>Submit</button>
		</form>
	);
}
```

At this point the browser can show the form and you can type, but the component itself does not “know” the values.

## 2) `useState`: storing form values in React

To make the component aware of what the user typed, you store values in React state.

```jsx
import { useState } from 'react';

function ContactUs() {
	const [name, setName] = useState('');

	// later: use name and setName
}
```

Key idea:

- `name` is the current value.
- `setName(newValue)` updates the value and causes React to re-render the component.

Most forms have multiple fields, so you typically have multiple state variables:

- `name`, `email`, `phone`, `phoneType`, `comments`, etc.

## 3) Controlled inputs: `value` + `onChange`

### What “controlled” means

A **controlled input** is an input whose displayed value is controlled by React state.

- The UI displays `value={name}`
- The UI updates state with `onChange={...}`

Example:

```jsx
<input
	id='name'
	type='text'
	value={name}
	onChange={e => setName(e.target.value)}
/>
```

This creates a feedback loop:

1. User types → `onChange` fires.
2. Handler reads the new value from `e.target.value`.
3. `setName(...)` updates state.
4. React re-renders.
5. The `<input>` receives the updated `value` prop.

### Common warning: `value` without `onChange`

If you add `value={name}` but forget `onChange`, React will warn that the field is read-only. That’s React protecting you from an input that can never update.

### Why use controlled inputs?

Controlled inputs make it easy to:

- validate input as the user types
- disable/enable submit
- show errors
- reset the form
- submit values without querying the DOM

## 4) The event object: `e.target.value`

React passes an event object to your handler:

```jsx
onChange={e => {
	console.log(e.target.value);
}}
```

Important pieces:

- `e` is the event
- `e.target` is the element that fired the event (`<input>`, `<select>`, `<textarea>`, etc.)
- `e.target.value` is the current text/selection

## 5) Labels in React: `htmlFor` instead of `for`

In HTML, labels use `for="id"`.

In React JSX, you must write `htmlFor`:

```jsx
<label htmlFor='email'>Email:</label>
<input id='email' type='text' />
```

Reason: `for` is a reserved word in JavaScript.

## 6) Controlled `<select>` (dropdown)

In plain HTML, a `<select>` is controlled by the DOM. In React, you control it the same way as inputs:

```jsx
const [phoneType, setPhoneType] = useState('');

<select
	name='phoneType'
	value={phoneType}
	onChange={e => setPhoneType(e.target.value)}
>
	<option value='' disabled>
		Select a phone type...
	</option>
	<option>Home</option>
	<option>Work</option>
	<option>Mobile</option>
</select>
```

Notes:

- The `value` prop selects the option that matches state.
- The “placeholder” option uses `value=''` and `disabled` so the user must pick a real option.

## 7) Controlled `<textarea>`

In HTML, a `<textarea>` uses inner text for its value:

```html
<textarea>hello</textarea>
```

In React, a controlled `<textarea>` uses `value` (like `<input>`):

```jsx
const [comments, setComments] = useState('');

<textarea
	id='comments'
	value={comments}
	onChange={e => setComments(e.target.value)}
/>
```

## 8) Submitting a form: `onSubmit` + `preventDefault`

By default, HTML form submission triggers a page load (or navigation). In a Single Page App (SPA), you usually *don’t* want that.

Attach an `onSubmit` handler to the form and call `preventDefault()`:

```jsx
const onSubmit = e => {
	e.preventDefault();
	// handle submission in JavaScript
};

<form onSubmit={onSubmit}>
	{/* fields */}
</form>
```

This keeps your React app running and lets you decide what happens on submit.

## 9) Building a “submission object”

Once the form values are stored in state, you can build an object from them. This mirrors what you’d typically send to an API.

```js
const contactUsInformation = {
	name,
	email,
	phone,
	phoneType,
	comments,
	submittedOn: new Date()
};

console.log(contactUsInformation);
```

Why this matters:

- It’s a clean bridge from “UI values” → “data to send to backend”.
- It keeps the submit logic independent from the JSX.

## 10) Resetting the form after submit

With controlled inputs, resetting is easy: set the state back to empty strings (or initial values).

```js
setName('');
setEmail('');
setPhone('');
setPhoneType('');
setComments('');
```

Because the inputs read from state, the UI clears immediately after the state reset.

## 11) Debugging tips (practical)

- If you can’t type in a field: check for `value={...}` without `onChange`.
- If the value isn’t updating: verify you used `e.target.value`.
- Use React DevTools to watch state change as you type.
- If submit reloads the page: you forgot `e.preventDefault()` or attached `onSubmit` to the wrong element.

## 12) Controlled components (the core idea)

HTML inputs naturally keep their own state.

React components can also keep state.

In a **controlled component**, you decide that React state is the “source of truth”, and the form elements simply display that state and report changes through events.

This is one of the most important patterns in React—especially for real apps where you need validation, conditional UI, and predictable behavior.

