# React JS

- [React JS](#react-js)
  - [Ways to start with React JS](#ways-to-start-with-react-js)
    - [Adding relevant script tags](#adding-relevant-script-tags)
    - [Using `create-react-app`](#using-create-react-app)
      - [Upgrading `create-react-app`](#upgrading-create-react-app)
      - [Deployment with `create-react-app`](#deployment-with-create-react-app)
    - [Using `Vite`](#using-vite)
  - [ReactJS code examples, explanations, and tips](#reactjs-code-examples-explanations-and-tips)
    - [Importing and initial steps of creating a React app](#importing-and-initial-steps-of-creating-a-react-app)
    - [`<React.StrictMode>`](#reactstrictmode)
    - [Creating and Using a Component](#creating-and-using-a-component)
    - [Component with props](#component-with-props)
      - [`children` prop](#children-prop)
      - [Prop Types](#prop-types)
    - [Adding events to a component](#adding-events-to-a-component)
    - [Conditional Rendering](#conditional-rendering)
      - [`if`](#if)
      - [logical and - `&&`](#logical-and---)
      - [logical or - `||`](#logical-or---)
      - [ternary operator - `? :`](#ternary-operator----)
    - [Rendering lists of components and data](#rendering-lists-of-components-and-data)
      - [`map` method](#map-method)
      - [`filter` method](#filter-method)
    - [Exporting and Importing](#exporting-and-importing)
    - [Inline styling of a component](#inline-styling-of-a-component)
    - [Hooks](#hooks)
      - [`useState`](#usestate)
      - [`useReducer`](#usereducer)
      - [`useEffect`](#useeffect)
      - [`useRef`](#useref)
      - [`forwardRef`](#forwardref)
      - [`useImperativeHandle`](#useimperativehandle)
      - [`useMemo`](#usememo)
      - [`useCallback`](#usecallback)
      - [Context API](#context-api)
        - [How to use Context and set value of context in child components](#how-to-use-context-and-set-value-of-context-in-child-components)
    - [Suspense component and lazy](#suspense-component-and-lazy)
      - [Suspense](#suspense)
      - [lazy](#lazy)
      - [Usage](#usage)

<hr>

## Ways to start with React JS

### Adding relevant script tags

One easy way to use React in our projects is to go to the [React link](https://legacy.reactjs.org/docs/cdn-links.html), and from there copy 2 links and paste into the head tags of our html file.

```html
<!-- These are those 2 links at the time of writing this -->
<script
  crossorigin
  src="https://unpkg.com/react@18/umd/react.development.js"
></script>
<script
  crossorigin
  src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"
></script>
```

The link for react-dom that we copied over enables us to access the global variable `ReactDOM` in our js file.

These 2 links are limiting, if we don't use babel. So, let's head to this [link](https://legacy.reactjs.org/docs/add-react-to-a-website.html#quickly-try-jsx) and copy the link for _babel_ and paste into the head tags in our html file.

```html
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

After adding the _babel_ we can use JSX in any `<script>` tag by adding `type="text/babel"` attribute to it.

```html
<script src="index.js" type="text/babel"></script>
```

JSX stands for JavaScript XML.

<hr>

### Using `create-react-app`

To create a react app, we need some tools. One of the tools that could be used is "[create-react-app](https://create-react-app.dev/)". To create a project called `my-app` using `create-react-app`, run this command:

```
npx create-react-app my-app
```

After running this, we get into the "my-app" folder and run `npm start`. Then open http://localhost:3000/ in a browser to see our app. This runs the app in the development mode.

You don’t need to install or configure tools like webpack or Babel. They are pre-configured and hidden so that you can focus on the code.

<hr>

#### Upgrading `create-react-app`

When new versions of Create React App are released, you can upgrade using a single command:

```
npm install react-scripts@latest
```

<hr>

#### Deployment with `create-react-app`

Before deploying your app you need to run this code:

```
npm run build or yarn build
```

This code builds the app for production to the build folder. It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.

Your app is ready to be deployed.

<hr>

### Using `Vite`

We can also create a react app using [Vite](https://vitejs.dev/). If we go to the link and then click "Get Started", we can find different codes to start a project. We use the below code for React:

```
npm create vite@latest my-react-app -- --template react
```

Note: When we use "create-react-app", we can name our files either with "js" or "jsx" extension. In Vite, we must use "jsx".

After the app is created, we need to use the below code in the terminal. This installs the dependencies:

```
npm install
```

Then to run the project, use this command:

```
npm run dev
```

By default, Vite can run the React app on port 5173, but we can change it using the **vite.config.js** file. We just need to add `server: {port: <port_number>}`.

```js
// vite.config.js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
  },
});
```

<hr>

## ReactJS code examples, explanations, and tips

### Importing and initial steps of creating a React app

To use react in our javascript files, we need to import `react` and `react-dom`:

```js
import React from "react";
import ReactDOM from "react-dom/client";
```

Starting from react 18, instead of `ReactDOM.render()`, we use `createRoot()`. `createRoot` lets you create a root to display React components inside a browser DOM node. After using `createRoot()`, we render the component with `render()`:

```js
import ReactDOM from "react-dom/client";

ReactDOM.createRoot(document.getElementById("root")).render(<component>);
```

<hr>

### `<React.StrictMode>`

`<StrictMode>` or `<React.StrictMode>` lets you find common bugs in your components early during development. Use `StrictMode` to enable additional development behaviors and warnings for the component tree inside:

Strict Mode enables the following development-only behaviors:

- Your components will re-render an extra time to find bugs caused by impure rendering.
- Your components will re-run Effects an extra time to find bugs caused by missing Effect cleanup.
- Your components will be checked for usage of deprecated APIs.

**Example**:

```html
<!-- index.html -->
<body>
  <div id="root"></div>
</body>
```

```js
/* index.js */
import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

<hr>

You can also enable Strict Mode for any part of your application:

```js
import { StrictMode } from "react";

function App() {
  return (
    <>
      <Header />

      <StrictMode>
        <main>
          <Sidebar />
          <Content />
        </main>
      </StrictMode>

      <Footer />
    </>
  );
}
```

<hr>

### Creating and Using a Component

This is how we create and use a component.

```js
function Greeting() {
  return <h2>My First Component</h2>;
}

function App() {
  return <Greeting />;
}
```

```js
// arrow function also works
const Greeting = () => {
  return <h2>My First Component</h2>;
};

function App() {
  return <Greeting />;
}
```

<hr>

**Notes**:

- A component must start with capital letter
- A component must return JSX (html)
- When we use the components, we can either use them as a self-closing tag `<Greeting/>` or like this: `<Greeting>...<Greeting/>`

JSX requires tags to be explicitly closed: self-closing tags like `<img>` must become `<img />`.

For historical reasons, `aria-*` and `data-*` attributes are written as in HTML with dashes.

We recommend using a [converter](https://transform.tools/html-to-jsx) to translate your existing HTML and SVG to JSX.

<hr>

### Component with props

This is how to create a component that accepts _props_ and how to use it:

```js
/* We create a component that accepts props */
const Book = (props) => {
  console.log(props);
  return (
    <article className="book">
      <h2>{props.title}</h2>
      <h4>{props.author}</h4>
    </article>
  );
};

/* We use the component and while using we pass the properties to the component */
function BookList() {
  return (
    <section className="booklist">
      <Book title="Chemistry" />
      <Book title="random title" author="some author />
    </section>
  );
}
```

<hr>

Instead of accepting properties into the component as _props_, we can destructure the _props_ inside the component.

```js
const Book = (props) => {
  const { title, author } = props;
  return (
    <article className="book">
      <h2>{title}</h2>
      <h4>{author}</h4>
    </article>
  );
};
```

We can also destructure in function parameters, like this:

```js
const Book = ({ title, author }) => {
  return (
    <article className="book">
      <h2>{title}</h2>
      <h4>{author} </h4>
    </article>
  );
};
```

If you want to give a default value to a prop, you can do it like this:

```js
function Book({ title, author = "Anonymous" }) {
  // ...
}
```

The default value, in the above example, is only used if the author prop is missing or if you pass `author={undefined}`. But if you pass `author={null}` or `author={0}`, the default value will not be used.

<hr>

We can also provide the props to the component using the spread operator.

Let's say we have this component:

```js
// HouseListing.jsx
export default function HouseListing(props) {
  return (
    <div>
      <p>Host: {props.host}</p>
      <p>Experience: {props.experience}</p>
      <p>Location: {props.location}</p>
      <p>Price: {props.price}</p>
    </div>
  );
}
```

We can declare props one by one:

```js
// Scenario 1: declare every prop

import HouseListing from "./components/HouseListing";

const props = {
  host: "Mario",
  experience: "Walk in the woods",
  location: "Norway",
  price: 29,
};

export default function Listings() {
  return (
    <div>
      <HouseListing
        host={props.host}
        experience={props.experience}
        location={props.location}
        price={props.price}
      />
    </div>
  );
}
```

Or, we can use the spread operator:

```js
// Scenario 2: using the spread operator

import HouseListing from "./components/HouseListing";

const props = {
  host: "Mario",
  experience: "Walk in the woods",
  location: "Norway",
  price: 29,
};

export default function Listings() {
  return (
    <div>
      <HouseListing {...props} />
    </div>
  );
}
```

<hr>

#### `children` prop

When we use the components like this `<component> ... </component>`, everything between tags can be accessed through the `children` property. In the below example, we create the _book_ component that expects _title_ and `children` as part of props. Then we render them inside an `article` tag. When we use the _book_ component, we provide a value for the _title_, and everything that we put between the opening and closing _book_ tags become `children` of the _book_ component.

```js
const Book = (props) => {
  const { title, children } = props;
  console.log(props);
  return (
    <article className="book">
      <h2>{title}</h2>
      {children}
    </article>
  );
};

function BookList() {
  return (
    <section className="booklist">
      <Book title="Some Book title">
        <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit.</p>
        <button>click me</button>
      </Book>
    </section>
  );
}
```

#### Prop Types

React will ask to set static types for props. If we want React to stop doing that, and if we use Vite, we can add the below code to the `rules` part of the **.eslintrc.cjs** file:

```js
// .eslintrc.cjs
// ...
rules: {
    // ...
    "react/prop-types": "off",
    // ...
  },
```

But in case, we want to set React Prop Types, here is how we can do it using the `prop-types` library (React recommends using TypeScript instead of checking prop types at runtime).

First, we need to install `prop-types`:

```bash
npm i prop-types
```

Then, we import it in a component, where we declare what type of prop the component expects.

To declare the prop types, we populate the `<ComponentName>.propTypes` object. This object outlines all the props for the component.

Here is a simple example, where we set various props and indicate what type of data they must have:

```js
import PropTypes from "prop-types";

const Component = ({
  strProp,
  numProp,
  boolProp,
  funcProp,
  arrProp,
  objProp,
  symProp,
}) => {
  return (
    <div>
      <p>This is a string property: {strProp}</p>
      <p>This is a number property: {numProp}</p>
      <p>This is a boolean property: {boolProp}</p>
      <p>This is a function property: {funcProp}</p>
      <p>This is an array property: {arrProp}</p>
      <p>This is a object property: {objProp}</p>
      <p>This is a symbol property: {symProp}</p>
    </div>
  );
};

Component.propTypes = {
  strProp: PropTypes.string,
  numProp: PropTypes.number,
  boolProp: PropTypes.bool,
  funcProp: PropTypes.func,
  arrProp: PropTypes.array,
  objProp: PropTypes.object,
  symProp: PropTypes.symbol,
};

export default Component;
```

After the above code, if a parent component supplies a value that is in a different type from the indicated ones, then the app will show an error in the console.

But we won't have an error if the props are not supplied. To indicate that a a prop must be supplied, we can use the `PropTypes.<type>.isRequired`:

```js
import PropTypes from "prop-types";

const Component = ({ strProp, numProp }) => {
  return (
    <div>
      <p>This is a string property: {strProp}</p>
      <p>This is a number property: {numProp}</p>
    </div>
  );
};

Component.propTypes = {
  strProp: PropTypes.string.isRequired,
  numProp: PropTypes.number,
};

export default Component;
```

There are also React-specific things that we can indicate. For example, if we want to know if a prop is renderable, then we can use `PropTypes.node`. An object is not renderable, and if we accidentally pass an object as a prop, then the `PropTypes.node` will show an error:

```js
import PropTypes from "prop-types";

const Component = ({ renderableReactNode }) => {
  return (
    <div>
      <p>This is a renderable property: {renderableReactNode}</p>
    </div>
  );
};

Component.propTypes = {
  renderableReactNode: PropTypes.node,
};

export default Component;
```

If we don't want to specify any type for a prop, but want to make it required, then we can chain `any` and `.isRequired`:

```js
import PropTypes from "prop-types";

const Component = ({ anyProp }) => {
  return (
    <div>
      <p>This is a any property: {anyProp}</p>
    </div>
  );
};

Component.propTypes = {
  anyProp: PropTypes.any.isRequired,
};

export default Component;
```

If we want the prop to receive a React component, we can indicate that we expect to receive `PropTypes.element`:

```js
import PropTypes from "prop-types";

const Component = ({ compProp }) => {
  return (
    <div>
      <p>This is a component property: {compProp}</p>
    </div>
  );
};

Component.propTypes = {
  compProp: PropTypes.element,
};

export default Component;
```

Chaining `PropTypes.element` with `.isRequired` makes sure to indicate that we must receive a single component (not more and not less):

```js
import PropTypes from "prop-types";

const Component = ({ singleCompProp }) => {
  return (
    <div>
      <p>This is a single component property: {singleCompProp}</p>
    </div>
  );
};

Component.propTypes = {
  singleCompProp: PropTypes.element.isRequired,
};

export default Component;
```

If we don't want to indicate a single prop type, and instead want a prop to be one of a few different types, then we can use the `oneOfType()` method. This method accepts an array where we can specify the types that we want the prop to be:

```js
import PropTypes from "prop-types";

const Component = ({ strOrNumProp }) => {
  return (
    <div>
      <p>This is either a string or a number property: {strOrNumProp}</p>
    </div>
  );
};

Component.propTypes = {
  strOrNumProp: PropTypes.oneOfType([PropTypes.string, PropTypes.number]),
};

export default Component;
```

If we want the value of our prop to be one of the specified values, we can use the `oneOf()` method. This method accepts an array where we can specify which values the prop can have:

```js
import PropTypes from "prop-types";

const Component = ({ stateProp }) => {
  return (
    <div>
      <p>This property is either in a loading or a ready state: {stateProp}</p>
    </div>
  );
};

Component.propTypes = {
  stateProp: PropTypes.oneOf(["Loading", "Ready"]),
};

export default Component;
```

We noted that we can specify that a prop must be an array using the `PropTypes.array`. However, if we want the array to consist of specific type of data, we can use the `arrayOf()` method.

```js
import PropTypes from "prop-types";

const Component = ({ arrayProp }) => {
  return (
    <div>
      <p>This property is an array of numbers: {arrayProp}</p>
    </div>
  );
};

Component.propTypes = {
  arrayProp: PropTypes.arrayOf(PropTypes.number),
};

export default Component;
```

In addition to using the `propTypes` property of a component, we can also use the `defaultProps` property to set some default values for our props:

```js

```

We can use the `shape` to specify objects:

<hr>

### Adding events to a component

We can add a click event to a button in a component like this:

```js
const EventExamples = () => {
  const handleButtonClick = () => {
    alert("handle button click");
  };

  return (
    <section>
      <button onClick={handleButtonClick}>click me</button>
    </section>
  );
};
```

We can also pass event handling function to the event immediately:

```js
const EventExamples = () => {
  return (
    <section>
      <button onClick={() => console.log("hello there")}>click me</button>
    </section>
  );
};
```

<hr>

All events propagate in React except `onScroll`, which only works on the JSX tag you attach it to.

If you want to prevent an event from reaching parent components, you need to call `e.stopPropagation()` like this Button component does:

```js
function Button({ onClick, children }) {
  return (
    <button
      onClick={(e) => {
        e.stopPropagation();
        onClick();
      }}
    >
      {children}
    </button>
  );
}

export default function Toolbar() {
  return (
    <div
      className="Toolbar"
      onClick={() => {
        alert("You clicked on the toolbar!");
      }}
    >
      <Button onClick={() => alert("Playing!")}>Play Movie</Button>
      <Button onClick={() => alert("Uploading!")}>Upload Image</Button>
    </div>
  );
}
```

<hr>

### Conditional Rendering

In React, you can conditionally render JSX using JavaScript syntax like `if` statements, `&&,` `||`, and `? :` operators.

#### `if`

```js
function Item({ name, isPacked }) {
  if (isPacked) {
    return <li>{name} ✔</li>;
  }
  return <li>{name}</li>;
}

export default function PackingList() {
  return (
    <section>
      <h1>Sally Ride's Packing List</h1>
      <ul>
        <Item isPacked={true} name="Space suit" />
        <Item isPacked={true} name="Helmet" />
        <Item isPacked={false} name="Photo of Tam" />
      </ul>
    </section>
  );
}
```

#### logical and - `&&`

Remember that the `&&` operator (logical AND) returns the first operand if it is "falsy", or the second operand if the first operand is "truthy".

**Example**:

```js
import { useState } from "react";

const RandomComponent = () => {
  return <h1>hello there</h1>;
};

const Cleanup = () => {
  const [toggle, setToggle] = useState(false);

  return (
    <div>
      <button onClick={() => setToggle(!toggle)}>toggle component</button>
      {toggle && <RandomComponent />}
    </div>
  );
};

export default Cleanup;
```

#### logical or - `||`

The `||` operator (logical OR) returns the first operand if it is "truthy", or the second operand if the first operand is "falsy".

**Example**:

```js
function DisplayName({ name }) {
  return <h3>{name || "Anonymous"}</h3>;
}

export default function Names() {
  return (
    <>
      <DisplayName name="Ziya" />
      <DisplayName />
    </>
  );
}
```

<hr>

#### ternary operator - `? :`

In JavaScript, the ternary operator is a way to concisely express a simple conditional statement. It is often called the "conditional operator" or the "ternary conditional operator".

Here is the basic syntax for using the ternary operator:

```js
condition ? expression1 : expression2;
```

**Example**:

```js
import { useState } from "react";

const User = () => {
  const [user, setUser] = useState(null);

  const handleLogin = () => {
    // normally connect to db or api
    setUser({ name: "Username" });
  };
  const handleLogout = () => {
    setUser(null);
  };

  return (
    <div>
      {user ? (
        <div>
          <h4>hello there, {user.name}</h4>
          <button onClick={handleLogout}>logout</button>
        </div>
      ) : (
        <div>
          <h4>Please Login</h4>
          <button onClick={handleLogin}>login</button>
        </div>
      )}
    </div>
  );
};

export default UserChallenge;
```

<hr>

### Rendering lists of components and data

#### `map` method

You will rely on JavaScript features like `for` loop and the array `map()` method to render lists of components.

```js
const products = [
  { title: "Cabbage", id: 1 },
  { title: "Garlic", id: 2 },
  { title: "Apple", id: 3 },
];

const listItems = products.map((product) => (
  <li key={product.id}>{product.title}</li>
));

return <ul>{listItems}</ul>;
```

Notice how `<li>` has a `key` attribute. For each item in a list, you should pass a string or a number that uniquely identifies that item among its siblings. Usually, a `key` should be coming from your data, such as a database ID. React uses your keys to know what happened if you later insert, delete, or reorder the items.

<hr>

#### `filter` method

Here is an example of using `filter` in ReactJS:

```js
export const people = [
  {
    id: 0,
    name: "Creola Katherine Johnson",
    profession: "mathematician",
  },
  {
    id: 1,
    name: "Mario José Molina-Pasquel Henríquez",
    profession: "chemist",
  },
  {
    id: 2,
    name: "Mohammad Abdus Salam",
    profession: "physicist",
  },
];

export default function PeopleList() {
  const chemists = people.filter((person) => person.profession === "chemist");

  const listItems = chemists.map((person) => (
    <li key={person.id}>
      <p>
        <b>{person.name}:</b>
        {" " + person.profession + "."}
      </p>
    </li>
  ));

  return <ul>{listItems}</ul>;
}
```

<hr>

### Exporting and Importing

How you export your component dictates how you must import it.

- **Default**

```js
export default function Button() {}

import Button from "./Button.js";
```

- **Named**

```js
export function Button() {}

import { Button } from "./Button.js";
```

When you write a default `import`, you can put any name you want after `import`. For example, you could write `import Banana from './Button.js'` instead and it would still provide you with the same `default export`. In contrast, with named imports, the name has to match on both sides. That’s why they are called named imports!

<hr>

### Inline styling of a component

When you need an inline style, you pass an object to the `style` attribute:

```js
export default function TodoList() {
  return (
    <ul
      style={{
        backgroundColor: "black",
        color: "pink",
      }}
    >
      <li>Improve the videophone</li>
      <li>Prepare aeronautics lectures</li>
      <li>Work on the alcohol-fuelled engine</li>
    </ul>
  );
}
```

The next time you see `{{` and `}}` in JSX, know that it’s nothing more than an object inside the JSX curlies!

<hr>

### Hooks

#### `useState`

`useState` hook returns an array with two elements:

- the current state value, and
- a function that we can use to update the state.

While initiating the current state value, it accepts a default value as an argument. State update triggers re-render.

**Example 1**:

```js
import { useState } from "react";

const UseStateBasics = () => {
  const [count, setCount] = useState(0);
  const handleClick = () => {
    setCount(count + 1);
    // be careful, we can set any value
    // setCount('pants');
  };

  return (
    <div>
      <h4>You clicked {count} times</h4>
      <button className="btn" onClick={handleClick}>
        Click me
      </button>
    </div>
  );
};

export default UseStateBasics;
```

<hr>

You may want to update only one property in an object, but keep the previous values for all other properties.

```js
import { useState } from "react";

export default function Form() {
  const [person, setPerson] = useState({
    firstName: "Barbara",
    lastName: "Hepworth",
    email: "bhepworth@sculpture.com",
  });

  function handleFirstNameChange(e) {
    setPerson({
      ...person,
      firstName: e.target.value,
    });
  }

  function handleLastNameChange(e) {
    setPerson({
      ...person,
      lastName: e.target.value,
    });
  }

  function handleEmailChange(e) {
    setPerson({
      ...person,
      email: e.target.value,
    });
  }

  return (
    <>
      <label>
        First name:
        <input value={person.firstName} onChange={handleFirstNameChange} />
      </label>
      <label>
        Last name:
        <input value={person.lastName} onChange={handleLastNameChange} />
      </label>
      <label>
        Email:
        <input value={person.email} onChange={handleEmailChange} />
      </label>
      <p>
        {person.firstName} {person.lastName} ({person.email})
      </p>
    </>
  );
}
```

Note that the `...` spread syntax is “shallow”—it only copies things one level deep. This makes it fast, but it also means that if you want to update a nested property, you’ll have to use it more than once.

```js
import { useState } from "react";

export default function Form() {
  const [person, setPerson] = useState({
    name: "Niki de Saint Phalle",
    artwork: {
      title: "Blue Nana",
      city: "Hamburg",
    },
  });

  function handleNameChange(e) {
    setPerson({
      ...person,
      name: e.target.value,
    });
  }

  function handleTitleChange(e) {
    setPerson({
      ...person,
      artwork: {
        ...person.artwork,
        title: e.target.value,
      },
    });
  }

  function handleCityChange(e) {
    setPerson({
      ...person,
      artwork: {
        ...person.artwork,
        city: e.target.value,
      },
    });
  }

  return (
    <>
      <label>
        Name:
        <input value={person.name} onChange={handleNameChange} />
      </label>
      <label>
        Title:
        <input value={person.artwork.title} onChange={handleTitleChange} />
      </label>
      <label>
        City:
        <input value={person.artwork.city} onChange={handleCityChange} />
      </label>

      <p>
        <i>{person.artwork.title}</i>
        {" by "}
        {person.name}
        <br />
        (located in {person.artwork.city})
      </p>
    </>
  );
}
```

<hr>

Every time you want to update an array, you’ll want to pass a new array to your state setting function. To do that, you can create a new array from the original array in your state by calling its non-mutating methods like `filter()` and `map()`.

```js
import { useState } from "react";

let nextId = 0;

export default function List() {
  const [name, setName] = useState("");
  const [artists, setArtists] = useState([]);

  return (
    <>
      <h1>Inspiring sculptors:</h1>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <button
        onClick={() => {
          setArtists([...artists, { id: nextId++, name: name }]);
        }}
      >
        Add
      </button>
      <ul>
        {artists.map((artist) => (
          <li key={artist.id}>{artist.name}</li>
        ))}
      </ul>
    </>
  );
}
```

The array spread syntax also lets you prepend an item by placing it before the original `...artists`:

```js
setArtists([
  { id: nextId++, name: name },
  ...artists, // Put old items at the end
]);
```

<hr>

The easiest way to remove an item from an array is to filter it out. In other words, you will produce a new array that will not contain that item. To do this, use the `filter` method, for example:

```js
import { useState } from "react";

let initialArtists = [
  { id: 0, name: "Marta Colvin Andrade" },
  { id: 1, name: "Lamidi Olonade Fakeye" },
  { id: 2, name: "Louise Nevelson" },
];

export default function FilterList() {
  const [artists, setArtists] = useState(initialArtists);

  return (
    <>
      <h1>Inspiring sculptors:</h1>
      <ul>
        {artists.map((artist) => (
          <li key={artist.id}>
            {artist.name}{" "}
            <button
              onClick={() => {
                setArtists(artists.filter((a) => a.id !== artist.id));
              }}
            >
              Delete
            </button>
          </li>
        ))}
      </ul>
    </>
  );
}
```

<hr>

It is particularly common to want to replace one or more items in an array. Assignments like `arr[0] = 'bird'` are mutating the original array, so instead you’ll want to use `map` for this as well.

To replace an item, create a new array with `map`. Inside your `map` call, you will receive the item index as the second argument. Use it to decide whether to return the original item (the first argument) or something else:

```js
import { useState } from "react";

let initialCounters = [0, 0, 0];

export default function CounterList() {
  const [counters, setCounters] = useState(initialCounters);

  function handleIncrementClick(index) {
    const nextCounters = counters.map((c, i) => {
      if (i === index) {
        // Increment the clicked counter
        return c + 1;
      } else {
        // The rest haven't changed
        return c;
      }
    });
    setCounters(nextCounters);
  }

  return (
    <ul>
      {counters.map((counter, i) => (
        <li key={i}>
          {counter}
          <button
            onClick={() => {
              handleIncrementClick(i);
            }}
          >
            +1
          </button>
        </li>
      ))}
    </ul>
  );
}
```

<hr>

Sometimes, you may want to insert an item at a particular position that’s neither at the beginning nor at the end. To do this, you can use the `...` array spread syntax together with the `slice()` method. The `slice()` method lets you cut a “slice” of the array. To insert an item, you will create an array that spreads the slice before the insertion point, then the new item, and then the rest of the original array.

In this example, the Insert button always inserts at the index 1:

```js
import { useState } from "react";

let nextId = 3;
const initialArtists = [
  { id: 0, name: "Marta Colvin Andrade" },
  { id: 1, name: "Lamidi Olonade Fakeye" },
  { id: 2, name: "Louise Nevelson" },
];

export default function Replace() {
  const [name, setName] = useState("");
  const [artists, setArtists] = useState(initialArtists);

  function handleClick() {
    const insertAt = 1; // Could be any index
    const nextArtists = [
      // Items before the insertion point:
      ...artists.slice(0, insertAt),
      // New item:
      { id: nextId++, name: name },
      // Items after the insertion point:
      ...artists.slice(insertAt),
    ];
    setArtists(nextArtists);
    setName("");
  }

  return (
    <>
      <h1>Inspiring sculptors:</h1>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <button onClick={handleClick}>Insert</button>
      <ul>
        {artists.map((artist) => (
          <li key={artist.id}>{artist.name}</li>
        ))}
      </ul>
    </>
  );
}
```

<hr>

#### `useReducer`

There is a different way of handling state updates, and that's by using reducers. You can add a reducer to your component using the `useReducer` hook. Import the `useReducer` method from the library like this:

```js
import { useReducer } from "react";
```

The `useReducer` method accepts

- a reducer function as its first parameter and
- the initial state as the second.

It returns a state variable and a dispatch method to make state changes.

You can define the state in the following way:

```js
const [state, dispatch] = useReducer(reducerFunction, initialValue);
```

The reducer function itself accepts two parameters and returns one value. The first parameter is the current `state`, and the second is the `action`.

- The `state` is the data we are manipulating.
- The `action` helps to identify the type of the `action` and change the state accordingly. It is executed by a `dispatch` function.

```js
function reducer(state, action) {}
```

**Example**:

```js
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
    </>
  );
}
```

**Example 2**:

```js
import React, { useReducer } from 'react';

const Counter = () => {
  // set initial state
  const initialState = 0;

  // implement reducer function
  const reducer = (state, action) => {
    switch (action.type) {
      case 'add':
        return state + action.payload;
      case 'subtract':
        return state - action.payload;
      case 'reset':
        return initialState;
      default:
        throw new Error();
    }
  };

  // write useReducer
  const [state, dispatch] = useReducer(reducer, initialState);

  // display state in component and trigger dispatch with buttons
  return (
    <div>
      <h3>Counter</h3>
      <h1>{state}</h1>
      <button onClick={() > dispatch({ type: 'subtract', payload: 1 })}>
        Decrease
      </button>
      <button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
      <button onClick={() => dispatch({ type: 'add', payload: 2 })}>
        Increase
      </button>
    </div>
  );
};

export default Counter;
```

<hr>

#### `useEffect`

The `useEffect` Hook allows you to perform side effects in your components. The word effect refers to a functional programming term called a "side effect".

Most React components are pure functions, meaning they receive an input and produce a predictable output of JSX. Side effects are not predictable because they are actions which are performed with the "outside world."

Common side effects include:

- Making a request to an API for data from a backend server
- To interact with browser APIs (that is, to use document or window directly)
- Using unpredictable timing functions like `setTimeout` or `setInterval`

If we perform a side effect directly in our component body, it gets in the way of our React component's rendering.

Side effects should be separated from the rendering process. If we need to perform a side effect, it should strictly be done after our component renders.

This is what `useEffect` gives us.

The basic syntax of `useEffect` is as follows:

```js
// 1. import useEffect
import { useEffect } from "react";

function MyComponent() {
  // 2. call it above the returned JSX
  // 3. pass two arguments to it: a function and an optional dependencies array
  useEffect(() => {}, []);

  // return ...
}
```

**Example**:

```js
import { useEffect } from "react";

function User({ name }) {
  useEffect(() => {
    document.title = name;
  }, [name]);

  return <h1>{name}</h1>;
}
```

The function passed to `useEffect` is a callback function. This will be called after the component renders.

The second argument is an array, called the **dependencies** array. This array should include all of the values that our side effect relies upon. This array will check and see if a value has changed between renders. If so, it will execute our `useEffect` function again.

**Example**:

```js
import { useState, useEffect } from "react";

function Count() {
  const [count, setCount] = useState(0);
  const [calculation, setCalculation] = useState(0);

  useEffect(() => {
    setCalculation(() => count * 2);
  }, [count]); // <- add the count variable here

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount((c) => c + 1)}>+</button>
      <p>Calculation: {calculation}</p>
    </>
  );
}
```

If you do not provide the dependencies array at all and only provide a function to `useEffect`, it will run after every render.

With an empty dependecies array, `useEffect` runs only on the first render:

```js
useEffect(() => {
  // With an empty dependecies array, runs only on the first render
}, []);
```

If you are updating state within your `useEffect`, make sure to provide an empty dependencies array. If you do provide an empty array, which I recommend you do by default for any time that you use `useEffect`, this will cause the effect function to only run once after the component has rendered the first time.

```js
function MyComponent() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetchData().then((myData) => setData(myData));
    // Correct! Runs once after render with empty array
  }, []);

  return (
    <ul>
      {data.map((item) => (
        <li key={item}>{item}</li>
      ))}
    </ul>
  );
}
```

<hr>

Some effects require cleanup to reduce memory leaks. Timeouts, subscriptions, event listeners, and other effects that are no longer needed should be disposed.

We do this by including a `return` function at the end of the `useEffect` Hook.

```js
function Timer() {
  const [time, setTime] = useState(0);

  useEffect(() => {
    let interval = setInterval(() => setTime(1), 1000);

    return () => {
      // setInterval clears when component unmounts
      clearInterval(interval);
    };
  }, []);
}
```

Components are unmounted when the parent component is no longer rendered or the parent component performs an update that does not render this instance. `ReactDOM.unmountComponentAtNode` will also trigger an unmount.

<hr>

#### `useRef`

`useRef` is a React Hook that lets you reference a value that’s not needed for rendering.

`useRef(<initialValue>)` is a built-in React hook that accepts one argument as the initial value and returns a reference (aka ref). A reference is an object having a special property `current`.

By using a ref, you ensure that:

- You can store information between re-renders (unlike regular variables, which reset on every render).
- Changing it does not trigger a re-render (unlike state variables, which trigger a re-render).
- The information is local to each copy of your component (unlike the variables outside, which are shared)

**Example 1**:

The component LogButtonClicks uses a reference to store the number of clicks on a button:

```js
import { useRef } from "react";

function LogButtonClicks() {
  const countRef = useRef(0);

  const handleClick = () => {
    countRef.current++;
    console.log(`Clicked ${countRef.current} times`);
  };

  console.log("I rendered!");

  return <button onClick={handleClick}>Click me</button>;
}
```

Updating the reference value `countRef.current++` doesn't trigger component re-rendering. This is demonstrated by the fact that 'I rendered!' is logged to the console just once, at initial rendering, and no re-rendering happens when the reference is updated.

**Example 2**:

```js
import { useRef, useState, useEffect } from "react";

function Stopwatch() {
  const timerIdRef = useRef(0);
  const [count, setCount] = useState(0);

  const startHandler = () => {
    if (timerIdRef.current) {
      return;
    }
    timerIdRef.current = setInterval(() => setCount((c) => c + 1), 1000);
  };

  const stopHandler = () => {
    clearInterval(timerIdRef.current);
    timerIdRef.current = 0;
  };

  useEffect(() => {
    return () => clearInterval(timerIdRef.current);
  }, []);

  return (
    <div>
      <div>Timer: {count}s</div>
      <div>
        <button onClick={startHandler}>Start</button>
        <button onClick={stopHandler}>Stop</button>
      </div>
    </div>
  );
}
```

`startHandler()` function, which is invoked when the Start button is clicked, starts the timer and saves the timer id in the reference `timerIdRef.current = setInterval(...)`.

To stop the stopwatch user clicks Stop button. The Stop button handler `stopHandler` accesses the timer id from the reference and stops the timer `clearInterval(timerIdRef.current)`.

Additionally, if the component unmounts while the stopwatch is active, the cleanup function of `useEffect()` is going to stop the timer too.

**Example 3**:

Another useful application of the `useRef()` hook is to access DOM elements directly. This is performed in 3 steps:

- Define the reference to access the element `const elementRef = useRef()`;
- Assign the reference to `ref` attribute of the element: `<div ref={elementRef}></div>`;
- After mounting, `elementRef.current` points to the DOM element.

```js
import { useRef, useEffect } from "react";

function AccessingElement() {
  const elementRef = useRef();

  useEffect(() => {
    const divElement = elementRef.current;
    console.log(divElement); // logs <div>I'm an element</div>
  }, []);

  return <div ref={elementRef}>I'm an element</div>;
}
```

**Example 4**:

You would need to access DOM elements, for example, to focus on the input field when the component mounts.

```js
import { useRef, useEffect } from "react";

function InputFocus() {
  const inputRef = useRef();

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} type="text" />;
}
```

During initial rendering React still determines the output of the component, so there's no DOM structure created yet. That's why `inputRef.current` evaluates to undefined during initial rendering.

`useEffect(callback, [])` hook invokes the callback right after mounting when the input element has already been created in DOM.

callback function of the `useEffect(callback, [])` is the right place to access `inputRef.current` because it is guaranteed that the DOM is constructed.

<hr>

#### `forwardRef`

To access a DOM element rendered in the component's body you can use a ref created by `useRef()` hook. But what if you need to access a DOM element of a child component? Then a simple ref is not enough and you have to combine refs with `React.forwardRef()`: a technique called refs forwarding.

`forwardRef()` is a higher-order component that wraps a React component. The wrapped component works the same way as the original component but also receives as the second parameter a ref: the forwarded reference from the parent component.

```js
import { useRef, useEffect, forwardRef } from "react";

export function Parent() {
  const elementRef = useRef();

  useEffect(() => {
    // Works!
    console.log(elementRef.current); // logs <div>Hello, World!</div>
  }, []);

  return <Child ref={elementRef} />; // assign the ref
}

const Child = forwardRef(function (props, ref) {
  return <div ref={ref}>Hello, World!</div>;
});
```

The parent component assigns `elementRef` to the child component `<Child ref={elementRef} />`. Then, thanks to being wrapped into `forwardRef()`, the child component gets the ref from the second parameter and uses it on its element `<div ref={ref}>`.

After mounting, `elementRef.current`, in the parent component, contains the DOM element from child component.

That's the purpose of `forwardRef()`: give the parent component access to DOM elements in the child component.

You can forward refs more than 1 level down in the component hierarchy. Just wrap each child, grandchild, and so on components in `forwardRef()`, and pass the ref down until you reach the target DOM element.

```js
import { forwardRef, useRef, useEffect } from "react";

export function Parent() {
  const elementRef = useRef();

  useEffect(() => {
    console.log(elementRef.current); // logs <div>Deep!</div>
  }, []);

  return <Child ref={elementRef} />;
}

const Child = forwardRef(function (props, ref) {
  return <GrandChild ref={ref} />;
});

const GrandChild = forwardRef(function (props, ref) {
  return <div ref={ref}>Deep!</div>;
});
```

<hr>

#### `useImperativeHandle`

In essence the only thing this hook does is let you create a completely custom value for the ref you return from a custom component. This means you can do more than just assign a single element to your ref for example.

```js
function CustomInput(props, ref) {
  useImperativeHandle(ref, () => {
    return { alertHi: () => alert("Hi") };
  });

  return <input style={{ backgroundColor: "red" }} {...props} />;
}

export default React.forwardRef(CustomInput);
```

Here we have the most basic use case of `useImperativeHandle` which takes 2 parameters. The first parameter is just the ref you are overriding and the second parameter is a function which returns the new value for your ref. In our case the ref for our `CustomInput` is now an object that contains the single function `alertHi`.

```js
function App() {
  const [value, setValue] = useState("")
  const inputRef = useRef()

  return (
    <>
      <CustomInput
        ref={inputRef}
        value={value}
        onChange={e => setValue(e.target.value)}
      >
      <button onClick={() => inputRef.current.alertHi()}>Alert</button>
    </>
  )
}
```

`useImperativeHandle` takes an optional third parameter which is a dependency array. This works just like `useEffect` in that anytime any of the values in the dependency array change, the function passed to `useImperativeHandle` will be rerun and update the value of your ref. This is useful if you depend on certain values like the `props.value` in our example. If you do not pass this third parameter to `useImperativeHandle`, it will rerun the function you pass to `useImperativeHandle` and update your ref every time the component is rendered.

```js
function CustomInput(props, ref) {
  useImperativeHandle(
    ref,
    () => {
      return { alertValue: () => alert(props.value) };
    },
    [props.value]
  );

  return <input ref={ref} style={{ backgroundColor: "red" }} {...props} />;
}

export default React.forwardRef(CustomInput);
```

<hr>

#### `useMemo`

Memoization is an optimization technique that passes a complex function to be memoized. In memoization, the result is “remembered” when the same parameters are passed-in subsequently.

If we have a function compute 1 + 1, it will return 2. But if it uses memoization, the next time we run 1’s through the function, it won’t add them up; it will just remember the answer is 2 without executing the adding function.

`useMemo` takes in a function and an array of dependencies.

```js
const memoizedValue = React.useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

The dependencies act similar to arguments in a function. The dependency’s list are the elements `useMemo` watches: if there are no changes, the function result will stay the same.

If your dependencies array is not provided, there is no possibility of memoization, and it will compute a new value on every render. You could use the `useRef` hook in that instance. The advantage `useMemo` offers over `useRef` is a re-memoizing if the dependencies change.

**Example**:

```js
import { useState, useMemo } from "react";

export default function Component() {
  const [number, setNumber] = useState(1);
  const [inc, setInc] = useState(0);

  const factorial = useMemo(() => factorialOf(number), [number]);

  const handleChange = (event) => {
    setNumber(Number(event.target.value));
  };
  const handleClick = () => setInc((i) => i + 1);

  return (
    <div>
      Factorial of
      <input type="number" value={number} onChange={handleChange} />
      if {factorial}
      <button onClick={handleClick}>Re-render</button>
    </div>
  );
}

function factorialOf(n) {
  console.log("factorialOf(n) called!");
  return n <= 0 ? 1 : n * factorialOf(n - 1);
}
```

Every time you change the value of the number, 'factorialOf(n) called!' is logged to console. That's expected.

However, if you click Re-render button, 'factorialOf(n) called!' isn't logged to console because `useMemo(() => factorialOf(number), [number])` returns the memoized factorial calculation. Great!

<hr>

#### `useCallback`

Before diving into `useCallback()` use, let's distinguish the problem `useCallback()` solves — the functions equality check.

Functions in JavaScript are regular objects. Let's write a function `factory()` that returns functions that sum numbers:

```js
function factory() {
  return (a, b) => a + b;
}

const sumFunc1 = factory();
const sumFunc2 = factory();

console.log(sumFunc1(1, 2)); // => 3
console.log(sumFunc2(1, 2)); // => 3

console.log(sumFunc1 === sumFunc2); // => false
console.log(sumFunc1 === sumFunc1); // => true
```

The functions `sumFunc1` and `sumFunc2` share the same code source, but they are different function objects. Comparing them (`sumFunc1 === sumFunc2`) evaluates to `false`. That's just how JavaScript objects work. An object (including a function object) equals only to itself.

Different function objects sharing the same code are often created inside React components.

That's when `useCallback(<callbackFunc>, <deps>)` is helpful: given the same dependency values, the hook returns the same function instance between renderings (aka memoization):

```js
import { useCallback } from "react";

function MyComponent() {
  // handleClick is the same function object
  const handleClick = useCallback(() => {
    console.log("Clicked!");
  }, []);

  // ...
}
```

<hr>

#### Context API

React context allows us to share data (state) across our components more easily. You can think of React context as the equivalent of global variables for our React components.

React context helps us avoid the problem of props drilling. _Props drilling_ is a term to describe when you pass props down multiple levels to a nested component, through components that don't need it.

There are four steps to using React context:

- Create context using the `createContext` method.
- Take your created context and wrap the context provider around your component tree.
- Put any value you like on your context provider using the `value` prop.
- Read that `value` within any component by using the context consumer.

**Example**:

In our App, let's pass down our own name using Context and read it in a nested component: User.

```js
// App.js
import React from "react";
import User from "./components/User/User";

export const UserContext = React.createContext();

export default function App() {
  return (
    <UserContext.Provider value="Name">
      <User />
    </UserContext.Provider>
  );
}
```

```js
// User.js
import { UserContext } from "../../App";

function User() {
  return (
    <UserContext.Consumer>{(value) => <h1>{value}</h1>}</UserContext.Consumer>
  );
}

export default User;
```

Instead of using `Consumer`, we can pass the entire context object to a hook called `React.useContext()`.

Here is the example above using the `useContext` hook:

```js
// App.js
import React from "react";
import User from "./components/User/User";

export const UserContext = React.createContext();

export default function App() {
  return (
    <UserContext.Provider value="Name">
      <User />
    </UserContext.Provider>
  );
}
```

```js
// User.js
import { UserContext } from "../../App";

function User() {
  const value = React.useContext(UserContext);

  return <h1>{value}</h1>;
}

export default User;
```

**Example 2**:

We can add a default value to `createContext`. However, the default will work when a parent component doesn't have the `Provider`.

```js
// context.js
import { createContext } from "react";

export const Context = createContext("Default Value");
```

```js
// Providing the Context
import { Context } from "./context";

function Main() {
  const value = "My Context Value";
  return (
    <Context.Provider value={value}>
      <MyComponent />
    </Context.Provider>
  );
}
```

```js
// Consuming the context
import { useContext } from "react";
import { Context } from "./context";

function MyComponent() {
  const value = useContext(Context);

  return <span>{value}</span>;
}
```

The hook returns the value of the context: `value = useContext(Context)`. The hook also makes sure to re-render the component when the context value changes.

**Example 3**:

Context API works even if a component is nested within several components.

```js
// App.js
import { useContext, createContext } from "react";
import { Layout } from "./components";

const UserContext = createContext("Unknown");

function Application() {
  const userName = "John Smith";
  return (
    <UserContext.Provider value={userName}>
      <Layout>
        <h1>Main content</h1>
      </Layout>
    </UserContext.Provider>
  );
}
```

```js
// Layout.js
import Header from "../Header/Header";

export default function Layout({ children }) {
  return (
    <div>
      <Header />
      <main>{children}</main>
    </div>
  );
}
```

```js
// Header.js
import UserInfo from "../UserInfo/UserInfo";

export default function Header() {
  return (
    <header>
      <UserInfo />
    </header>
  );
}
```

```js
// UserInfo.js
import { UserContext } from "../../App";

export default function UserInfo() {
  const userName = useContext(UserContext);
  return <span>{userName}</span>;
}
```

##### How to use Context and set value of context in child components

```js
//Context.js
import React from "react";
export const Context = React.createContext();
```

```js
//App.js
import React, { useState } from "react";
import { Context } from "./Context.js";

import ComponentA from "./ComponentA";
import ComponentB from "./ComponentB";

export default function App() {
  const [context, setContext] = useState("default context value");
  return (
    <Context.Provider value={[context, setContext]}>
      <ComponentA />
      <ComponentB />
    </Context.Provider>
  );
}
```

```js
//ComponentA.js
import React, { useContext } from "react";
import { Context } from "./Context";

export default function ComponentA() {
  const [context, setContext] = useContext(Context);
  return (
    <div>
      ComponentA:
      <button onClick={() => setContext("New Value")}>
        Change Context Value
      </button>
    </div>
  );
}
```

```js
//ComponentB.js
import React, { useContext } from "react";
import { Context } from "./Context";

export default function ComponentB() {
  const [context, setContext] = useContext(Context);
  return <div>ComponentB: {context}</div>;
}
```

<hr>

### Suspense component and lazy

#### Suspense

`Suspense` lets you display a fallback until its children have finished loading. The `Suspense` component receives two props, `children` and `fallback`. It then renders `fallback` until all the data required by `children` is available and `children` can be rendered.

By default, the whole tree inside `Suspense` is treated as a single unit. For example, even if only one of these components suspends waiting for some data, all of them together will be replaced by the loading indicator.

Only Suspense-enabled data sources will activate the `Suspense` component. They include:

- Data fetching with Suspense-enabled frameworks like Relay and Next.js
- Lazy-loading component code with `lazy`
- Reading the value of a Promise with `use` (this is still experimental)

`Suspense` does not detect when data is fetched inside an Effect or event handler.

<hr>

#### lazy

`lazy` lets you defer loading component’s code until it is rendered for the first time. It is also known as on-demand loading because it only loads content visible on users’ screens.

Usually, you import components with the static `import` declaration. To defer loading a component’s code until it’s rendered for the first time, you can use dinamic importing with `lazy` like this:

```js
import { lazy } from "react";

const Component = lazy(() => import("./Component.js"));
```

Using this pattern requires that the lazy component you’re importing was exported as the `default` export.

Now that your component’s code loads on demand, you also need to specify what should be displayed while it is loading. You can do this by wrapping the `lazy` component or any of its parents into a `<Suspense>` boundary.

Do not declare lazy components inside other components. This will cause all state to be reset on re-renders. Instead, always declare them at the top level of your module.

<hr>

#### Usage

```js
import React, { Suspense } from "react";

// Import the `MyComponent` module lazily, so it doesn't get loaded until it is actually needed.
const MyComponent = React.lazy(() => import("./MyComponent"));

function App() {
  return (
    <div>
      <h1>Welcome to my app</h1>

      {/* Use the `Suspense` component with a fallback prop, 
      which will be displayed while the lazy-loaded component is being fetched */}
      <Suspense fallback={<div>Loading...</div>}>
        <MyComponent />
      </Suspense>
    </div>
  );
}

export default App;
```
