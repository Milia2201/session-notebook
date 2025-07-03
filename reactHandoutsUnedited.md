# React Basics

## Learning Objectives

- [ ] Understanding what React is and why it is used
- [ ] Learn the differences between JSX and HTML
- [ ] Explore the declarative approach of React
- [ ] Creating React components
- [ ] Understanding rendering with React
- [ ] Project Scaffolding with the Vite tool

---

## What is React and Why Do We Use It?

React is a **JavaScript library** for building user interfaces. It allows developers to:

- Create **reusable components** to organize and simplify their code.
- Focus on **what the UI should look like** (declarative), while React handles the how behind the scenes.

Unlike **Vanilla JS**, where you manage the DOM manually, React abstracts this process for efficiency.

### Introduction to JSX

**JSX** is a syntax extension for JavaScript that looks like HTML but behaves like JavaScript. It allows you to **describe the UI declaratively**.

```jsx
const element = <p>Hello World!</p>;
```

Key Points:

- JSX looks like HTML but is transformed into JavaScript that the browser can understand.
- Files containing JSX typically use the `.jsx` file extension.
- JSX expressions can include JavaScript code wrapped in curly braces `{}`

```jsx
const name = "React";
const element = <p>Hello {name}!</p>; // Outputs: Hello React!
```

### Imperative vs Declarative Programming

To understand the difference between imperative and declarative code, let's look at an example of a simple button.

> ❗️ The main difference between imperative and declarative code is that imperative code describes _how_ something should be built, and declarative code describes _what_ needs to be built.

#### Imperative Code in Vanilla JavaScript

You describe how the UI is built step by step.

```js
const button = document.createElement("button");
button.type = "button";
button.textContent = "click me";
button.addEventListener("click", () => console.log("Hello World"));
document.body.append(button);
```

- We create the element with `document.createElement()`
- We set the button type,
- We set the text content
- We add the event listener
- We append the button to the body

#### Declarative Code in React + JSX

You describe what the UI should look like.

```jsx
const element = (
  <button type="button" onClick={() => console.log("Hello World")}>
    click me
  </button>
);
```

- We describe in JSX what element we want (in this case a button element)
- React figures out how to update the DOM according to our description

> 💡 A metaphor: Image you are really hungry. You have two options:
>
> The Vanilla JavaScript way would be to cook a meal yourself. You would have to go to the grocery store, buy the ingredients, prepare them, cook them, and finally eat them.
>
> There is also the React way: You could just order food from a restaurant. You would just have to tell them what you want to eat, and they (React) would take care of the rest.

## React Components

React components are reusable, independent building blocks of a React application. Each component combines logic and appearance and represents a part of the user interface that can be used multiple times.

> 💡 Components can be as 'small' as a button or as 'big' as an entire page.

### Creating a Component

- A component is a function that returns JSX.

```jsx
function Button() {
  return (
    <button type="button" onClick={() => console.log("Hello World")}>
      click me
    </button>
  );
}
```

### Using Components

- Use the component as a custom HTML tag:

```js
export default function App() {
  return (
    <div>
      <Button />
      <Button />
      <Button />
    </div>
  );
}
```

Key Rules:

- Components must have PascalCase names.
- Components must return JSX with one parent element.

This is a very powerful concept, because it allows us to reuse the same component in multiple places in our application.

> 📙 Read about [**Your First Component**
> in the React Docs](https://react.dev/learn/your-first-component).

---

## Nesting Elements

JSX elements in a React component can be nested the same way we have been nesting our HTML elements.

```jsx
function Card() {
  return (
    <div>
      <p>Some Text</p>
      <p>Some more Text</p>
    </div>
  );
}
```

## Attributes

In most cases the names for attributes are the same as in HTML, but there are some exceptions. For example, the `class` attribute from HTML is called `className` in JSX.

```jsx
const element = <p className="text">Some Text</p>;
```

> 📙 Find out more about the [differences in attributes](https://legacy.reactjs.org/docs/dom-elements.html#differences-in-attributes)

---

Passing string values to attributes is done by using double quotes. To pass any JavaScript expression use curly braces.

```jsx
const myValue = "This is a string";
const input = <input type="text" value={myValue} minLength={5} />;
```

### Dynamic Values in JSX

To make components dynamic, you can insert JavaScript expressions into JSX using curly braces `{}`.

```js
export default function App() {
  const buttonText = "click with React";
  return (
    <button type="button" onClick={() => console.log("Hello React!")}>
      {buttonText}
    </button>
  );
}
```

```js
const name = "Pawtricia";
const element = <p>My cat's name is {name}</p>;
```

```js
const a = 5;
const b = 10;

const element = (
  <p>
    {a} + {b} = {a + b}
  </p>
);
```

> 💡 You can only use **expressions** inside JSX. Statements like `if/else` or `for`-loops are not allowed.

> 📙 Read more about [**JavaScript in JSX with Curly Braces**
> in the React Docs](https://react.dev/learn/javascript-in-jsx-with-curly-braces).

---

## How React Renders

React needs a **root element** in the DOM to render your application. This root acts as the entry point where React mounts its components

**HTML**

```html
<div id="root"></div>
```

In most projects, this code is already provided in templates or starters. A typical setup looks like this:

```js
const rootElement = document.getElementById("root");
const root = createRoot(rootElement);

root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

- `App`: The root React component of your application.
- `StrictMode`: A development-only tool that highlights potential issues in your code without affecting the visible UI.

### How React Updates the DOM

React works **smart, not hard**. It uses the Virtual DOM to track changes and efficiently updates only the parts of the DOM that have changed compared to the last render.

Benefits:

- React avoids unnecessary updates, ensuring fast rendering.
- Focus remains consistent, and inputs keep their values.
- Declarative code is easier to write and understand.

## Nice to know: React, JSX, Transpilers and Bundlers

React uses JSX, a syntax extension that lets us write HTML-like code in JavaScript. However, JSX is not standard JavaScript, so it needs to be transformed into regular JavaScript that browsers can understand.

- Transpilers (e.g., Babel)

  - Convert JSX into standard JavaScript code that browsers can run.
  - Example: JSX like `<h1>Hello</h1>` gets converted to `createElement(...)`.

- Bundlers (e.g., Vite or Rollup)
  - Combine all project files (JS, JSX, CSS) into optimized bundles.
  - Automatically run the transpiler when needed.
  - Provide a development server with live reloading when you run:

```sh
  npm run dev
```

### Importing CSS Files

Bundlers allow you to use non-standard features, like importing CSS files directly into JavaScript:

```js
import "./styles.css";
```

- The bundler transforms this into a `<link>` tag in the final HTML.
- This simplifies managing styles in modern JavaScript projects.

---

## npm

[npm](https://www.npmjs.com/) (Node Package Manager) is a package registry for JavaScript projects. It allows you to:

- Install and manage libraries (called packages):

```sh
  npm install package-name
```

- Run project scripts defined in `package.json`, like starting the development server.

```sh
  npm run dev
```

---

## `package.json`

The `package.json` file is the configuration file for your project. It includes:

- Metadata: Project name, version, and description.
- `dependencies`: Libraries your app needs to run.
- `devDependencies`: Tools needed for development (e.g., linters, bundlers).
- `scripts`: Shortcuts for running commands like starting a development server.

A `package.json` may look something like this:

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "A description of my app",
  "scripts": {
    "test": "npm run …"
  },
  "author": "Alex Newfish",
  "license": "UNLICENSED",
  "dependencies": {
    "my-dependency": "^10.4.1",
    "my-other-dependency": "^2.0.0"
  },
  "devDependencies": {
    "my-dev-dependency": "^8.0.105",
    "my-other-dev-dependency": "^0.1.6"
  }
}
```

### Installing dependencies

To install all dependencies listed in `package.json`, run:

```sh
 npm install
```

> 💡 Always run `npm install` after cloning a project to set up its dependencies.

- `node_modules`:

  - Contains all installed packages (dependencies).
  - **Do not commit this folder** to your repository as it is large and can be regenerated using npm install.
  - Add `node_modules` to your `.gitignore` file to exclude it from version control.

- `package-lock.json`:
  - Stores the exact versions of installed dependencies to ensure consistency across different environments and team members.
  - **Should be committed** to the repository to avoid unexpected changes caused by newer versions of a package.

---

## Setting Up a React Project with Vite

[Vite](https://vitejs.dev/guide/) automates project scaffolding and setup, saving time.

> 💡 In principle, you could create a new React project from scratch. However, this would be a lot of work and we would have to set up a lot of things ourselves.

> 💡 Vite, by the way, works quite similar to the `ghcd` tool you have probably already used.

A new project is created by running the following command in the terminal:

```sh
  npm create vite@latest my-react-app
```

- If running this command for the first time, you need to install the `create-vite` package, accept and continue.
- Select `React` as the framework and the `JavaScript` template (without SWC – speedy web compiler).
- Navigate into your project folder:

```sh
  cd my-first-react-app
  npm install
  npm run dev
```

### Project Structure

Here’s a quick overview of key files and folders:

| File / Folder        | Description                                                                       | contains                                                                           |
| -------------------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| README.md            | general info about project                                                        | reminder how to start the dev-server                                               |
| package.json         | project configuration                                                             | information about dependencies, scripts, metadata                                  |
| vite.config.js       | configuration for vite                                                            | Configurations for basic behavior of dev server, bundler, plugin management.       |
| node_modules folder  | dependencies                                                                      | all dependencies of the project                                                    |
| index.html           | root html file, don't mess with the `div id="root"></div>`                        | root element for React, script tag for `src/main.jsx` file                         |
| **public folder**    | static assets that are not processed by the bundler                               | vite.svg                                                                           |
| **src folder**       | all source code that will go through Rollup processing                            | all JavaScript, JSX, CSS, and other files that make up your React application.     |
| main.jsx / index.jsx | The JavaScript entry point where ReactDOM renders the App component into the DOM. | imports react-dom and the App component                                            |
| App.jsx              | The root component of the React app                                               | typically where you start writing your app's code and organizing other components. |
| App.css              | CSS file for the App component                                                    | styles for the App component                                                       |
| index.css            | CSS file for global styles                                                        | css variables, style resets, fonts                                                 |

---

## Resources

- [What is React: A Visual Introduction For Beginners on learnreact.design](https://learnreact.design/posts/what-is-react)
- [Writing Markup with JSX in the React Docs](https://react.dev/learn/writing-markup-with-jsx)
- [JavaScript in JSX with Curly Braces in the React Docs](https://react.dev/learn/javascript-in-jsx-with-curly-braces)
- [Your First Component in the React Docs](https://react.dev/learn/your-first-component)
- [Difference between a Framework and a Library on freecodecamp](https://www.freecodecamp.org/news/the-difference-between-a-framework-and-a-library-bd133054023f/)
- [Vite Getting Started](https://vitejs.dev/guide/)

- Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-basics/react-basics.md?plain=1

  ------------------------------------------------------------------------------------------------------------------------------------------------
# React Props

## Learning Objectives

- [ ] Understanding what props are
- [ ] Understanding how to pass props to a component
- [ ] Understanding how to use props in a component
- [ ] Understanding how to render conditionally

---

## Using Props

Props is short for properties. They are a way to pass data to a child component. A component receives a props object as the first function parameter.

Props are [passed to a component as attributes](#passing-props-to-a-component).

```js
function UserCard(props) {
  return <div>{props.name}</div>;
}
```

For convenience the props object is often destructured in the function parameter.

```js
function UserCard({ name }) {
  return <div>{name}</div>;
}
```

You can choose any names for your props.

> 💡 There are some naming conventions though. Boolean props are often prefixed with `is`, `has` or `should`. For example `isDisabled`, `hasError` or `shouldShow`. Props that take functions are often prefixed with `on`. For example `onClick`, `onSubmit` or `onHover`. Following these conventions makes it easier to understand the purpose of the prop.

Props can be of any type (string, number, array, object, function, ...).

You should treat the props object as immutable and read-only.

---

## Passing Props to a Component

Props are passed to a component as attributes.

```js
<UserCard name="Alex" />
```

You can pass any type of data as a prop.

```js
<UserCard
  name="Alex"
  age={25}
  onContact={() => console.log("let's chat!")}
  isFavorite={true}
  favoriteFoods={["Pasta", "Salad"]}
  contactDetails={{ email: "alex@neuefische.de", phone: "123456789" }}
/>
```

String props can be passed using double quotes. All other props must be passed using curly braces.

> 💡 Notice the double curly braces for the object. This is because the outer curly braces are used to signify a JavaScript expression. The inner curly braces are used to define an object.

> 💡 There is a shorthand syntax for boolean props. If the value should be `true` you can omit the value.
>
> ```js
> <UserCard isFavorite />
> ```

Omitting any attribute will result in the value `undefined` for that prop.

> 📙 Read more about [**Passing props to a Component**
> in the React Docs](https://react.dev/learn/passing-props-to-a-component).

### Conditional Rendering

You can use props to conditionally render parts of a component.

```js
function UserCard({ name, isFavorite }) {
  return (
    <div>
      {name}
      {isFavorite ? <span>🌟</span> : null}
    </div>
  );
}
```

> 💡 In JSX `null` is a way to render nothing.

You can not use an `if` statement within JSX because only expressions are allowed. You can use an `if` statement outside of the JSX though.

```js
function UserCard({ name, isFavorite }) {
  let favoriteStar = null;
  if (isFavorite) {
    favoriteStar = <span>🌟</span>;
  }

  return (
    <div>
      {name}
      {favoriteStar}
    </div>
  );
}
```

> 📙 Read more about [**Conditional Rendering**
> in the React Docs](https://react.dev/learn/conditional-rendering).

---

## Resources

- [Passing props to a Component in the React Docs](https://react.dev/learn/passing-props-to-a-component)
- [Conditional Rendering in the React Docs](https://react.dev/learn/conditional-rendering)

- Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-props/react-props.md?plain=1
  
    ------------------------------------------------------------------------------------------------------------------------------------------------

    ------------------------------------------------------------------------------------------------------------------------------------------------

    ------------------------------------------------------------------------------------------------------------------------------------------------

    ------------------------------------------------------------------------------------------------------------------------------------------------

    ------------------------------------------------------------------------------------------------------------------------------------------------

  
