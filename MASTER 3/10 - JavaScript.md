
# 💠Table of Contents
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 2 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: true # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```

---

# 💠 JavaScript Core Concepts

JavaScript executes within a **runtime environment** that enriches the language with additional capabilities depending on the platform—such as browser APIs (e.g., the DOM) or Node.js modules (e.g., file system access). The runtime consists of several key components:

- **Call Stack**: A data structure that keeps track of function calls and their execution order.
    
- **Heap**: A memory space used for storing objects and dynamic data.
    
- **Event Loop**: Coordinates asynchronous tasks by handling the execution of callbacks, promises, and other deferred operations.
    
- **Web APIs** (in browsers) or **Core Modules** (in Node.js): Provide essential asynchronous features like timers, HTTP requests, and DOM manipulation, enabling non-blocking operations.


---

# 💠 ECMAScript

**ECMAScript** is the standardized specification that defines the core syntax, types, and behavior of JavaScript. Modern JavaScript development is guided by its evolving features.

Founded with **ES5**, got modernized with **ES6 (ES2015)**
### Key Features:
- **Lexical Scoping** with `let`, `const`, `var`
- **Arrow Functions** for cleaner syntax
- **Promises**, `async/await` for async handling
- **Modules** with `import/export`
- **Destructuring**, **spread/rest operators**
- **Optional chaining (`?.`)**, **nullish coalescing (`??`)**

---

# 💠 DOM (Document Object Model)

DOM is the interface between JavaScript and the browser's rendered HTML.

### Core Concepts:
- **Selectors**: `getElementById`, `querySelector`
- **Event Handling**: `addEventListener`
- **DOM Manipulation**: `appendChild`, `innerHTML`, `classList`
- **Browser APIs**: `fetch`, `localStorage`, `History API`

---

# 💠 Bundlers & Build Tools

Bundlers are essential tools in modern JavaScript development. They take your project’s source code (written in modules, often with newer syntax or multiple files) and **bundle** it into one or more optimized files for use in the browser or Node.js.

## 1. Why Bundlers Matter

Before bundlers, developers had to manage dozens of `<script>` tags or use older build systems. Bundlers solve key problems:

- Combine multiple files/modules into fewer files (typically one or a few).
- Transpile modern JS (ES6+) or TypeScript into backwards-compatible code.
- Minify and optimize assets (JS, CSS, images).
- Support hot module replacement (HMR) for faster development.
- Integrate tools like linters, preprocessors, or testing frameworks.

## 2. Common Tools:

- **Webpack**: Highly configurable, powerful ecosystem.
- **Vite**: Fast dev server with ES modules.
- **Rollup**: Great for libraries, tree-shaking focus.

---

# 💠 TypeScript

**TypeScript** is a typed superset of JavaScript that compiles to plain JS.

### Key Advantages:
- **Static Typing**: Catch errors at compile time.
- **Interfaces & Types**: Define shapes of data.
- **Enums**, **Generics**, **Decorators**
- **Tooling Support**: Autocompletion, refactoring, IntelliSense.

---

# 💠 OPS (DevOps in JS World)

## 1. Tooling for Ops/Build:

- **NPM/Yarn**: Package managers.
- **ESLint**, **Prettier**: Linting and formatting.
- **Husky**: Adds git hooks like pre-commit

---

# 💠 Testing

## 1. Frameworks:
- **Jest**: Unit and integration testing.
- **Vitest**: Fast Vite-based test runner.
- **Cypress**, **Playwright**: End-to-end browser testing.

---

# 💠 Craftsmanship

- **Separation of concerns**: Clear layering (UI, logic, data).
- **Functional programming**: Prefer immutability, pure functions.
- **Modular code**: Small, reusable components.
- **Code reviews** and **pair programming**
- **Refactoring** regularly to keep tech debt low.
- **Design Patterns**: Observer, Module, Factory, etc.