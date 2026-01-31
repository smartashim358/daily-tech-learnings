# React Core Concepts -- State, Props, and Routing & Day 20

This guide is written in a practical, developer‑friendly way.\
No unnecessary theory. Only what you need to **understand and build real
apps**.

------------------------------------------------------------------------

## 1. React State Management

### What is State?

**State = Component's Memory**

State stores data that can change over time.\
When state changes → React automatically re‑renders the UI.

Example: Counter App

``` jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>{count}</h2>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}

export default Counter;
```

### Key Points

-   `useState()` is a Hook.
-   First value = current state.
-   Second value = function to update state.
-   Updating state triggers re‑render.

### When to Use State

-   Form inputs
-   Toggle buttons
-   API data
-   Counters
-   UI visibility (modal, dropdown)

------------------------------------------------------------------------

## 2. Props in React

### What are Props?

**Props = Data passed from Parent → Child Component**

Props are **read‑only**.\
Child components **cannot modify** them.

Example:

``` jsx
function Welcome(props) {
  return <h1>Hello {props.name}</h1>;
}

function App() {
  return <Welcome name="Ashim" />;
}
```

### Modern Syntax (Destructuring)

``` jsx
function Welcome({ name }) {
  return <h1>Hello {name}</h1>;
}
```

### Key Points

-   Props make components reusable.
-   One‑way data flow.
-   Parent controls the data.

------------------------------------------------------------------------

## 3. React Routing (React Router)

Routing allows switching pages **without reloading the browser**.

Install:

``` bash
npm install react-router-dom
```

Basic Setup:

``` jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

function Home() {
  return <h1>Home</h1>;
}

function About() {
  return <h1>About</h1>;
}

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

Navigation Links:

``` jsx
import { Link } from "react-router-dom";

<Link to="/about">Go to About</Link>
```

### Key Points

-   `BrowserRouter` wraps the app.
-   `Routes` contains all routes.
-   `Route` defines path → component.
-   `Link` prevents page reload.

------------------------------------------------------------------------

## Real‑World Mental Model

-   **State** → Data inside component.
-   **Props** → Data from parent.
-   **Routing** → Navigation between pages.

If you master these three → You can build 70% of React apps.

------------------------------------------------------------------------

## Developer Insight

A professional React developer:

-   Keeps state minimal.
-   Uses props for reusability.
-   Structures routing early in the project.
-   Avoids unnecessary global state.

Clean React = Small Components + Clear Data Flow.
