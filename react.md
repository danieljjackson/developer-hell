# React

## Install
To install and setup a `React` project, we can use the `Vite` build tool. This will install `create-vite@5.1.0` or the latest version of `Vite` at the time.

```shell
$ npm create vite
```

We can then use `Vite` to scaffold the application using the prompts in the terminal. Select `React` when the choice of framework selection is available. Once complete, change directory into the project folder created and install the `npm` packages required. 

```shell
$ npm install
```

Run the `development` server once the installation has been completed. The application will run on the default `port` on `localhost` of: `http://localhost:5173/`

```shell
$ npm run dev
```

The initial file structure will look like this:

```
node_modules /
public /
src /
  assets /
  App.css
  App.jsx
  index.css
  main.jsx
```

## Setup
Once the setup has been completed, we can remove any boilerplate code to start building the `React` application. First, remove the `App.css` and `index.css` CSS stylesheets and update the `main.jsx` file:

```javascript
import React from `react`
import ReactDOM from `react-dom/client`
import App from `./App.jsx`

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

Then, in the `App.jsx` file, remove all additional boilerplate code to leave this:

```javascript
function App() {
  return (
    <h1>Hello World</h1>
  )
}

export default App
```

## Components
It is often best to add any reusable `components` into a folder/directory within the `src/` folder. For example, if we were to create a `Heading` component to replace our `<h1>` element, we can create a folder within our file structure and add a file named `index.jsx`.

```
node_modules /
public /
src /
  assets /
  components /
    heading /
      index.jsx
```

Our `Heading` component will be created within the `index.jsx` file with the following code:

```javascript
// src/components/heading/index.jsx

function Heading() {
  return <h1>Heading</h1>
}

export default Heading
```

We can then import this into the `App.jsx` file to render our `Heading` component:

```javascript
import Heading from "./components/heading"

function App() {
  return (
    <Heading />
  )
}

export default App
```

### Props
We can use `props`, also known as `properties`, within our components to pass data into the component to render. In the `Heading` component, we can use the `children` prop to change the content of the heading to display something different each time the component is used.


```javascript
// src/components/heading/index.jsx

function Heading({ children }) {
  return <h1>{children}</h1>
}

export default Heading
```

We can pass data into the `prop` within our component like so to render the heading of `"This is a Heading"` onto the page:

```javascript
import Heading from "./components/heading"

function App() {
  return (
    <Heading>This is a Heading</Heading>
  )
}

export default App
```

In this example of a `Heading` component, we can change the element being rendered using a `prop` named `level` to set the type of Heading being rendered, from `<h1>` through to `<h6>`.

```javascript
// src/components/heading/index.jsx

function Heading({ level, children }) {
  const Tag = `h${level}`

  return <Tag>{children}</Tag>
}

export default Heading
```

For example, if we want to set the `Heading` to render as a `<h2>`, we can pass the value of `2` into the `level` prop.

```javascript
import Heading from "./components/heading"

function App() {
  return (
    <Heading level={2}>This is a Heading</Heading>
  )
}

export default App
```

### Default Prop Values
We can set default values for our `props` within a component. These default values will be used when the component renders unless a value is passed into the component. For example, we can set the `level` of the `Heading` to be `1` so that a heading will always render as a `<h1>` unless we pass a value into the component to overwrite this.

```javascript
// src/components/heading/index.jsx

function Heading({ level = 1, children }) {
  const Tag = `h${level}`

  return <Tag>{children}</Tag>
}

export default Heading
```

So if we pass no value into the `level` prop when using the `Heading` component, it will render, by default, as a `<h1>` heading.

```javascript
import Heading from "./components/heading"

function App() {
  return (
    <Heading>This is a h1 Heading</Heading>
  )
}

export default App
```

## Hooks

### useState
The `useState` hook allows us to add `state` to a component. It returns an `array` with two values: the `current state` and a `function` to `update the state`. To use the `useState` hook, we must first import it into our component.

```javascript
import React, { useState } from "react"
```

The hook takes an initial state value and returns an updates atete value whenever the `setter function` is called.

```javascript
const [state, setState] = useState(initialValue)
```

Here, the `initialValue` is the value we want to start with and `state` is the current state value that can be used in our component. The `setState` function is used to update the `state` which will trigger a re-render of the component. The value rendered on the page will be the `initialValue` of `1`.

Our example component would look something like this:

```javascript
import React, { useState } from "react"

function Component() {
  const [state, setState] = useState(1)

  return (
    <div>{state}</div>
  )
}

export default Component
```

#### Update ths state
We can use the `useState` function, or whatever it's been named, to take a new value and update the `state` variable. Here's an example that uses a text box to update the `state` variable on every change. This will cause the component to re-render.

```javascript
import React, { useState } from "react"

function Component() {
  const [state, setState] = useState(1)

  return (
    <>
      <input type="text" value={state} onChange={e => setState(e.target.value)} />
      <div>{state}</div>
    </>
  )
}

export default Component
```
