Since you already know Angular and TypeScript, let's understand **React Props** by comparing them directly with Angular's **@Input()**.

# What are Props?

**Props (Properties)** are data passed from a parent component to a child component.

Think of Props as:

| Angular                      | React                        |
| ---------------------------- | ---------------------------- |
| `@Input()`                   | `props`                      |
| One-way data flow            | One-way data flow            |
| Parent → Child communication | Parent → Child communication |

---

# Angular Example

### Child Component

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-user',
  template: `<h2>{{name}}</h2>`
})
export class UserComponent {
  @Input() name!: string;
}
```

### Parent Component

```html
<app-user [name]="'Ahmad'"></app-user>
```

Output:

```text
Ahmad
```

---

# React Equivalent (JavaScript - JSX)

### Child Component

```jsx
function User(props) {
  return <h2>{props.name}</h2>;
}
```

### Parent Component

```jsx
<User name="Ahmad" />
```

Output:

```text
Ahmad
```

---

# React with TypeScript (TSX)

In real projects, TypeScript is preferred.

### Define Props Type

```tsx
type UserProps = {
  name: string;
};
```

### Child Component

```tsx
function User(props: UserProps) {
  return <h2>{props.name}</h2>;
}
```

### Parent Component

```tsx
<User name="Ahmad" />
```

---

# Destructuring Props (Common React Style)

Instead of:

```tsx
function User(props: UserProps) {
  return <h2>{props.name}</h2>;
}
```

Most React developers write:

```tsx
function User({ name }: UserProps) {
  return <h2>{name}</h2>;
}
```

Angular equivalent mentally:

```typescript
@Input() name!: string;
```

Both expose `name` directly.

---

# Multiple Props

## Angular

```typescript
@Input() name!: string;
@Input() age!: number;
```

```html
<app-user
    [name]="'Ahmad'"
    [age]="35">
</app-user>
```

---

## React TSX

```tsx
type UserProps = {
  name: string;
  age: number;
};

function User({ name, age }: UserProps) {
  return (
    <>
      <h2>{name}</h2>
      <p>{age}</p>
    </>
  );
}
```

```tsx
<User
  name="Ahmad"
  age={35}
/>
```

---

# Passing Objects

## Angular

```typescript
@Input() employee!: Employee;
```

```html
<app-user [employee]="employee"></app-user>
```

---

## React

```tsx
type Employee = {
  id: number;
  name: string;
};

type UserProps = {
  employee: Employee;
};

function User({ employee }: UserProps) {
  return <h2>{employee.name}</h2>;
}
```

```tsx
<User employee={employee} />
```

---

# Passing Functions

This is extremely common in React.

## Angular

Child emits event:

```typescript
@Output() save = new EventEmitter<void>();
```

Parent listens:

```html
<app-user (save)="onSave()"></app-user>
```

---

## React

Parent passes function as prop.

### Parent

```tsx
function onSave() {
  alert("Saved");
}

<User onSave={onSave} />
```

### Child

```tsx
type UserProps = {
  onSave: () => void;
};

function User({ onSave }: UserProps) {
  return (
    <button onClick={onSave}>
      Save
    </button>
  );
}
```

Angular mental model:

```text
@Output() EventEmitter
≈
Function Prop
```

---

# Props are Read-Only

In Angular:

```typescript
@Input() name!: string;
```

You should not modify it inside child.

Same in React:

```tsx
function User({ name }: UserProps) {
  name = "New Name"; // ❌ Bad
}
```

Props are immutable.

Think:

```text
Parent owns data.
Child receives data.
```

---

# Real Enterprise Example

Imagine a list of employees.

### Angular

```html
<app-employee-card
   *ngFor="let emp of employees"
   [employee]="emp">
</app-employee-card>
```

---

### React

```tsx
{employees.map(emp => (
  <EmployeeCard
    key={emp.id}
    employee={emp}
  />
))}
```

Child:

```tsx
function EmployeeCard(
  { employee }: EmployeeCardProps
) {
  return (
    <div>
      {employee.name}
    </div>
  );
}
```

---

# TypeScript Benefits

Without TypeScript:

```jsx
<User age="Thirty Five" />
```

No compile-time error.

With TypeScript:

```tsx
type UserProps = {
  age: number;
};
```

```tsx
<User age="Thirty Five" />
```

Error:

```text
Type 'string' is not assignable to type 'number'
```

Similar to Angular's strong typing.

---

# Interview Question

### What are Props in React?

**Answer:**

Props are read-only inputs passed from a parent component to a child component. They enable component reusability and support one-way data flow. Props are similar to Angular's `@Input()` decorator.

---

# Angular Developer Cheat Sheet

| Angular                | React                                    |
| ---------------------- | ---------------------------------------- |
| Component              | Component                                |
| @Input()               | Props                                    |
| @Output() EventEmitter | Callback Function Prop                   |
| ngFor                  | map()                                    |
| ngIf                   | Conditional Rendering                    |
| Service                | Context / Custom Hooks / State Libraries |
| Template HTML          | JSX / TSX                                |
| Two-way Binding        | State + Event Handler                    |
| Dependency Injection   | Hooks / Context                          |

**One-line memory trick:**

> **React Props = Angular @Input() + TypeScript Interface describing the data being passed.**
