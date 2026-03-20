# 🚀 My First React 19.2 Application with TypeScript

> **Note**
> This guide was created on March 20, 2026, using the latest versions:
> **React 19.2.4** · **TypeScript 5.9.3** · **Vite 8.0.1** · **Node.js 22.22.0**

---

## 📋 Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Project Creation](#2-project-creation)
3. [Project Structure Explained](#3-project-structure-explained)
4. [Understanding Each File](#4-understanding-each-file)
5. [Key React Concepts](#5-key-react-concepts)
6. [Running the Application](#6-running-the-application)
7. [Next Steps](#7-next-steps)

---

## 1. Prerequisites

Before creating a React app, you need:

| Tool | Minimum Version | Your Version | ✅ |
|------|----------------|-------------|---|
| **Node.js** | 20.19+ or 22.12+ | v22.22.0 | ✅ |
| **npm** | 10+ | v11.8.0 | ✅ |

> **Tip**
> Download Node.js from [nodejs.org](https://nodejs.org). npm comes bundled with Node.js.

---

## 2. Project Creation

### Why Vite?

**Vite** (French for "fast") is the **recommended** tool for creating React applications in 2026. It replaced the old `create-react-app` which is now deprecated. Key advantages:

- ⚡ **Instant dev server startup** (no bundling during development)
- 🔥 **Hot Module Replacement (HMR)** – see changes instantly without refreshing
- 📦 **Optimized production builds** using Rollup
- 🔧 **First-class TypeScript support** out of the box

### The Command

```powershell
npx -y create-vite@latest ./ --template react-ts
```

Let's break this down:

| Part | Meaning |
|------|---------|
| `npx -y` | Execute an npm package without installing it globally. `-y` auto-accepts installation. |
| `create-vite@latest` | The Vite project scaffolding tool, using the latest version. |
| `./` | Create the project in the **current directory**. |
| `--template react-ts` | Use the **React + TypeScript** template. |

> **Important**
> Other available templates: `react` (JavaScript), `react-swc-ts` (TypeScript with SWC compiler, even faster), `vue-ts`, `svelte-ts`, etc.

---

## 3. Project Structure Explained

Here's the complete project structure that was generated:

```
MyFirst Application with React/
├── 📁 node_modules/          # All installed dependencies (don't edit!)
├── 📁 public/                # Static assets served as-is
│   └── favicon.svg           # Browser tab icon
├── 📁 src/                   # YOUR APPLICATION CODE lives here
│   ├── 📁 assets/            # Images, fonts, etc. (processed by Vite)
│   │   ├── hero.png
│   │   ├── react.svg
│   │   └── vite.svg
│   ├── App.css               # Styles specific to the App component
│   ├── App.tsx                # The main App component
│   ├── index.css              # Global styles
│   └── main.tsx               # Application entry point
├── .gitignore                 # Files to exclude from Git
├── eslint.config.js           # Linting configuration
├── index.html                 # The single HTML page (SPA entry)
├── package.json               # Project metadata and dependencies
├── package-lock.json          # Exact dependency versions (auto-generated)
├── tsconfig.json              # TypeScript configuration (root)
├── tsconfig.app.json          # TypeScript config for app code
├── tsconfig.node.json         # TypeScript config for build tools
└── vite.config.ts             # Vite build configuration
```

> **Tip**
> **Key difference between `public/` and `src/assets/`:**
> - `public/` → Files served **as-is**, no processing. Good for `robots.txt`, favicons.
> - `src/assets/` → Files **processed by Vite** (optimized, hashed filenames, inlined if small).

---

## 4. Understanding Each File

### 4.1 `index.html` — The Single Page

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>myfirst-application-with-react</title>
  </head>
  <body>
    <!-- 👇 This empty div is where React renders your entire app -->
    <div id="root"></div>
    <!-- 👇 This loads your TypeScript entry point -->
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
```

**Key takeaway:** React is a **Single Page Application (SPA)** framework. There's only ONE HTML file. React dynamically generates and updates the page content inside `<div id="root">`.

---

### 4.2 `src/main.tsx` — The Entry Point

```tsx
import { StrictMode } from 'react'          // 1️⃣ Import StrictMode
import { createRoot } from 'react-dom/client' // 2️⃣ Import the renderer
import './index.css'                          // 3️⃣ Import global styles
import App from './App.tsx'                   // 4️⃣ Import your main component

// 5️⃣ Find the <div id="root"> and render the App inside it
createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```

| Concept | Explanation |
|---------|-------------|
| `createRoot()` | **React 19 API** for rendering. Replaced `ReactDOM.render()` from older React. |
| `document.getElementById('root')!` | Gets the `<div id="root">` from `index.html`. The `!` is TypeScript's **non-null assertion** (we're sure this element exists). |
| `<StrictMode>` | A development helper that warns you about deprecated patterns. Has **no effect in production**. |
| `<App />` | Your root component — the entire app starts here. |

---

### 4.3 `src/App.tsx` — Your Main Component

```tsx
import { useState } from 'react'           // Import the useState Hook
import reactLogo from './assets/react.svg'  // Import images as URLs
import viteLogo from './assets/vite.svg'
import heroImg from './assets/hero.png'
import './App.css'                          // Import component styles

function App() {
  // 👇 Declare a state variable "count" with initial value 0
  const [count, setCount] = useState(0)

  return (
    <>
      <section id="center">
        <div className="hero">
          <img src={heroImg} className="base" width="170" height="179" alt="" />
          <img src={reactLogo} className="framework" alt="React logo" />
          <img src={viteLogo} className="vite" alt="Vite logo" />
        </div>
        <div>
          <h1>Get started</h1>
          <p>
            Edit <code>src/App.tsx</code> and save to test <code>HMR</code>
          </p>
        </div>
        {/* 👇 Button with click handler that updates state */}
        <button
          className="counter"
          onClick={() => setCount((count) => count + 1)}
        >
          Count is {count}
        </button>
      </section>
      {/* ... more sections ... */}
    </>
  )
}

export default App
```

> **Important — Critical React concepts in this file:**
> - **JSX/TSX** — HTML-like syntax inside TypeScript. React converts it to JavaScript.
> - **`className`** not `class` — Because `class` is a reserved word in JavaScript.
> - **`<> ... </>`** — A **Fragment**. Groups elements without adding an extra DOM node.
> - **`{curly braces}`** — Embed JavaScript expressions inside JSX.

---

### 4.4 `vite.config.ts` — Vite Configuration

```typescript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],     // Enables React support (JSX transform, HMR)
})
```

This is intentionally minimal. You can extend it with options like:
- `server.port` — Change the dev server port
- `build.outDir` — Change the build output directory
- `resolve.alias` — Create import path shortcuts

---

### 4.5 `tsconfig.app.json` — TypeScript Configuration

```jsonc
{
  "compilerOptions": {
    "target": "ES2023",              // Output modern JavaScript
    "lib": ["ES2023", "DOM"],        // Available APIs
    "module": "ESNext",              // Use ES modules
    "jsx": "react-jsx",             // Use the modern JSX transform (no need to import React)
    "strict": true,                  // Enable all strict type-checking
    "noUnusedLocals": true,          // Error on unused variables
    "noUnusedParameters": true,      // Error on unused function parameters
    "moduleResolution": "bundler",   // Let Vite handle module resolution
    "noEmit": true                   // TypeScript only checks types, Vite does the build
  },
  "include": ["src"]                 // Only check files in src/
}
```

> **Tip**
> **`"jsx": "react-jsx"`** means you DON'T need to write `import React from 'react'` at the top of every component file. The new JSX transform (since React 17) handles this automatically.

---

### 4.6 `package.json` — Project Configuration

```json
{
  "name": "myfirst-application-with-react",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",                 // 🟢 Start dev server
    "build": "tsc -b && vite build", // 📦 Build for production
    "lint": "eslint .",            // 🔍 Check code quality
    "preview": "vite preview"      // 👁️ Preview production build
  },
  "dependencies": {
    "react": "^19.2.4",            // React core library
    "react-dom": "^19.2.4"         // React DOM renderer
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^6.0.1",  // Vite React plugin
    "typescript": "~5.9.3",            // TypeScript compiler
    "vite": "^8.0.1",                  // Vite build tool
    "eslint": "^9.39.4",               // Code linter
    // ... other dev dependencies
  }
}
```

| Script | Command | Purpose |
|--------|---------|---------|
| `npm run dev` | `vite` | Start the development server with HMR |
| `npm run build` | `tsc -b && vite build` | Type-check, then create production bundle |
| `npm run lint` | `eslint .` | Check code for errors and style issues |
| `npm run preview` | `vite preview` | Preview the production build locally |

---

## 5. Key React Concepts

### 5.1 Components

React apps are built from **components** — reusable, self-contained pieces of UI.

```tsx
// A simple component (function that returns JSX)
function Welcome({ name }: { name: string }) {
  return <h2>Hello, {name}!</h2>
}

// Using the component
<Welcome name="Luis" />
```

### 5.2 State with `useState`

**State** is data that can change over time. When state changes, React **re-renders** the component.

```tsx
const [count, setCount] = useState(0)
//     ↑          ↑                ↑
//   value    setter function   initial value
```

### 5.3 Props (Properties)

**Props** are how you pass data from a parent to a child component:

```tsx
// Parent
<Greeting name="Luis" age={30} />

// Child
function Greeting({ name, age }: { name: string; age: number }) {
  return <p>{name} is {age} years old</p>
}
```

### 5.4 TypeScript Benefits in React

TypeScript adds **type safety** to React, catching bugs at compile time:

```tsx
// ✅ TypeScript catches errors BEFORE you run the code
interface User {
  name: string
  email: string
  age: number
}

function UserCard({ user }: { user: User }) {
  return (
    <div>
      <h3>{user.name}</h3>
      <p>{user.email}</p>
      {/* TypeScript would error if you wrote user.phone (doesn't exist!) */}
    </div>
  )
}
```

### 5.5 React 19 New Features

React 19.2 includes several new features you'll eventually use:

| Feature | Description |
|---------|-------------|
| **`use()` Hook** | Read resources (Promises, Context) directly in render |
| **Server Components** | Components that render on the server (with frameworks like Next.js) |
| **Actions** | Simplified form handling with `<form action={...}>` |
| **`useOptimistic`** | Show optimistic UI updates before server confirms |
| **`useFormStatus`** | Track form submission state |
| **Document Metadata** | Render `<title>`, `<meta>` directly in components |

---

## 6. Running the Application

### Start the Development Server

```powershell
npm run dev
```

This starts the Vite dev server. Open your browser to:

🌐 **http://localhost:5173/**

You'll see the default Vite + React starter page with:
- The React and Vite logos
- A "Get started" heading
- A counter button that increments when clicked

### Try Hot Module Replacement (HMR)

1. Open `src/App.tsx`
2. Change `<h1>Get started</h1>` to `<h1>Hello React 19! 🎉</h1>`
3. **Save the file** → The browser updates **instantly** without refreshing!

### Build for Production

```powershell
npm run build
```

This creates an optimized `dist/` folder ready for deployment.

---

## 7. Next Steps

Now that you understand the project structure, here's a suggested learning path:

```
✅ Project Setup
    ↓
📝 Create Custom Components
    ↓
🎨 Add Styling
    ↓
🔄 Learn useState & useEffect
    ↓
📡 Fetch Data from APIs
    ↓
🧭 Add Routing (react-router)
    ↓
📦 State Management
    ↓
🚀 Deploy to Production
```

### Recommended Resources

| Resource | Link |
|----------|------|
| 📖 Official React Docs | [react.dev](https://react.dev) |
| 🎓 React Tutorial | [react.dev/learn](https://react.dev/learn) |
| ⚡ Vite Documentation | [vite.dev](https://vite.dev) |
| 🔷 TypeScript Handbook | [typescriptlang.org/docs](https://www.typescriptlang.org/docs/) |

---

> **Quick experiment to try right now:**
> 1. Create a new file `src/MyButton.tsx`
> 2. Create a simple button component
> 3. Import and use it in `App.tsx`
> This is the fundamental React workflow: **create components → compose them together**!
