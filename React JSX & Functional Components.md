# React JSX & Functional Components

## 📝 Description

This document introduces React's JSX syntax and functional components - the building blocks of modern React development. Learn how to write component-based UIs, understand JSX compilation, and master the fundamentals of React component structure.

**What you'll learn:**
- What JSX is and how it works under the hood
- Creating and using functional components
- Passing and using props effectively
- Common JSX rules and best practices
- Practical component composition patterns

**Prerequisites:** Basic JavaScript ES6+ knowledge

**Difficulty Level:** Beginner

**Estimated Reading Time:** 15-20 minutes

---

## 1️⃣ What is JSX?

**JSX (JavaScript XML)** is a syntax extension that allows you to write HTML-like UI in your JavaScript.

- It's **not HTML**, but it looks like it
- React uses JSX to define UI components
- JSX is **transpiled** (by Babel) into JavaScript

### Basic JSX Example

```jsx
const element = <h1>Hello, world!</h1>;
```

This JSX is transpiled into:

```javascript
const element = React.createElement("h1", null, "Hello, world!");
```

## 🔍 JSX in Depth

### ✅ Valid JSX Patterns

**Embedding JavaScript with {}:**

```jsx
const name = "Vijay";
const greeting = <h1>Hello, {name}!</h1>;
```

**Single Parent Element:**

```jsx
return (
  <div>
    <h1>Hello</h1>
    <p>World</p>
  </div>
);
```

**Using React Fragments:**

```jsx
return (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
);
```

### ❌ Invalid JSX

**Multiple sibling elements without wrapper:**

```jsx
// This will cause a syntax error
return (
  <h1>Hello</h1>
  <p>World</p>
);
```

## 🧠 JSX Under the Hood

JSX is **syntactic sugar** over `React.createElement()`:

```jsx
const element = <h1 className="greet">Hi</h1>;
```

Is converted to:

```javascript
const element = React.createElement("h1", { className: "greet" }, "Hi");
```

## 2️⃣ What are Functional Components?

A **Functional Component** is:
- A plain JavaScript function
- Starts with a **capital letter**
- Accepts **props** as input
- Returns **JSX** as output

### Basic Example

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

**Usage:**

```jsx
<Welcome name="Vijay" />
```

**Renders:**

```
Hello, Vijay!
```

## 3️⃣ Props in Functional Components

**Props** are like function arguments — passed in from the parent component.

### Using Props with Destructuring

```jsx
function Greet({ name, age }) {
  return (
    <p>
      Hi {name}, you are {age} years old.
    </p>
  );
}

// Usage:
<Greet name="Pingu" age={4} />
```

## 4️⃣ Practical Examples

### Example 1: UserCard Component

```jsx
const UserCard = ({ userDetails }) => {
  return (
    <div>
      <h2>{userDetails.name}</h2>
      <p>{userDetails.email}</p>
    </div>
  );
};
```

### Example 2: UsersList Component

```jsx
const users = [
  { name: "Vijay", email: "vijay@site.com" },
  { name: "Pingu", email: "pingu@site.com" },
];

export function App() {
  return (
    <div>
      {users.map((user) => (
        <UserCard key={user.email} userDetails={user} />
      ))}
    </div>
  );
}
```

**Key Points:**
- Use `key` prop for list items (React needs this for efficient rendering)
- Wrap mapped elements in a container element
- Pass data through props for component reusability

## 5️⃣ Common Pitfalls to Avoid

| Mistake | Fix |
|---------|-----|
| Returning multiple elements without wrapper | Wrap in `<div>` or `<>` `</>` (fragment) |
| Using lowercase for component names | Always capitalize component names |
| Trying to use `if` inside JSX | Use ternaries `? :` or logical `&&` |
| Using `class` instead of `className` | JSX uses `className` for CSS classes |

### Examples of Common Fixes

**Conditional Rendering:**

```jsx
function Greeting({ isLoggedIn, name }) {
  return (
    <div>
      {isLoggedIn ? <h1>Welcome back, {name}!</h1> : <h1>Please log in</h1>}
    </div>
  );
}
```

**Conditional Display:**

```jsx
function Notification({ hasNotifications, count }) {
  return (
    <div>
      {hasNotifications && <span>You have {count} notifications</span>}
    </div>
  );
}
```

## 🧪 Practice Quiz Solutions

### Q1: Basic JSX with Variables

```jsx
function Greeting() {
  const name = "Vijay";
  return <h1>Hello, {name}</h1>;
}
```

**Answer:** "Hello, Vijay"

**Explanation:** JSX evaluates the expression inside `{name}` and renders the value.

### Q2: JSX as Variables

```jsx
function Box() {
  const box = <div>Hi</div>;
  return box;
}
```

**Answer:** "Hi"

**Explanation:** JSX is just a value (React element), so you can assign it to variables and return it.

### Q3: Multiple Sibling Elements

```jsx
function Test() {
  return <p>1</p><p>2</p>;
}
```

**Answer:** Syntax Error ❌

**Explanation:** JSX must return only one parent element. React doesn't know how to render two sibling JSX tags without a wrapper.

**Fix:**

```jsx
function Test() {
  return (
    <>
      <p>1</p>
      <p>2</p>
    </>
  );
}
```

## 🎯 Key Takeaways

- **JSX is syntactic sugar** over `React.createElement()`
- **Functional Components** are just functions that return JSX
- **Props** are input parameters passed to components
- **You can only return one parent element** from a component
- **Always capitalize component names** (React treats lowercase as HTML tags)
- **Use `key` prop** when rendering lists of elements
- **Use `{}` to embed JavaScript expressions** in JSX
- **Use `className`** instead of `class` for CSS styling

## 🚨 Best Practices

1. **Always wrap multiple elements** in a parent container or fragment
2. **Use descriptive prop names** for better code readability  
3. **Extract reusable logic** into separate components
4. **Keep components small and focused** on a single responsibility
5. **Use destructuring** for cleaner prop access
