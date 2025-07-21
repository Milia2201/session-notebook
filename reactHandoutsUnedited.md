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
# React Nesting

## Learning Objectives

- Understanding the concept of nesting
- Creating multiple custom components to create a hierarchy
- Using the `children` prop to render JSX from the parent component
- Understanding composition as a way to build complex components

---

## Passing JSX as Props

Elements created by JSX are just objects. They can be passed around like any other object: for example, as props.

```js
function UserCard({ avatar }) {
  return <div className="card">{avatar}</div>;
}
```

```js
function App() {
  return <UserCard avatar={<Avatar />} />;
}
```

## The `children` Prop

You are already familiar with nesting built-in browser tags:

```js
<div>
  <img />
</div>
```

Oftentimes you'd want your own components to be nestable as well.

```js
<UserCard>
  <Avatar />
</UserCard>
```

If you nest a component inside of another component, the nested component is passed as a prop to the parent component. This special prop is called `children`.

```jsx
function UserCard({ children }) {
  return <div className="card">{children}</div>;
}
```

This component will render the nested element(s) as a child of the `div` element.

> 💡 The nested element(s) can be a single element, multiple elements, or even a string or number.

> 📙 Read more about [**Passing JSX as children**
> in the React Docs](https://react.dev/learn/passing-props-to-a-component#passing-jsx-as-children).

## Fragments

Sometimes you want to return multiple elements from a component function without wrapping them in a `div` or other element. You can use a `Fragment` (`<></>` or `<Fragment></Fragment>`) for this.

This is necessary because React components can only return a single element from a component function.

```jsx
function UserList() {
  return (
    <>
      <UserCard>
        <Avatar />
      </UserCard>
      <UserCard>
        <Avatar />
      </UserCard>
    </>
  );
}
```

This is equivalent to the following, but the shorthand version above is generally preferred.

```jsx
import { Fragment } from "react";

function UserList() {
  return (
    <Fragment>
      <UserCard>
        <Avatar />
      </UserCard>
      <UserCard>
        <Avatar />
      </UserCard>
    </Fragment>
  );
}
```

> 💡 The `<Fragment></Fragment>` syntax is only necessary if you want to pass the special `key` prop to the fragment, which will become important when you start working with lists.

> 💡 When researching you sometimes might see `<React.Fragment></React.Fragment>`, which is the same thing.

> 📙 Read more about [**Fragment (<>...</>)**
> in the React Docs](https://react.dev/reference/react/Fragment).

---

## Composition

When we build React applications, we often want to build complex components from simpler components. This is called composition.

To do so you need to break down you application into components. You can then compose these components to build more complex components.

It is important to figure out which components you need and how they should be composed. This is called application design.

> 📙 Read [**Thinking in React**
> in the React Docs](https://react.dev/learn/thinking-in-react) up to and including Step 2. Later steps require state, which we will cover in a future session.

---

## Resources

- [Passing JSX as children in the React Docs](https://react.dev/learn/passing-props-to-a-component#passing-jsx-as-children)
- [Fragment (<>...</>) in the React Docs](https://react.dev/reference/react/Fragment)
- [Thinking in React in the React Docs](https://react.dev/learn/thinking-in-react)

  Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-nesting/react-nesting.md?plain=1
  ------------------------------------------------------------------------------------------------------------------------------------------------

  # React State 1

## Learning Objectives

- [ ] Knowing how to attach events in React
- [ ] Understanding the concept of "state"
- [ ] Using `useState()` to handle state in React
- [ ] Understanding the React Lifecycle

---

## What is state?

State is data that changes over time. Think of the lamp on your desk. It can be switched on or
switched off. The lamp is in a particular state at a given time and that state can change over time.

Another example could be the amount of money in your purse. At any given time you have a certain amount
of money in your purse, but the amount of money can change. The state of your purse can change.
Going to the grocery store will decrease the amount of money, while going to the ATM will increase
it.

This concept also applies to software. Your app can have data that changes over time.

Think of a post on a social media app. You might have liked a specific post, or not. The "liked"
state of a post can be on or off, like the lamp on your desk.

The website of your bank refers to your purse in the analog world. At any given time, the banking software
displays the current balance of your account, the current state. You can use the banking software to
change that state. For example you could transfer money to another account to decrease the number
stored in the "balance" state.

Oftentimes such stateful data changes after a user interaction, like a click on a button.

---

## State in React

In React we work with state by using the `useState` hook function.

We call the `useState` function and pass the **initial state** value as argument. This is the value
that is used in our app until something changes.

Calling the `useState` function gives us two things in return:

- a variable with the **current state** as value
- the `set` function to set a **new state**

```js
import { useState } from "react";

function SocialMediaPost() {
  const [liked, setLiked] = useState(false);

  function toggleLiked() {
    setLiked(!liked);
  }

  return (
    <article>
      <p>Liked: {liked ? "Yes" : "No"}</p>
      <button type="button" onClick={toggleLiked}>
        {liked ? "Remove like" : "Add like"}
      </button>
    </article>
  );
}
```

> 💡 There is a naming convention for React apps that the state variable and the function always
> follow the pattern of `x` and `setX`

> 📙 Read more about the
> [**concept of state** in the React Docs](https://react.dev/learn/adding-interactivity).

In React state is encapsulated per instance of a component. Think of a feed in a social media app.
The feed is a list of posts. Each post is an individual instance of the `SocialMediaPost` component,
each with individual state. When you change the "liked" state of one specific post, all other posts
stay as they are.

A React component can have multiple states. You can use the `useState` function as much as you need.

You can store all kinds of data in state (like booleans, numbers, strings, objects or arrays).

```js
import { useState } from "react";

function SocialMediaPost() {
  const [liked, setLiked] = useState(false);
  const [comments, setComments] = useState([]);
  const [views, setViews] = useState(0);

  /* ... */

  return <article>{/* ... */}</article>;
}
```

---

## What happens when state changes?

To handle state in React we can not simply use a "normal" variable and assign a new value. React
needs to be informed that the data was changed.

This is related to the render cycle of React components.

When React renders a component it executes the component function, which returns JSX. If the JSX
includes a state variable, it uses the variable's value at that time to place into the JSX. Calling
the `set` function with a new value informs React, that the state has changed.

> 💡 Changing a state triggers a re-render of the component.

When re-rendering the component, React executes the component function again from top to bottom,
which will again return JSX. However, this time the variable has a new value - the value that was
passed with the call of the `set` function. This means the return JSX includes the new value.

> 📙 Read more about
> [**state updates and re-rendering** in the React Docs](https://react.dev/learn/render-and-commit).

---

## Resources

- [React Docs: Adding Interactivity](https://react.dev/learn/adding-interactivity)
- [React Docs: Responding to Events](https://react.dev/learn/responding-to-events)
- [React Docs: State: A Component's Memory](https://react.dev/learn/state-a-components-memory#when-a-regular-variable-isnt-enough)
- [React Docs: Render and Commit](https://react.dev/learn/render-and-commit)
- [MDN: React Events and State](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_interactivity_events_state)

  Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-state-1/react-state-1.md?plain=1
  
    ------------------------------------------------------------------------------------------------------------------------------------------------
# React with Arrays

## Learning Objectives

- [ ] Knowing how to use `.map()` to render lists in JSX
- [ ] Understanding how to render items from an array of objects
- [ ] Knowing to add a unique key for list items

---

## Arrays in JSX

To render elements from an array in React we use the array method `.map()`.

The array method `.map()` is used to apply a transformation to all items of an array. When rendering
an array to JSX we like to do exactly this. We like to transform each item of an array into a JSX
tag. This is why we are using `.map()`.

```js
function Drinks() {
  const drinks = ["water", "lemonade", "coffee", "tee"];

  return (
    <ul>
      {drinks.map((drink) => (
        <li>{drink}</li>
      ))}
    </ul>
  );
}
```

---

## Key Property

The example above misses a tiny, but very important part: the `key` prop!

Without the `key` prop you will see an error in the console:

> `Warning: Each child in a list should have a unique "key" prop.`

When rendering an array in JSX you need to pass a **unique identifier** as value for the `key` prop
of the first JSX tag returned in `.map()`. This is important for React to keep track of changes that
happens to the data when re-rendering.

Therefore you must always make sure your array contains a unique id per item. You can ensure this by
using objects to define the data in your arrays.

```js
function Drinks() {
  const drinks = [
    { id: 0, name: "water" },
    { id: 1, name: "lemonade" },
    { id: 2, name: "coffee" },
    { id: 3, name: "tea" },
  ];

  return (
    <ul>
      {drinks.map(({ id, name }) => (
        <li key={id}>{name}</li>
      ))}
    </ul>
  );
}
```

> 📙 If you are interested in understanding the details behind this, you can read about
> [**the `key` prop** in the React Docs](https://react.dev/learn/rendering-lists#keeping-list-items-in-order-with-key).

> 💡 If you pass the `key` prop to a component, you cannot access it in the component. It is a special prop that React only uses internally.
>
> ```js
> function Drink({ name, key }) {
>   console.log(key); // → undefined
>   return <li>{name}</li>;
> }
>
> function Drinks() {
>   const drinks = [
>     { id: 0, name: "water" },
>     { id: 1, name: "lemonade" },
>     { id: 2, name: "coffee" },
>     { id: 3, name: "tea" },
>   ];
>
>   return (
>     <ul>
>       {drinks.map(({ id, name }) => (
>         <Drink key={id} name={name} />
>       ))}
>     </ul>
>   );
> }
> ```
>
> If you want to access the `id` in this example you can pass it again as a prop:  
> `<Drink key={id} id={id} name={name} />`.

## Keyed Fragments

If you are rendering a list of items that are not wrapped in a single JSX tag, you can use a
`<Fragment>` to wrap the items.

```js
import { Fragment } from "react";

function Drinks() {
  const drinks = [
    { id: 0, name: "water", description: "very wet" },
    { id: 1, name: "lemonade", description: "quite sweet" },
    { id: 2, name: "coffee", description: "cold brew" },
    { id: 3, name: "tea", description: "earl grey, hot" },
  ];

  return (
    <dl>
      {drinks.map(({ id, name, description }) => (
        <Fragment key={id}>
          <dt>{name}</dt>
          <dd>{description}</dd>
        </Fragment>
      ))}
    </dl>
  );
}
```

> 💡 Here you cannot use the short syntax (`<>…</>`) for the `<Fragment>` because you need to
> pass the `key` prop to the `<Fragment>`. The short syntax does not allow to pass props.

---

## Resources

- [React Docs: Rendering Lists](https://react.dev/learn/rendering-lists)

- Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-with-arrays/react-with-arrays.md?plain=1
    ------------------------------------------------------------------------------------------------------------------------------------------------
# React State 2

## Learning Objectives

- [ ] Knowing how to handle form fields: controlled components, uncontrolled components
- [ ] Knowing how to handle form submit events
- [ ] Understanding the concept of lifting state up
- [ ] Knowing how to pass state and functions via props
- [ ] Understanding that state updates are not synchronous
- [ ] Knowing what a `hook` in React is and which rules apply to hooks

---

## Sharing State Between Components

### Passing State Down

The value of a state variable and the setter function can be passed down to child components as
props. They are functions and values, so they can be passed down like any other data.

```js
function Parent() {
  const [count, setCount] = useState(0);

  function handleIncrement() {
    setCount(count + 1);
  }

  return <Child count={count} onIncrement={handleIncrement} />;
}
```

```js
function Child({ count, onIncrement }) {
  return (
    <>
      <p>Count: {count}</p>
      <button onClick={onIncrement}>increment</button>
    </>
  );
}
```

### Lifting State Up

When we have multiple components that need to share state, we can lift the state up to the parent
component and pass it down as props. This is called "lifting state up" because you usually start with
the state directly in the child component and then move it up to the parent components as you need
it in more and more components.

A state variable can be passed down to multiple child components. The child components can then
update the state variable by calling the setter function.

Any state variable should live as low in the component tree as possible but has high as needed. If
the whole `App` needs to know about the state variable, it should live in the `App` component. If
only child components of the `Article` need to know about the state variable, it should live in the
`Article` component.

Consider the following example:

<img src="./assets/lifting-state-up.png" width="616" height="694" />

Here we find that a `Link` in the `Navigation` component needs to know about a state that previously
existed in the `Article` component. We can lift the state up to the `App` component and pass it down
to the `Article` component as a prop.

> 📙 Read more about
> [**Sharing State Between Components** in the React docs](https://react.dev/learn/sharing-state-between-components).

## Handling Form Data

### Using Form Data `onSubmit`

We can use the `onSubmit` event handler to handle form data. The `onSubmit` event handler is called
when the user submits the form. We can get the form data (just like with regular JavaScript) from
the `event` object.

```js
function SearchForm() {
  function handleSubmit(event) {
    event.preventDefault();
    const form = event.target;
    const searchTerm = form.elements.searchTerm.value;
    console.log("A new search term was submitted:", searchTerm);
  }
  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="searchTerm">Search</label>
      <input name="searchTerm" id="searchTerm" />
      <button>Search</button>
    </form>
  );
}
```

In this example the input elements value is not manually controlled by React: The input is an
"uncontrolled input". It's value is managed by the browser. In the submit event handler we just
"peek" at the input field and read the value from the DOM.

### Using Controlled Inputs

We can use React to control the value of an input element. This is called a "controlled input". This
means that we manually set the value attribute of the input element. We can wire up a state variable
to the value attribute of the input element. This way the input element will always have the same
value as the state variable. Combined with the `onChange` event handler we can update the state
variable when the user types in the input field.

```js
function SearchForm() {
  const [searchTerm, setSearchTerm] = useState("");

  function handleSubmit() {
    event.preventDefault();
    console.log("A new search term was submitted:", searchTerm);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="searchTerm">Search</label>
      <input
        name="searchTerm"
        id="searchTerm"
        value={searchTerm}
        onChange={(event) => setSearchTerm(event.target.value)}
      />
      <button>Search for {searchTerm}</button>
    </form>
  );
}
```

In this example you always know the value of the search term input. Since it is a state variable,
you can use it in other places in your application. You should prefer using uncontrolled inputs
when possible, but sometimes you need to use a controlled input.

You might need a controlled input when

- showing search results while the user is typing,
- autocompleting the user's input or
- validating the user's input.

## State Updates are not Immediate

When we call the setter function of a state variable, React will not immediately update the state
variable. Instead, it will update it's internal value and schedule a re-render of the component.

```js
// ⚠️ This code is broken!
function Counter() {
  const [count, setCount] = useState(0); // count is 0 initially

  function handleIncrement() {
    // when this is first called, count is still 0
    console.log(count); // → 0

    // this will set reacts internal state to 1,
    // but does not update the count variable
    setCount(count + 1);
    console.log(count); // → 0

    // the count variable is still 0, thus count + 1 is still 1,
    // so react's internal state will still be 1
    setCount(count + 1);
    console.log(count); // → 0

    // since setter functions were called
    // react will schedule a re-render of
    // the component with the new count value of 1
  }

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={handleIncrement}>increment by 2</button>
    </>
  );
}
```

This behavior can be unexpected, but it is important to understand that state variables are not
immediately updated.

There are a few ways to fix the code above. In this example we could call `setCount(count + 2)` and
be done. If for some reason we need to call `setCount` twice, we can use the functional form of the
setter function, which provides the current internal value of the state variable as an argument.

```js
// ⚠️ This code is unnecessary complicated, but it works!
function Counter() {
  const [count, setCount] = useState(0); // count is 0 initially

  function handleIncrement() {
    // when this is first called, count is still 0
    console.log(count); // → 0

    // this will set reacts internal state to 1,
    // but does not update the count variable
    setCount((prevCount) => prevCount + 1);
    console.log(count); // → 0

    // the internal value of count is 1,
    // we get it as the the first parameter of the function we pass to the setter.
    // 1 + 1 is 2, so react's internal state will now be _2_
    setCount((prevCount) => prevCount + 1);
    console.log(count); // → 0

    // since setter functions were called
    // react will schedule a re-render of
    // the component with the new count value of _2_
  }

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={handleIncrement}>increment by 2</button>
    </>
  );
}
```

> 💡 Here the prefix `prev` is used to indicate that the value is the previous value of the state
> variable. Another common convention is to use the just the first letter of the state variable as
> the parameter name: `setCount(c => c + 1)`.

> 📙 Read more about
> [**Updating state based on the previous state**](https://react.dev/reference/react/useState#updating-state-based-on-the-previous-state)
> and
> [**I’ve updated the state, but logging gives me the old value**](https://react.dev/reference/react/useState#ive-updated-the-state-but-logging-gives-me-the-old-value)
> in the React docs.

## React Hooks

The `useState` function is part of a broader set of features of react that give components extra
powers.

Hooks are functions that allow component functions to hook into React features (like state) and
allow components to do more than a traditional JavaScript function can. They follow the naming
convention `useXzy`.

Common hooks that you'll come across are `useState` and `useEffect`.

When using hooks you need to follow a few rules:

- Only call hooks at the top level. Don’t call Hooks inside loops, conditions, or nested functions.
- Only call hooks from React function components or custom hooks. Don’t call Hooks from regular
  JavaScript functions.

> 📙 Read more about [**Hooks** in the React Docs](https://reactjs.org/docs/hooks-overview.html)
> from when they were introduced to React.

---

## Resources

- [Sharing State Between Components in the React Docs](https://react.dev/learn/sharing-state-between-components)
- [Updating state based on the previous state in the React Docs](https://react.dev/reference/react/useState#updating-state-based-on-the-previous-state)
- [I’ve updated the state, but logging gives me the old value in the React Docs](https://react.dev/reference/react/useState#ive-updated-the-state-but-logging-gives-me-the-old-value)
- [Hooks at a Glance in the React Docs](https://reactjs.org/docs/hooks-overview.html)

  Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-state-2/react-state-2.md?plain=1
  
    ------------------------------------------------------------------------------------------------------------------------------------------------
# React State 3

## Learning Objectives

- [ ] Knowing how to handle arrays and objects in state
- [ ] Knowing what state mutation is and how to avoid it

---

## Avoiding State Mutation

Regardless of how complex the state you have in your application (object, array, array of objects) is, you must always treat state as immutable.
This means that you should not directly mutate the state, e.g. with reassigning a new value to it.

To avoid mutation when updating state, you need to

1. create a new object / array (or make a copy of the existing one), and
2. use the setter function with the recently created / updated copy in order to cause a re-render.

---

## Updating Objects in State

To make a copy of an object and change only some properties, you can use the spread syntax:

```js
const [person, setPerson] = useState({
  firstName: "John",
  lastName: "Doe",
});

function handleChangeFirstName(firstName) {
  setPerson({ ...person, firstName });
}

// Somewhere else:
handleChangeFirstName("Jane");
```

> ❗️ If you were to assign a new value directly, you would mutate the state. This is bad because we must treat state as immutable. Doing so can lead to hard to find bugs.
>
> ```js
> // ⚠️ NEVER DO THIS
> function handleChangeFirstName(firstName) {
>   person.firstName = firstName;
>   setPerson(person);
> }
> ```

> 📙 Learn more about [**Updating Objects in State** in the React Docs](https://react.dev/learn/updating-objects-in-state).

---

## Updating Arrays in State

As you know, there are several ways to update arrays. Some of them, however, mutate the array, and some
of them don't.

|           | avoid (mutates the array)           | prefer (returns a new array) |
| --------- | ----------------------------------- | ---------------------------- |
| adding    | `push`, `unshift`                   | `[...arr]` spread syntax     |
| removing  | `pop`, `shift`, `splice`            | `filter`                     |
| replacing | `splice`, `arr[i] = ...` assignment | `map`                        |
| sorting   | `reverse`, `sort`                   | copy the array first         |

> 💡 It does not matter whether your array state contains only primitives or other objects / arrays;
> in all cases, you should only use the preferred array methods.

### Adding to an Array

To add an element to an array, you can use the spread syntax:

```js
const [numbers, setNumbers] = useState([0, 1, 2]);

function handleAppendNumber(number) {
  setNumbers([...numbers, number]);
}

// Somewhere else:
handleAppendNumber(3);

function handlePrependNumber(number) {
  setNumbers([number, ...numbers]);
}

// Somewhere else:
handlePrependNumber(-1);
```

### Removing from an Array

To remove an element from an array, you can use the `filter` method:

```js
const [numbers, setNumbers] = useState([0, 1, 2]);

function handleRemoveNumber(numberToRemove) {
  setNumbers(numbers.filter((number) => number !== numberToRemove));
}

// Somewhere else:
handleRemoveNumber(1);
```

### Replacing an Array Element

To replace an element in an array, you can use the `map` method:

```js
const [numbers, setNumbers] = useState([0, 1, 2]);

function handleReplaceNumber(oldNumber, newNumber) {
  setNumbers(
    numbers.map((number) => {
      if (number === oldNumber) return newNumber;
      return number;
    })
  );
}

// Somewhere else:
handleReplaceNumber(1, 1337);
```

> 📙 Learn more about [**Updating arrays without mutation** in the React Docs](https://react.dev/learn/updating-arrays-in-state#updating-arrays-without-mutation).

---

## Updating Arrays of Objects in State

Most of the time, you will encounter arrays of objects in your state.

### Adding a new Object

You can add a new object to the state array by using the spread syntax:

```js
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleAddTree(tree) {
  setTrees([...trees, tree]);
}

// Somewhere else:
handleAddTree({id: 3, name: "Spruce", height: 13})
```

### Removing an Object

To remove an object, you can `filter` the array for a unique identifier. In most cases, this
identifier is in scope because the relevant object is rendered via `map`.

```js
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleRemoveTree(idToRemove) {
  setTrees(trees.filter((tree) => tree.id !== idToRemove));
}

// Somewhere else:
handleRemoveTree(0);
```

### Replacing an Object

To replace an object, you can use `map` to create a new array with the updated object. Remember to create a copy of the object first, otherwise you will mutate the state.

```js
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleSetNewHeightForTree(id, height) {
  setTrees(
    trees.map((tree) => {
      if (tree.id === id) return { ...tree, height };
      return tree;
    })
  );
}

// Somewhere else:
handleSetNewHeightForTree(0, 8);
```

### Sorting an Array of Objects

To sort an array of objects, you can use `sort` on a _copy of the array_ with a custom compare function. The compare function
returns a number, which is used to determine the order of the elements.

```js
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

function handleSortTreesByHeight() {
  setTrees([...trees].sort((a, b) => a.height - b.height));
}
```

> 📙 Learn more about [**Updating objects inside Arrays** in the React Docs](https://react.dev/learn/updating-arrays-in-state#updating-objects-inside-arrays).

## Choosing the State Structure

There are some common pitfalls when choosing your state structure.

### Group Related State

If you have state that belongs (and updates) together, group it into a single object. This makes it easier to update the state.

```js
// ❌ MEH
const [userName, setUserName] = useState("Alex");
const [userAge, setUserAge] = useState(28);

// ✅ BETTER
const [user, setUser] = useState({ name: "Alex", age: 28 });
```

### Avoid Redundant State

If you have a value that is derived from a state, you should avoid storing it in state. Instead just use a normal variable.

The problem with redundant state is that it can get out of sync with the source of truth if you forget to update it correctly.

```js
// ❌ BAD
const [user, setUser] = useState({ name: "Alex", age: 28 });
const [isAdult, setIsAdult] = useState(user.age >= 18);

// ✅ GOOD
const [user, setUser] = useState({ name: "Alex", age: 28 });
const isAdult = user.age >= 18;
```

### Avoid Duplication in State

Avoid storing the same value in multiple places in state. This can lead to bugs and makes it harder to update the state.

```js
// ❌ BAD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [selectedTree, setSelectedTree] = useState(trees.find((tree) => tree.id === 0));

// Somewhere else:
setSelectedTree(trees.find((tree) => tree.id === 2));


// ✅ GOOD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [selectedTreeId, setSelectedTreeId] = useState(0);

const selectedTree = trees.find((tree) => tree.id === selectedTreeId);

// Somewhere else:
setSelectedTreeId(2);
```

### Avoid Having Duplicate Lists in State

If you have a list of items in state, you should avoid storing a derived version of it in a different state variable. This is a common mistake when you want to display a filtered version of the list.

```js
// ❌ BAD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [filteredTrees, setFilteredTrees] = useState(trees.filter((tree) => tree.height > 7));

// Somewhere else:
setFilteredTrees(trees.filter((tree) => tree.height > 9));

// ✅ GOOD
const [trees, setTrees] = useState([
  { id: 0, name: "Oak", height 7.5},
  { id: 1, name: "Beech", height 6},
  { id: 2, name: "Pine", height 10}
]);

const [minHeight, setMinHeight] = useState(7);

const filteredTrees = trees.filter((tree) => tree.height > minHeight);

// Somewhere else:
setMinHeight(9);
```

> 📙 Read more about [**Choosing the State Structure** in the React Docs](https://react.dev/learn/choosing-the-state-structure). The Docs have many more examples and explanations.

---

## Resources

- [Updating Objects in State (React Docs)](https://react.dev/learn/updating-objects-in-state)
- [Updating Arrays in State (React Docs)](https://react.dev/learn/updating-arrays-in-state)

- Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-state-3/react-state-3.md?plain=1
    ------------------------------------------------------------------------------------------------------------------------------------------------
# React Effects and Fetch

## Learning Objectives

- [ ] Knowing that `fetch` is a side effect
- [ ] Knowing how to use the `useEffect` hook
- [ ] Understanding the callback function of `useEffect`
- [ ] Understanding the dependency array of `useEffect`
- [ ] Understanding the cleanup function of `useEffect`
- [ ] Knowing other side effects and cases for`useEffect`

---

## Effects in React

Effects are a way to synchronize React components with external systems.

Examples for interactions with external systems include:

- manipulating the DOM directly (e.g. setting the document title)
- making network requests to fetch data
- working with other Web APIs
- setting up and tearing down subscriptions and global event handlers
- setting timers
- integrating with third-party libraries.

Using an effect is an escape hatch from the declarative world of React. It is a way to run imperative code that is not directly related to rendering the UI. While the component function is required to be pure, effect functions by design are not. They encapsulate side effects.

An effect is defined as a function that is executed after the component was rendered (and the DOM was updated). It can be synchronized to run not only on mounting, but when all or only certain reactive values within the component function have changed.

Effect functions can return a cleanup function that is executed before the effect function runs again, or when the component is unmounted.

> 💡 A **reactive value** is a value that changes: props, state, derivatives thereof or values and functions declared inside of a component function.

> 💡 **Mounting** means a component was rendered, put into the DOM and displayed on the screen for first time. After that various updates and re-renders might occur (e.g. due to state changes). **Unmounting** means the component gets removed and is no longer displayed on the screen.

## `useEffect`

The `useEffect` hook is used to add effects to a React component. It takes two arguments:

- a function that defines the effect (usually an anonymous function)
- an array of variables that the effect depends on

For example, the following code will update the component title to the value of the `title` prop:

```js
import { useEffect } from "react";

function Title({ title }) {
  useEffect(() => {
    // updating the document title is a side effect
    // that is not directly related to rendering the UI
    document.title = title;
  });

  return <h1>{title}</h1>;
}
```

### Effect Dependencies

The effect above will run after the component was rendered and the DOM was updated. But that is way more often than necessary. The effect should only run when the `title` prop changes. To achieve this, we can pass an array of reactive values to the `useEffect()` hook. The effect will only run when one of the reactive values in the array changes.

```js
import { useEffect } from "react";

function Title({ title }) {
  useEffect(() => {
    document.title = title;
  }, [title]);

  return <h1>{title}</h1>;
}
```

This becomes important when the component function has more than one prop or state variable. Imagine having a `count` state in the component:

```js
import { useEffect, useState } from "react";

function Title({ title }) {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = title;
  }, [title]);

  return (
    <div>
      <h1>{title}</h1>
      <p>{count}</p>
      <button type="button" onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

The effect function will only run when the `title` variable is different from the previous value. The `count` state variable is not part of the array, so the effect will not run when the `count` state changes.

> 💡 Always add all reactive values that are used in the effect function to the array of dependencies. React comes with ESLint rules that will warn you if you forget to add a variable to the array of dependencies.
>
> **If the effect has no dependencies the dependency array should be empty: `[]`**.
>
> An empty dependency array tells React to run this effect only once: when the component appears on the screen for the first time.

### Cleanup Function

The effect function can return a cleanup function that is executed before the effect function runs again, or when the component is unmounted.

```js
import { useEffect } from "react";

function Title({ title }) {
  useEffect(() => {
    // make a copy of the old title
    const oldTitle = document.title;

    document.title = title;

    // cleanup function
    return () => {
      // undo what we have done by setting the old title again
      document.title = oldTitle;
    };
  }, [title]);

  return <h1>{title}</h1>;
}
```

The cleanup function should undo the side effects of the effect function. In the example above, the cleanup function resets the document title to the default value.

When the effect function is used to set up a subscription or global event handler, the cleanup function should remove the subscription or event handler.

```js
import { useEffect, useState } from "react";

function WindowWidth() {
  const [windowWidth, setWindowWidth] = useState();

  useEffect(() => {
    function handleResize(event) {
      setWindowWidth(event.target.innerWidth);
    }

    window.addEventListener("resize", handleResize);

    // cleanup function
    return () => {
      window.removeEventListener("resize", handleResize);
    };
  }, []);

  return <p>The window is {windowWidth}px wide. 📏</p>;
}
```

For timers, the cleanup function should clear the timer.

```js
import { useEffect, useState } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      setSeconds((s) => s + 1);
    }, 1000);

    // cleanup function
    return () => {
      clearInterval(timer);
    };
  }, []);

  return <p>The timer is at {seconds} seconds. ⏱</p>;
}
```

> 📙 Read more about [**Synchronizing with Effects** in the React docs](https://react.dev/learn/synchronizing-with-effects).

> 📙 Even though effects can be incredibly useful, you might not actually need an effect to do what you want. Read more about [**You might not need an effect** in the React docs](https://react.dev/learn/you-might-not-need-an-effect).

## How to Fetch Data in React

One of the most common use cases for effects is to fetch data from an external API.

The concept is as follows: After the component first renders, an effect function will run and fetch data from an external API. Once the data is fetched, a state variable is set from within the effect function. If the fetch is dependent on a prop or state variable, the effect function will run again when the variable changes.

The effect function itself can not be async, but it can call async functions. To get around this you can define an async function inside the effect function and call it immediately (without actually awaiting its result).

The following example shows how to fetch data from an API and display the data in a component:

```js
import { useEffect, useState } from "react";

function Jokes() {
  const [jokes, setJokes] = useState([]);

  useEffect(() => {
    async function startFetching() {
      const response = await fetch(
        "https://example-apis.vercel.app/api/bad-jokes"
      );
      const jokes = await response.json();

      setJokes(jokes);
    }

    startFetching();
  }, []);

  return (
    <ul>
      {jokes.map(({ id, joke }) => (
        <li key={id}>{joke}</li>
      ))}
    </ul>
  );
}
```

If the data you want to fetch is dependent on a prop or state variable, you need to add it to the array of variables that the effect depends on:

```js
import { useEffect, useState } from "react";

function Joke({ id }) {
  const [joke, setJoke] = useState();

  useEffect(() => {
    async function startFetching() {
      const response = await fetch(
        `https://example-apis.vercel.app/api/bad-jokes/${id}`
      );
      const joke = await response.json();

      setJoke(joke);
    }

    startFetching();
  }, [id]);

  if (!joke) {
    return null;
  }

  return <h2>{joke.joke}</h2>;
}
```

The above approach works well enough for simple use cases. It does not cover a few of important features, though:

- It does not handle race conditions. (If the user changes the `id` prop before the first fetch is complete, there is a chance that the wrong joke is displayed.)
- It does not handle loading states.
- It does not handle errors. (Neither network errors nor errors from the API.)
- It does not handle caching.

In the future we will use a data fetching library to address these issues.

> 💡 Even when you use a data fetching library, the library will use effects (and the `useEffect` hook) under the hood to fetch data.

> 📙 Read more about [**Fetching Data** in the React docs](https://react.dev/learn/synchronizing-with-effects#fetching-data). The docs also describe a way to handle race conditions.

---

## Resources

- [React docs: Synchronizing with Effects](https://react.dev/learn/synchronizing-with-effects)
- [React docs: Fetching data example with useEffect](https://react.dev/learn/synchronizing-with-effects#fetching-dat)
- [React docs: You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)

- Handout
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-effects-and-fetch/react-effects-and-fetch.md?plain=1
------------------------------------------------------------------------------------------------------------------------------------------------
  # React Effects and Fetch

## Learning Objectives

- [ ] Knowing that `fetch` is a side effect
- [ ] Knowing how to use the `useEffect` hook
- [ ] Understanding the callback function of `useEffect`
- [ ] Understanding the dependency array of `useEffect`
- [ ] Understanding the cleanup function of `useEffect`
- [ ] Knowing other side effects and cases for`useEffect`

---

## Effects in React

Effects are a way to synchronize React components with external systems.

Examples for interactions with external systems include:

- manipulating the DOM directly (e.g. setting the document title)
- making network requests to fetch data
- working with other Web APIs
- setting up and tearing down subscriptions and global event handlers
- setting timers
- integrating with third-party libraries.

Using an effect is an escape hatch from the declarative world of React. It is a way to run imperative code that is not directly related to rendering the UI. While the component function is required to be pure, effect functions by design are not. They encapsulate side effects.

An effect is defined as a function that is executed after the component was rendered (and the DOM was updated). It can be synchronized to run not only on mounting, but when all or only certain reactive values within the component function have changed.

Effect functions can return a cleanup function that is executed before the effect function runs again, or when the component is unmounted.

> 💡 A **reactive value** is a value that changes: props, state, derivatives thereof or values and functions declared inside of a component function.

> 💡 **Mounting** means a component was rendered, put into the DOM and displayed on the screen for first time. After that various updates and re-renders might occur (e.g. due to state changes). **Unmounting** means the component gets removed and is no longer displayed on the screen.

## `useEffect`

The `useEffect` hook is used to add effects to a React component. It takes two arguments:

- a function that defines the effect (usually an anonymous function)
- an array of variables that the effect depends on

For example, the following code will update the component title to the value of the `title` prop:

```js
import { useEffect } from "react";

function Title({ title }) {
  useEffect(() => {
    // updating the document title is a side effect
    // that is not directly related to rendering the UI
    document.title = title;
  });

  return <h1>{title}</h1>;
}
```

### Effect Dependencies

The effect above will run after the component was rendered and the DOM was updated. But that is way more often than necessary. The effect should only run when the `title` prop changes. To achieve this, we can pass an array of reactive values to the `useEffect()` hook. The effect will only run when one of the reactive values in the array changes.

```js
import { useEffect } from "react";

function Title({ title }) {
  useEffect(() => {
    document.title = title;
  }, [title]);

  return <h1>{title}</h1>;
}
```

This becomes important when the component function has more than one prop or state variable. Imagine having a `count` state in the component:

```js
import { useEffect, useState } from "react";

function Title({ title }) {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = title;
  }, [title]);

  return (
    <div>
      <h1>{title}</h1>
      <p>{count}</p>
      <button type="button" onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

The effect function will only run when the `title` variable is different from the previous value. The `count` state variable is not part of the array, so the effect will not run when the `count` state changes.

> 💡 Always add all reactive values that are used in the effect function to the array of dependencies. React comes with ESLint rules that will warn you if you forget to add a variable to the array of dependencies.
>
> **If the effect has no dependencies the dependency array should be empty: `[]`**.
>
> An empty dependency array tells React to run this effect only once: when the component appears on the screen for the first time.

### Cleanup Function

The effect function can return a cleanup function that is executed before the effect function runs again, or when the component is unmounted.

```js
import { useEffect } from "react";

function Title({ title }) {
  useEffect(() => {
    // make a copy of the old title
    const oldTitle = document.title;

    document.title = title;

    // cleanup function
    return () => {
      // undo what we have done by setting the old title again
      document.title = oldTitle;
    };
  }, [title]);

  return <h1>{title}</h1>;
}
```

The cleanup function should undo the side effects of the effect function. In the example above, the cleanup function resets the document title to the default value.

When the effect function is used to set up a subscription or global event handler, the cleanup function should remove the subscription or event handler.

```js
import { useEffect, useState } from "react";

function WindowWidth() {
  const [windowWidth, setWindowWidth] = useState();

  useEffect(() => {
    function handleResize(event) {
      setWindowWidth(event.target.innerWidth);
    }

    window.addEventListener("resize", handleResize);

    // cleanup function
    return () => {
      window.removeEventListener("resize", handleResize);
    };
  }, []);

  return <p>The window is {windowWidth}px wide. 📏</p>;
}
```

For timers, the cleanup function should clear the timer.

```js
import { useEffect, useState } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      setSeconds((s) => s + 1);
    }, 1000);

    // cleanup function
    return () => {
      clearInterval(timer);
    };
  }, []);

  return <p>The timer is at {seconds} seconds. ⏱</p>;
}
```

> 📙 Read more about [**Synchronizing with Effects** in the React docs](https://react.dev/learn/synchronizing-with-effects).

> 📙 Even though effects can be incredibly useful, you might not actually need an effect to do what you want. Read more about [**You might not need an effect** in the React docs](https://react.dev/learn/you-might-not-need-an-effect).

## How to Fetch Data in React

One of the most common use cases for effects is to fetch data from an external API.

The concept is as follows: After the component first renders, an effect function will run and fetch data from an external API. Once the data is fetched, a state variable is set from within the effect function. If the fetch is dependent on a prop or state variable, the effect function will run again when the variable changes.

The effect function itself can not be async, but it can call async functions. To get around this you can define an async function inside the effect function and call it immediately (without actually awaiting its result).

The following example shows how to fetch data from an API and display the data in a component:

```js
import { useEffect, useState } from "react";

function Jokes() {
  const [jokes, setJokes] = useState([]);

  useEffect(() => {
    async function startFetching() {
      const response = await fetch(
        "https://example-apis.vercel.app/api/bad-jokes"
      );
      const jokes = await response.json();

      setJokes(jokes);
    }

    startFetching();
  }, []);

  return (
    <ul>
      {jokes.map(({ id, joke }) => (
        <li key={id}>{joke}</li>
      ))}
    </ul>
  );
}
```

If the data you want to fetch is dependent on a prop or state variable, you need to add it to the array of variables that the effect depends on:

```js
import { useEffect, useState } from "react";

function Joke({ id }) {
  const [joke, setJoke] = useState();

  useEffect(() => {
    async function startFetching() {
      const response = await fetch(
        `https://example-apis.vercel.app/api/bad-jokes/${id}`
      );
      const joke = await response.json();

      setJoke(joke);
    }

    startFetching();
  }, [id]);

  if (!joke) {
    return null;
  }

  return <h2>{joke.joke}</h2>;
}
```

The above approach works well enough for simple use cases. It does not cover a few of important features, though:

- It does not handle race conditions. (If the user changes the `id` prop before the first fetch is complete, there is a chance that the wrong joke is displayed.)
- It does not handle loading states.
- It does not handle errors. (Neither network errors nor errors from the API.)
- It does not handle caching.

In the future we will use a data fetching library to address these issues.

> 💡 Even when you use a data fetching library, the library will use effects (and the `useEffect` hook) under the hood to fetch data.

> 📙 Read more about [**Fetching Data** in the React docs](https://react.dev/learn/synchronizing-with-effects#fetching-data). The docs also describe a way to handle race conditions.

---

## Resources

- [React docs: Synchronizing with Effects](https://react.dev/learn/synchronizing-with-effects)
- [React docs: Fetching data example with useEffect](https://react.dev/learn/synchronizing-with-effects#fetching-dat)
- [React docs: You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)

- Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-effects-and-fetch/react-effects-and-fetch.md?plain=1
------------------------------------------------------------------------------------------------------------------------------------------------
# React with Local Storage

## Learning Objectives

- [ ] Understanding the concept of persistent storage in the browser
- [ ] Knowing the difference between `localStorage` and `sessionStorage`
- [ ] Using the methods `setItem()` and `getItem()`
- [ ] Using a library to handle local storage in React apps

---

## The Web Storage API

> 💡 Note that the Web Storage API is not part of React. It is a browser API that is available in all modern browsers.

The Web Storage API provides two methods for storing data on the client:

- `localStorage` stores data with no expiration date
- `sessionStorage` stores data for one session (data is lost when the browser tab is closed)

Data is stored in the browser and per domain, i.e. all data stored by `example.com` can be accessed by `www.example.com` and `subdomain.example.com`, but not by `others.org`.

This makes it possible to store data across page reloads and browser restarts in a secure way.

To store data the API uses key-value pairs. The key is a string and the value can be a string, a number or a boolean.

> 💡 All following examples use `localStorage` but the same applies to `sessionStorage`.

> 📙 Read more about the [**Web Storage API** on the mdn web docs](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API).

### Storing Data

To store data, use the `setItem()` method:

```js
localStorage.setItem("name", "Alex");
localStorage.setItem("age", 28);
localStorage.setItem("isOnline", true);
```

### Retrieving Data

To retrieve data, use the `getItem()` method:

```js
const name = localStorage.getItem("name"); // → "Alex"
const age = localStorage.getItem("age"); // → 28
const isOnline = localStorage.getItem("isOnline"); // → true
```

Calling `getItem` returns `null` if the key does not exist.

```js
const nope = localStorage.getItem("nope"); // → null
```

### Removing Data

To remove data, use the `removeItem()` method:

```js
localStorage.removeItem("name");
```

### Clearing All Data

To remove all data, use the `clear()` method:

```js
localStorage.clear();
```

### Storing Complex Data

The Web Storage API only supports strings, numbers and booleans. To store more complex data, you need to serialize it first. This can be done using the `JSON.stringify()` method:

```js
const user = {
  name: "Alex",
  age: 28,
  isOnline: true,
};

localStorage.setItem("user", JSON.stringify(user));
```

To retrieve the data, you need to parse it using the `JSON.parse()` method:

```js
const user = JSON.parse(localStorage.getItem("user"));
```

### Helper Functions

To make working with the Web Storage API easier, you can create helper functions that encapsulate the serialization and deserialization:

```js
// store data
function setItem(key, value) {
  localStorage.setItem(key, JSON.stringify(value));
}

// retrieve data
function getItem(key) {
  return JSON.parse(localStorage.getItem(key));
}
```

These functions will work with simple data types like strings and numbers as well as complex data types:

```js
setItem("user", {
  name: "Alex",
  age: 28,
  isOnline: true,
});
setItem("count", 42);

const user = getItem("user");
const count = getItem("count");
```

## React with Local Storage

You can also use the Web Storage API in React. Most commonly, you'll want to persist state in local storage so that it survives page reloads.

React has several ways that allow you to synchronize state with local storage. The general concept is to retrieve the initial state from local storage and to store the state in local storage whenever it changes.

Because it becomes quite tricky to correctly wire up all the different pieces yourself, you'll want to use a library that provides a hook for this.

### `use-local-storage-state`

The [`use-local-storage-state`](https://github.com/astoilkov/use-local-storage-state) library provides a hook that allows you to persist state in local storage.

You can use it as a drop-in replacement for the `useState` hook (commented out in the example below):

```js
// import { useState } from "react";
import useLocalStorageState from "use-local-storage-state";

function Counter() {
  // const [count, setCount] = useState(0);
  const [count, setCount] = useLocalStorageState("count", { defaultValue: 0 });

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

> 💡 Notice that the first argument of the `useLocalStorageState` hook is the key that is used to store the state in local storage. If you use the same key for multiple components, they will share the same state.

> 💡 You don't need to handle serialization or parsing of complex data yourself with `use-local-storage-state`. The library takes care of it for you in the background.

> 📙 Read more about [**how to use the `use-local-storage-state` hook** in its docs](https://github.com/astoilkov/use-local-storage-state#usage).

---

## React Custom Hooks

The `useLocalStorageState` hook is not part of React itself. It is a custom hook that is provided by a third-party library. Just like the author of `use-local-storage-state` created a custom hook, you can create your own custom hooks to abstract away common logic that uses other hooks (`useState`, `useEffect`, …).

> 📑 Learn more about [**React Custom Hooks** in the document we prepared](./assets/react-custom-hooks.md) (with examples).

---

## Resources

- [Web Storage API on the mdn web docs](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API)
- [use-local-storage-state on GitHub](https://github.com/astoilkov/use-local-storage-state)
- [📑 React Custom Hooks document](./assets/react-custom-hooks.md)

- Handout:
- https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-with-local-storage/react-with-local-storage.md?plain=1
------------------------------------------------------------------------------------------------------------------------------------------------
# React Custom Hooks

## Learning Objectives

- [ ] Understanding what a custom hook is and how to create one
- [ ] Understanding that custom hooks can abstract stateful logic (`useState`, `useEffect`)
- [ ] Understanding when to create a custom hook

---

## Introduction

React comes with a few basic (but nevertheless _use_-ful) hooks. We learned about `useState` and `useEffect`.

Sometimes you need a hook that is build for a more specific use case. You can create your own custom hooks. They are functions that start with `use` and can use other hooks.

- A state with several specific update functions (e.g. `value`, `increment()`, `decrement()`, `reset()` → `useCount()`)
- A state that is synchronized with window events and values (e.g. `useWindowWidth()`)
- A state that represents a fetched resource (e.g. `useFetch()`)
- A state that is persisted in the browser's local storage (e.g. [`useLocalStorageState()`](https://github.com/astoilkov/use-local-storage-state))

> 📙 Read more about [**Reusing Logic with Custom Hooks** in the React docs](https://react.dev/learn/reusing-logic-with-custom-hooks).

## Counter Example

You could define a custom `useCount` hook like this:

```js
import { useState } from "react";

function useCount(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  function increment() {
    setCount(count + 1);
  }

  function decrement() {
    setCount(count - 1);
  }

  function reset() {
    setCount(initialValue);
  }

  return { count, increment, decrement, reset };
}
```

And use it like this:

```js
import { useCount } from "./useCount";

function Counter() {
  const { count, increment, decrement, reset } = useCount(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

> 💡 Here `useCount` uses the `useState` hook internally. This is why it needs to be a hook itself. Custom hooks need to follow the same rules as normal hooks: Only call hooks at the top level of your function, and only call them from inside a React function component or a custom hook.

## Custom Hook Return Values

Custom hooks can return anything a normal function can return. Here are some examples of common return values:

### Returning a single value

Sometimes hooks only need to return a single value.

```js
function useWindowWidth() {
  const [width, setWidth] = useState();

  useEffect(() => {
    function handleResize() {
      setWidth(window.innerWidth);
    }

    handleResize();

    window.addEventListener("resize", handleResize);
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return width;
}
```

This hook only returns the current window width. It doesn't need to return anything else. The value can be given any name when using the hook.

```js
const currentWindowWidth = useWindowWidth();
```

### Returning an array

```js
function useD6() {
  const [value, setValue] = useState();

  function roll() {
    setValue(Math.floor(Math.random() * 6) + 1);
  }

  return [value, roll];
}
```

This hook returns an array with the current value and a function to roll the dice. Returning an array is a common pattern, since it allows you to use array destructuring to get the values analogous to how `useState` works. Array destructuring has the benefit that you can easily name the values.

```js
const [firstDie, rollFirstDie] = useD6();
const [secondDie, rollSecondDie] = useD6();
```

### Returning an object

```js
function useCount(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  function increment() {
    setCount(count + 1);
  }

  function decrement() {
    setCount(count - 1);
  }

  function reset() {
    setCount(initialValue);
  }

  return { count, increment, decrement, reset };
}
```

> 💡 The return statement makes use of object shorthand notation. This is a nice way to return an object with properties that have the same name as the variable. The above is equivalent to:
>
> ```js
> return {
>   count: count,
>   increment: increment,
>   decrement: decrement,
>   reset: reset,
> };
> ```

When a hook exposes more values and functions, it is common to return an object. This allows you to use object destructuring to get the values. You can also just omit the properties you don't need from the destructuring.

```js
const { count, increment } = useCount(0);
```

## Hook Parameters

Custom hook functions can have parameters like normal functions. This allows you to make the hook more flexible. In the `useCount` example above, the initial value can be passed as a parameter.

```js
function useCount(initialValue = 0) {
  // …
}

const { count, increment, decrement, reset } = useCount(1337);
```

## Hooks and Modules

Custom hooks can be defined in the same file as the component that uses them. But it is also common to define them in a separate file and import them.

```js
// useCount.js
import { useState } from "react";

export function useCount(initialValue = 0) {
  // …
}
```

```js
// Counter.js
import { useCount } from "./useCount";

function Counter() {
  const { count, increment, decrement, reset } = useCount(0);
  // …
}
```

## Abstract recurring logic into custom hooks

### A simple `useFetch` hook

As fetch is a very common use case, it is a good candidate for a custom hook. Here is a simple `useFetch` hook that fetches a resource and returns the parsed response.

```js
import { useState, useEffect } from "react";

export function useFetch(url) {
  const [data, setData] = useState();

  useEffect(() => {
    async function startFetching() {
      const response = await fetch(url);
      const data = await response.json();
      setData(data);
    }
    startFetching();
  }, [url]);

  return data;
}
```

And use it like this:

```js
import { useFetch } from "./useFetch";

function App() {
  const jokes = useFetch("https://example-apis.vercel.app/api/bad-jokes");

  return (
    <div>
      <h1>Bad Jokes</h1>
      <ul>
        {jokes?.map(({ id, joke }) => (
          <li key={id}>{joke}</li>
        ))}
      </ul>
    </div>
  );
}
```

> 💡 Notice that this hook does not implement any advanced features like handling race conditions, error handling, loading states or caching.

### A `usePokemon` hook that uses `useFetch`

If we now want to have a simple to use hook for a very specific use case like fetching a single pokemon from the pokeapi, we can build a `usePokemon` hook that uses the `useFetch` hook internally.

```js
import { useFetch } from "./useFetch";

export function usePokemon(name) {
  const pokemon = useFetch(`https://pokeapi.co/api/v2/pokemon/${name}`);

  return pokemon;
}
```

And use it like this:

```js
import { usePokemon } from "./usePokemon";

function App() {
  const pokemon = usePokemon("pikachu");

  return (
    <div>
      <h1>{pokemon?.name}</h1>
      <img src={pokemon?.sprites.front_default} alt={pokemon?.name} />
    </div>
  );
}
```

Here we are using a custom hook (`useFetch`) inside another custom hook (`usePokemon`). This allows for quite powerful abstractions.

## When should you create a custom hook?

Custom hooks are a powerful tool to abstract recurring logic. But you should only create a custom hook if you are going to reuse the logic in multiple components. If you only need the logic in a single component, it is better to keep it in the component itself.

If you are using something only once: Don't abstract it. If you are using something twice: You might want to abstract it.

---

## Resources

- [Reusing Logic with Custom Hooks in the React docs](https://react.dev/learn/reusing-logic-with-custom-hooks)

- Handout
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-custom-hooks/react-custom-hooks.md?plain=1

------------------------------------------------------------------------------------------------------------------------------------------------
# React Styled Components

## Learning Objectives

- [ ] Understanding what a CSS-in-JS library is and why we prefer it over normal CSS
- [ ] Knowing how to use styled components

  - [ ] create basic styled components
  - [ ] style custom components
  - [ ] adapt styling based on props
  - [ ] use nested styles with pseudo-elements and pseudo-classes
  - [ ] write global styles

- [ ] Knowing how to use fonts from Google with Next.js

---

## What is CSS-in-JS and why do we use it?

CSS-in-JS refers to a collection of ideas to solve complex problems in CSS. There are several libraries which use this approach, one of them is **styled components**. All implementations have in common that they leverage JavaScript as a language for creating styles.

Here's a list of advantages of a CSS-in-JS library like **styled components**:

- automatic critical CSS injected (and nothing more)
- no class name bugs
- easier deletion of CSS
- simple dynamic styling
- painless maintenance
- automatic vendor prefixing

> 📙 Read more about the [motivation to use styled components](https://styled-components.com/docs/basics#motivation).

---

## Styling with styled components

### Basic Styling

To create a styled component,

- import `styled`
- use it to create a styled component like `ListItem`, and
- implement the styled component in the return statement of your component.

```js
//components/List.js
import styled from "styled-components";

export default function List() {
  return (
    <StyledList>
      <ListItem>Item 1</ListItem>
      <ListItem>Item 2</ListItem>
      <ListItem>Item 3</ListItem>
    </StyledList>
  );
}

const ListItem = styled.li`
  background-color: crimson;
`;

const StyledList = styled.ul`
  list-style-type: none;
`;
```

> 💡 Note that the name of a styled component is in uppercase (because it's a component), but must not equal the function name; a common naming pattern is to include the word `Styled`.

> 📙 Read more about [basic styling with styled component](https://styled-components.com/docs/basics#getting-started).

### Styling a Custom Component

Sometimes, there already is a component with predefined styles, but you want to further extend them:

- you might have defined a `Button` component with basic styling yourself [see a good example in the docs](https://styled-components.com/docs/basics#extending-styles) or
- a framework offers a component you want to use, like the `Link` component from `next/link`:

```js
import styled from "styled-components";
import Link from "next/link";

export default function List() {
  return (
    <ul>
      <li>
        <StyledLink>Let's go somewhere!</StyledLink>
      </li>
    </ul>
  );
}

const StyledLink = styled(Link)`
  text-decoration: none;
`;
```

> 📙 Read more about [styling any component](https://styled-components.com/docs/basics#styling-any-component).

### Adapting based on props

You can adapt styling based on props. To do so, you need to pass the props to the styled component. Most of the time you'll want to prefix the prop with a `$`. This tells styled components, that the prop should not be passed to the underlying DOM element or component and should only be used for styling.

```js
import styled from "styled-components";

export default function List() {
  return (
    <StyledList $isOnFire>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </StyledList>
  );
}
```

To use the props to change the styles interpolate a function into the styling template sting. The function receives the props as an argument.

For example, you can use the ternary operator to check whether a property is true or false:

```js
const StyledList = styled.ul`
  list-style-type: ${(props) => (props.$isOnFire ? "🔥" : "❄️")};
  /* or with destructuring: */
  list-style-type: ${({ $isOnFire }) => ($isOnFire ? "🔥" : "❄️")};
`;
```

If you want to set several CSS properties based on the same prop, you can use the `css` helper:

```js
import styled, { css } from "styled-components";

const StyledList = styled.ul`
  ${({ $isOnFire }) =>
    $isOnFire &&
    css`
      list-style-type: "🔥";
      background-color: red;
      color: white;
    `}
`;
```

> 💡 Besides others, the advantages of the `css` helper is syntax highlighting and performance optimization.

> 📙 Read more about [styling based on props](https://styled-components.com/docs/basics#adapting-based-on-props).

### Pseudoelements and Pseudoselectors

To apply pseudoelements, pseudoselectors, or nesting styles, you can use a single ampersand `&` which refers to the component itself:

```js
const StyledLink = styled(Link)`
  text-decoration: none;
  &:hover {
    color: red;
  }
`;
```

> 📙 Read more about [pseudoelements and pseudoselectors](https://styled-components.com/docs/basics#pseudoelements-pseudoselectors-and-nesting).

### Global Styling

To implement global styling, you'll need to create a global styled component. To keep the structure of the project clear, create a `styles.js` file in the root of the project for this:

```js
// styles.js
import { createGlobalStyle } from "styled-components";

export default createGlobalStyle`
  *,
  *::before,
  *::after {
    box-sizing: border-box;
  }
  body {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
      Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  }
	// more global styles here...
`;
```

Import the `GlobalStyle` component into the `pages/_app.js` file and render it above the `<Component />`:

```js
// pages/_app.js
import GlobalStyle from "../styles";

export default function App({ Component, pageProps }) {
  return (
    <>
      <GlobalStyle />
      <Component {...pageProps} />
    </>
  );
}
```

> 💡 There is no consensus as to where to put the `GlobalStyle` component. The decision for a `styles.js` file was made to mirror the fact that, until now, global styles were written in a `styles.css` file.

> 📙 Read more about [createGlobalStyle](https://styled-components.com/docs/api#createglobalstyle).

### Google Fonts GDPR- (DSGVO-) compliant integration

Next.js features the `@next/font` npm package. It will automatically optimize your fonts (including custom fonts) and **remove external network requests for improved privacy and performance** by self-hosting Google fonts.

You need to [install `@next/font` in your project](https://nextjs.org/docs/basic-features/font-optimization#usage) first. To implement a font family, import it where needed and use it inside the styled component.

The following example sets the font-family in the `GlobalStyle` component for the HTML `body` element:

```js
import { createGlobalStyle } from "styled-components";
import { Open_Sans } from "@next/font/google";

const openSans = Open_Sans({ subsets: ["latin"] });

export default createGlobalStyle`
  // ... some globals styles here...
  }
  body {
    margin: 0;
    font-family: ${openSans.style.fontFamily}; 
    padding: 2rem;
  }
	// ... some more global styles here ...
`;
```

> 📙 Read more about [Google Fonts in Next.js](https://nextjs.org/docs/basic-features/font-optimization) and check the [api reference for `@next/font`](https://nextjs.org/docs/api-reference/next/font).

---

## Resources

- [What actually is CSS-in-JS?](https://medium.com/dailyjs/what-is-actually-css-in-js-f2f529a2757)
- [styled components](https://styled-components.com/)
- [Next.js: Font Optimization](https://nextjs.org/docs/basic-features/font-optimization)
- [Google Fonts](https://fonts.google.com/)

- Handout:
- https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-styled-components/react-styled-components.md?plain=1
------------------------------------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------------------------------------------------------------------------------

