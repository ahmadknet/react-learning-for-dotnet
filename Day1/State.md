Since you already know Angular and TypeScript, the easiest way to understand **React State** is to compare it directly with Angular component properties.

# What is State?

**State = data that can change over time and when it changes, the UI updates automatically.**

Examples:

* Counter value
* Logged-in user
* Loading indicator
* Search text
* Form values
* API response data

---

# Angular Approach

In Angular, component properties are effectively your state.

```typescript
@Component({
  selector: 'app-counter',
  template: `
    <h2>{{ count }}</h2>

    <button (click)="increment()">
      Increment
    </button>
  `
})
export class CounterComponent {

  count = 0;

  increment() {
    this.count++;
  }
}
```

### What happens?

```typescript
this.count++;
```

Angular's change detection runs and updates:

```html
<h2>{{ count }}</h2>
```

---

# React Approach (TSX)

In React, changing a normal variable does **not** update the UI.

You must use **State**.

```tsx
import { useState } from "react";

function Counter() {

  const [count, setCount] = useState<number>(0);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <>
      <h2>{count}</h2>

      <button onClick={increment}>
        Increment
      </button>
    </>
  );
}

export default Counter;
```

---

# Angular vs React

| Angular                        | React                 |
| ------------------------------ | --------------------- |
| Component property             | State variable        |
| `count = 0`                    | `useState(0)`         |
| `this.count++`                 | `setCount(count + 1)` |
| Change Detection               | Re-render             |
| Template updates automatically | Component re-renders  |

---

# Why React Needs State

This does NOT work:

```tsx
function Counter() {

  let count = 0;

  const increment = () => {
    count++;
  };

  return (
    <button onClick={increment}>
      {count}
    </button>
  );
}
```

When button is clicked:

```tsx
count++;
```

Variable changes, but React does not know it should update the UI.

So React provides:

```tsx
const [count, setCount] = useState(0);
```

Now React tracks the value.

---

# Understanding useState

```tsx
const [count, setCount] = useState(0);
```

Equivalent thinking:

```typescript
let count = 0;

function setCount(newValue) {
    count = newValue;

    // React triggers re-render
}
```

React internally does much more, but conceptually this is what happens.

---

# Example: Textbox

## Angular

```typescript
name = '';
```

```html
<input [(ngModel)]="name">

<p>{{ name }}</p>
```

Typing updates:

```typescript
name
```

automatically.

---

## React TSX

```tsx
const [name, setName] = useState<string>("");
```

```tsx
<input
  value={name}
  onChange={(e) => setName(e.target.value)}
/>

<p>{name}</p>
```

Typing calls:

```tsx
setName(...)
```

which updates state and re-renders.

---

# State with Object

## Angular

```typescript
user = {
  name: 'Ahmad',
  age: 35
};

this.user.age = 36;
```

Angular detects changes.

---

## React

```tsx
const [user, setUser] = useState({
  name: "Ahmad",
  age: 35
});
```

Wrong:

```tsx
user.age = 36;
```

Correct:

```tsx
setUser({
  ...user,
  age: 36
});
```

React prefers creating a **new object** rather than modifying the existing one.

---

# State with Array

## Angular

```typescript
employees.push(newEmployee);
```

Usually works.

---

## React

Wrong:

```tsx
employees.push(newEmployee);
```

Correct:

```tsx
setEmployees([
  ...employees,
  newEmployee
]);
```

Again, create a new array.

---

# Mental Model for Angular Developers

Think of React State as:

```typescript
@Component Property
+
Change Notification
+
Automatic UI Refresh
```

Example mapping:

| Angular              | React TSX                               |
| -------------------- | --------------------------------------- |
| `count = 0`          | `const [count, setCount] = useState(0)` |
| `this.count = 5`     | `setCount(5)`                           |
| `user.name = 'John'` | `setUser({...user, name:'John'})`       |
| Template binding     | JSX expression `{count}`                |
| Change Detection     | Re-render                               |

---

# Interview Question

**Q: What is State in React?**

**Answer:**

State is a component's internal data that can change over time. When state changes through a state setter function such as `setCount`, React re-renders the component and updates the UI.

```tsx
const [count, setCount] = useState(0);
```

For an Angular developer, React State is similar to a component property that automatically triggers a UI refresh when updated through React's state management mechanism.
