---
title: "What are Controlled and Uncontrolled Components in React.js?"
seoTitle: "Controlled vs Uncontrolled Components in React"
seoDescription: "An easy guide to understanding controlled and uncontrolled components in React.js, including their differences, advantages, and best practices"
datePublished: Mon Jun 24 2024 05:03:03 GMT+0000 (Coordinated Universal Time)
cuid: clxsihvwt000409l8fuw90jii
slug: what-are-controlled-and-uncontrolled-components-in-reactjs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719205293364/ec06b5d5-c55a-4c6c-b4d7-7d28a31581e7.jpeg
tags: tutorial, express, blogging, js, javascript, nodejs, beginner, reactjs, node, beginners, frontend-development, rest-api, difference, reactcomponent, reacthooks

---

[![BuyMeACoffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black align="left")](https://buymeacoffee.com/dk119819)

React.js, a popular JavaScript library for building user interfaces, offers a flexible approach to managing forms and user inputs through controlled and uncontrolled components. Understanding the distinction between these two types of components is essential for developers aiming to create efficient and maintainable code. In this article, we'll explore what controlled and uncontrolled components are, their key differences, use cases, and best practices.

---

## 1\. Introduction to Components in React.js

React.js is built around the concept of components, which are reusable pieces of UI that encapsulate their own structure, logic, and styling. Components can be either **stateful** or **stateless**:

* **Stateful Components** (Class components or Functional components with hooks) manage and store state.
    
* **Stateless Components** (Functional components) do not manage state internally.
    

Form handling in React is typically managed through controlled and uncontrolled components, each offering unique advantages and approaches.

---

## 2\. Controlled Components

### Definition and Characteristics

A **controlled component** in React is a form element whose value is controlled by the state of a React component. This means that the state of the component dictates the value of the form element. Every state change is handled through a React event handler, making the React state the "single source of truth" for the form element.

### Characteristics of Controlled Components:

* **State Management:** The component’s state controls the form data.
    
* **Event Handling:** Updates to the form element's value are handled by React events.
    
* **Single Source of Truth:** The form element's value is synced with the state.
    

### Advantages

1. **Predictable State Management:** Since the state of the form elements is stored in React state, it becomes easier to manage and predict the behavior of the form.
    
2. **Validation:** Form validation can be easily handled by adding logic to the event handlers.
    
3. **Instant Feedback:** The form elements can provide immediate feedback to users by updating the state.
    

### Examples

Here’s an example of a controlled component:

```jsx
import React, { useState } from 'react';

function ControlledForm() {
  const [name, setName] = useState('');

  const handleChange = (event) => {
    setName(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    alert('A name was submitted: ' + name);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={name} onChange={handleChange} />
      </label>
      <input type="submit" value="Submit" />
    </form>
  );
}

export default ControlledForm;
```

In this example, the input element's value is controlled by the `name` state, and any changes to the input are handled by the `handleChange` function.

---

## 3\. Uncontrolled Components

### Definition and Characteristics

An **uncontrolled component** in React is a form element that maintains its own internal state. The React component does not directly manage the form element’s state; instead, it accesses the value using references (refs).

### Characteristics of Uncontrolled Components:

* **Direct DOM Access:** The value is accessed directly from the DOM using refs.
    
* **Less Code:** Fewer state variables and event handlers are needed.
    
* **Initial Values:** Default values can be set using the defaultValue attribute.
    

### Advantages

1. **Simplicity:** Uncontrolled components require less boilerplate code since there is no need to manage state for form elements.
    
2. **Ease of Integration:** They can be easier to integrate into existing codebases or third-party libraries where the form handling logic is already defined.
    

### Examples

Here’s an example of an uncontrolled component:

```jsx
import React, { useRef } from 'react';

function UncontrolledForm() {
  const nameInput = useRef(null);

  const handleSubmit = (event) => {
    event.preventDefault();
    alert('A name was submitted: ' + nameInput.current.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" ref={nameInput} />
      </label>
      <input type="submit" value="Submit" />
    </form>
  );
}

export default UncontrolledForm;
```

In this example, the input element's value is accessed using a ref, making it an uncontrolled component.

---

## 4\. Key Differences Between Controlled and Uncontrolled Components

### Controlled Components:

* **State Management:** Managed by React state.
    
* **Event Handling:** Updates via React event handlers.
    
* **Use Case:** When form validation, conditional rendering, or complex form interactions are needed.
    

### Uncontrolled Components:

* **State Management:** Managed by the DOM.
    
* **Event Handling:** Accessed via refs.
    
* **Use Case:** Simple forms or when integrating with non-React code.
    

### Summary of Differences:

| Feature | Controlled Components | Uncontrolled Components |
| --- | --- | --- |
| State Management | React state | DOM |
| Event Handling | React event handlers | Refs |
| Code Complexity | More boilerplate | Less boilerplate |
| Use Cases | Complex forms, validation | Simple forms, existing integrations |
| Default Values | Set through state | Set through `defaultValue` attribute |

---

## 5\. When to Use Controlled vs. Uncontrolled Components

### Controlled Components:

* **Form Validation:** When you need to validate user input in real-time.
    
* **Complex Forms:** When forms require conditional rendering or interdependent inputs.
    
* **Immediate Feedback:** When user interactions need to update the UI immediately.
    

### Uncontrolled Components:

* **Simple Forms:** For basic forms where validation and interactivity are minimal.
    
* **Third-Party Integrations:** When integrating with libraries or frameworks that handle their own form logic.
    
* **Less Overhead:** When simplicity and minimal state management are desired.
    

---

## 6\. Best Practices for Using Controlled and Uncontrolled Components

### Best Practices for Controlled Components:

1. **State Management:** Keep state as simple and minimal as possible.
    
2. **Performance Optimization:** Avoid excessive re-renders by using techniques like memoization and shouldComponentUpdate.
    
3. **Form Validation:** Centralize validation logic to maintain consistency.
    
4. **Modular Code:** Break down large forms into smaller, manageable components.
    

### Best Practices for Uncontrolled Components:

1. **Use Refs Wisely:** Ensure refs are used appropriately to avoid accessing the DOM too frequently.
    
2. **Default Values:** Utilize `defaultValue` for setting initial values without relying on state.
    
3. **Minimal State:** Only use uncontrolled components for forms that do not require complex state management.
    

---

## 7\. Common Pitfalls and How to Avoid Them

### Pitfalls in Controlled Components:

1. **Excessive State Updates:** Frequent state updates can lead to performance issues. Optimize state management and minimize re-renders.
    
2. **Complex State Logic:** Avoid overly complex state logic by breaking it down into smaller, reusable functions or hooks.
    

### Pitfalls in Uncontrolled Components:

1. **Inconsistent State:** Relying on the DOM for state can lead to inconsistencies, especially in complex forms.
    
2. **Limited Validation:** Uncontrolled components are harder to validate, making it challenging to provide real-time feedback.
    

---

## 8\. Conclusion

Understanding the differences between controlled and uncontrolled components in React.js is crucial for developing efficient and maintainable applications. Controlled components offer a more predictable and manageable approach to form handling, making them ideal for complex forms and real-time validation. Uncontrolled components, on the other hand, provide simplicity and ease of integration, making them suitable for basic forms and third-party integrations.

By leveraging the strengths of each type of component and following best practices, developers can create robust, user-friendly forms that enhance the overall user experience. Whether you choose controlled or uncontrolled components, the key is to understand their use cases and apply them appropriately in your projects.

---

## 💰 You can help me by Donating

[![BuyMeACoffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black align="left")](https://buymeacoffee.com/dk119819)