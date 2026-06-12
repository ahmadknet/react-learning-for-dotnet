Perfect. Since you already know **Angular** and **C#**, let's learn **React Components through the lens of Angular Components**, using **TypeScript (TSX)** from the start.

---

# What is a Component?

A Component is a **self-contained UI unit** that contains:

1. UI (HTML/JSX)
2. Logic (TypeScript)
3. Data
4. Events

Think:

```text
Component = Screen Section + Logic
```

Examples:

```text
Header Component
Login Component
Employee Component
Search Component
Footer Component
```

---

# Angular Component

You already know this:

```typescript
@Component({
  selector: 'app-header',
  template: `
    <h1>Employee Portal</h1>
  `
})
export class HeaderComponent {
}
```

Usage:

```html
<app-header></app-header>
```

---

# React Component (TSX)

Equivalent:

```tsx
function Header() {
  return (
    <h1>Employee Portal</h1>
  );
}
```

Usage:

```tsx
<Header />
```

---

# First Mental Model

For Angular developers:

```text
Angular Component Class
           =
React Function Component
```

---

Angular:

```typescript
export class EmployeeComponent {
}
```

React:

```tsx
function Employee() {
}
```

---

# How React Thinks

Angular:

```text
Component
   |
   +-- Template
   +-- Class
```

React:

```text
Function
   |
   +-- Returns UI
```

The function itself is the component.

---

# Angular File Structure

```text
employee.component.ts
employee.component.html
employee.component.css
```

Three files.

---

# React File Structure

```text
Employee.tsx
Employee.css
```

Often only two files.

Sometimes even:

```text
Employee.tsx
```

only.

---

# Example: Employee Component

## Angular

employee.component.ts

```typescript
@Component({
  selector: 'app-employee',
  template: `
      <h2>Ahmad</h2>
      <p>.NET Developer</p>
  `
})
export class EmployeeComponent {
}
```

---

## React TSX

```tsx
function Employee() {
  return (
    <>
      <h2>Ahmad</h2>
      <p>.NET Developer</p>
    </>
  );
}
```

Same purpose.

Different syntax.

---

# Component Naming

Angular:

```typescript
EmployeeComponent
HeaderComponent
```

---

React:

```tsx
Employee
Header
```

Usually no "Component" suffix.

---

# Component Tree

Angular:

```text
AppComponent
   |
   +-- HeaderComponent
   |
   +-- EmployeeComponent
   |
   +-- FooterComponent
```

---

React:

```text
App
   |
   +-- Header
   |
   +-- Employee
   |
   +-- Footer
```

Exactly the same concept.

---

# Component Composition

This is the most important concept.

Small components combine into larger components.

---

Header:

```tsx
function Header() {
  return <h1>Portal</h1>;
}
```

---

Footer:

```tsx
function Footer() {
  return <h1>Footer</h1>;
}
```

---

App:

```tsx
function App() {
  return (
    <>
      <Header />
      <Footer />
    </>
  );
}
```

Think:

```text
App
 |
 +-- Header
 |
 +-- Footer
```

This is called:

```text
Component Composition
```

---

# C# Analogy

Imagine a C# class:

```csharp
public class EmployeeCard
{
    public string Render()
    {
        return "<h2>Employee</h2>";
    }
}
```

Usage:

```csharp
var card = new EmployeeCard();
```

---

React:

```tsx
<EmployeeCard />
```

React creates and renders the component instance.

---

# Why Components Matter

Imagine an Employee Management Screen.

Without Components:

```tsx
5000 lines in one file
```

Nightmare.

---

With Components:

```text
EmployeePage
    |
    +-- SearchBar
    |
    +-- EmployeeGrid
    |
    +-- EmployeeCard
```

Each developer can work independently.

---

# TypeScript Component

A proper React TypeScript component:

```tsx
function Employee(): JSX.Element {
  return (
    <div>
      Employee Details
    </div>
  );
}
```

This tells TypeScript:

```text
This function returns UI
```

However, in modern React you'll often see:

```tsx
function Employee() {
  return (
    <div>
      Employee Details
    </div>
  );
}
```

TypeScript infers the return type automatically.

---

# Angular vs React Architecture

## Angular

```text
Component
 |
 +-- HTML
 |
 +-- TS Class
 |
 +-- Dependency Injection
 |
 +-- Lifecycle Methods
```

---

## React

```text
Component
 |
 +-- TSX Function
 |
 +-- Hooks
 |
 +-- JSX
```

React is simpler.

Fewer concepts.

---

# Enterprise Example

Suppose you're building a Job Portal.

Components:

```text
App
 |
 +-- Navbar
 |
 +-- JobSearch
 |
 +-- JobList
 |
 +-- JobCard
 |
 +-- Footer
```

---

JobCard might be:

```tsx
function JobCard() {
  return (
    <div>
      <h3>.NET Developer</h3>
      <p>Mumbai</p>
    </div>
  );
}
```

---

JobList might use multiple JobCards:

```tsx
function JobList() {
  return (
    <>
      <JobCard />
      <JobCard />
      <JobCard />
    </>
  );
}
```

This is exactly how large React applications are built.

---

# Angular Developer Summary

When you see this Angular code:

```typescript
@Component({
  selector: 'app-employee'
})
export class EmployeeComponent {
}
```

Mentally translate it to:

```tsx
function Employee() {
  return (
    <div>
      Employee Component
    </div>
  );
}
```

---

# Key Takeaway

For an Angular developer:

```text
Angular Component
       =
React Component
```

The biggest difference is:

```text
Angular:
Class + Decorators + Template

React:
Function + JSX/TSX + Hooks
```

Don't think of a React Component as something completely new. Think of it as an **Angular Component rewritten as a TypeScript function that returns UI**. Once that clicks, Props become simply the React equivalent of `@Input()`, and State becomes the React equivalent of component properties that change over time.
