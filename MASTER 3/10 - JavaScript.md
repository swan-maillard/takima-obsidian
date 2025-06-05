---
cover: "[[javascript.png]]"
---
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

JavaScript is a **scripting language** that is **dynamically typed**, **prototype-based**, and heavily supports **functional programming**. It was originally created for the browser, but now runs server-side (via Node.js) and beyond.

## 1. Core Characteristics:
- **Dynamically Typed**: Types are assigned at runtime.
- **Prototype-Oriented OOP**: Instead of defining blueprints (classes), you create a **prototype object**, and other objects are cloned or extended from it.
- **Single-Threaded with Event Loop**: Manages async operations using a non-blocking model.
- **Standardized by ECMAScript (ES)**: One new version released annually (ES2025 is the latest).
    
## 2. Runtime Architecture
- **Call Stack**: Manages execution context (LIFO).
- **Heap**: Memory space for dynamic data and objects.
- **Event Loop**: Handles async tasks (via callbacks, promises, async/await).
- **Web APIs (browsers)** and **Core Modules (Node.js)**: Provide features like timers, HTTP, DOM, file access.
    

---

# 💠 ECMAScript (ES)

**ECMAScript** defines the core JS syntax and behavior. Major versions have introduced essential features:

## 1. Key Milestones
- **ES5** (2009): Strict mode, `Array.forEach`, getters/setters.
- **ES6 / ES2015**: `let`, `const`, arrow functions, promises, classes, modules.
- **ESNext**: Catch-all term for upcoming proposals (e.g., private fields `#name`).
- **ES2025** _(latest)_: Introduces **pattern matching** (like `match` in Rust/Scala).

## 2. Popular Features
- **Arrow Functions**: Short syntax, lexical `this`.
- **Destructuring**, **Spread/Rest**
- **Optional Chaining (`?.`)**, **Nullish Coalescing (`??`)**
- **Modules**: `import/export`
- **Async/Await**: Cleaner async code.
- **Symbol**, **BigInt**: New primitive types for uniqueness and large numbers.

---

# 💠 Functions & Concepts

## 1. Pure Functions
- Always produce the same output for the same input.
- No side effects (don’t modify external state).
- Idempotent.

## 2. Closures
- A closure is a function that **"remembers"** its parent scope even after the outer function has returned.

```js
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  };
}
```

## 3. Callback
- A function passed as a parameter to another function.
- Often used in async logic.

```js
function greet(name, callback) {
  callback(`Hello, ${name}`);
}
```

## 4. Promise
- Represents an async operation’s eventual result.
- Replaces nested callbacks (callback hell).

```js
fetch(url).then(response => ...).catch(error => ...)
```

## 5. Async/Await
- Built on top of Promises.
- Allows writing async code like it's synchronous.

```js
const data = await fetchData();
```

---

# 💠 DOM (Document Object Model)

The DOM is a **tree-like representation** of the structure of a web page.

Browsers provide the **DOM API**, as well as the **BOM API** (Browser Object Model) which comes with the **Fetch API** and **WebSockets API**.

---

# 💠 Bundlers & Build Tools

Bundlers improve JS performance and compatibility.
Common bundlers are **Webpack**, **Rollup** (used by Vite) or **Parcel**

What they do:
- Combine multiple JS/CSS/assets into fewer files.
- **Transpile** modern JS or TypeScript → older JS (via Babel, ESBuild).
- Enable `import` of non-JS assets (images, styles).
- Optimize output: **tree shaking**, **minification**, **obfuscation**, **code splitting**.


---

# 💠 Polyfills

A **polyfill** is a piece of code (usually JS) that **emulates a modern feature** in older browsers.

- Automatically included via Babel or core-js.
- Ensures consistent behavior across environments.

---

# 💠 TypeScript (TS)

**TypeScript** is a statically typed superset of JavaScript compiled into plain JS.

- **Static Typing**: Types are checked at compile-time.
- **Interfaces**, **Type Aliases**: Define the shape of data.
- **Enums**, **Generics**, **Decorators** (experimental).
- **Type Inference** and **Narrowing**
- **Great Tooling**: IntelliSense, autocompletion, type safety.
- Interpolates with JS code.


---

# 💠 Frameworks & Libraries

## 1. Frameworks
- **Angular**: Complete app framework with DI, forms, routing.
- **Vue.js**: Lightweight, reactive UI framework.
- **Next.js**: React-based with SSR, API routes, full-stack capabilities.

## 2. Libraries
- **React**: Library for building UIs (component-based).
- **Babel**: Transpiler that converts ES6+ into compatible JS.

## 3. Differences

| **Library**                                  | **Framework**                      |
| -------------------------------------------- | ---------------------------------- |
| A library is a tool                          | A framework is a full structure    |
| You use it when you need it                  | It tells you how to build your app |
| You write the main code and call the library | The framework calls your code      |

---

# 💠 OPS (DevOps in JS Ecosystem)

- **NPM / Yarn**: Package managers.
- **ESLint / Prettier**: Linting & formatting.
- **Husky**: Git hook automation (pre-commit, pre-push).
- **i18n**: Internationalization libraries (e.g., `react-i18next`, `yarn i18n`)

---

# 💠 Testing

- **Jest**: All-in-one unit/integration test runner.
- **Vitest**: Fast Vite-native test framework.
- **Cypress**, **Playwright**: End-to-end testing in real browsers.