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

### useEffect
The `useEffect` hook is usually used to `fetch data`, `read from local storage`, and `register/deregister event listeners`. The `useEffect` hook allows us to perform side effects within our component. 

We must first import the hook into our component:

```javascript
import React, { useEffect } from "react"
```

We can then use the `useEffect` hook that will only run on the first render of the component:

```javascript
useEffect(() => {
  // This will only run on the first render
}, [])
```

If we want the `useEffect` hook to run on every render of the component:

```javascript
useEffect(() => {
  // This will run on every render
})
```

For example, we can use the `useEffect` hook to fetch data from an `API`, update the state using the `useState` hook, and re-render the component with the new data.

```javascript
import React, { useState, useEffect } from "react"

function App() {
  const [data, setData] = useState([])

  useEffect(() => {
    const fetchData = async () => {
      const response = await fetch('https://jsonplaceholder.typicode.com/users')
      const jsonData = await response.json()
      setData(jsonData)
    }
    fetchData()
  }, [])

  return (
    <>
      <ul>
        {data.map(user => (
          <li key={user.id}>
            {user.name} ({user.email})
          </li>
        ))}
      </ul>
    </>
  )
}

export default App
```

In this example, we are making an `HTTP request` to the `JSONPlaceholder API` using `fetch`. We then use `useState` to create a state variable called `data` and initialize an empty array. Using the `useEffect` hook, we define a function called `fetchData` that makes an API request using `fetch`, parses the response using `response.json()`, and then updates the `state` using the `setData` function in the `useState` hook. When we call the `fetchData()` function in the `useEffect` hook, we fetch the data when the component first renders. Finally, we map over the `data array` to display the user information in a list.

We can do something similar with images:

```javascript
import React, { useState, useEffect } from "react"

function App() {
  const [dogImage, setDogImage] = useState(null)

  useEffect(() => {
    fetch('https://dog.ceo/api/breeds/image/random/3')
      .then(response => response.json())
      // Set the dogImage to the image URL that we received from the above response
      .then(data => setDogImage(data.message))
  }, [])

  return (
    <>
      {dogImage && dogImage.map((dog) => <img key={dog} width="200px" height="200px" src={dog} alt="Image of a dog." />)}
    </>
  )
}

export default App
```

### useState
The `useState` hook allows us to add `state` to a component. It returns an `array` with two values: the `current state` and a `function` to `update the state`. To use the `useState` hook, we must first import it into our component.

```javascript
import React, { useState } from "react"
```

The hook takes an initial state value and returns an updates atete value whenever the `setter function` is called.

```javascript
const [state, setState] = useState(initialValue)
```

If we don't wish to set an initial value, we can use an empty string:

```javascript
const [state, setState] = useState("")
```

To improve the performance of our application, we can update our hook to only run once instead of each time the component re-renders:

```javascript
const [state, setState] = useState(() => {
  return initialValue
})
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

The state can also be updated by using a `Button` component and an `onClick` event:

```javascript
<button type="button" onClick={() => setState(4)}>Set State to 4</button>
```

This is a simple `Counter` example to `increase` or `decrease` the count based on button clicks:

```javascript
import React, { useState } from "react"

function Component() {
  const [state, setState] = useState(() => {
    return 4
  })

  const increaseCount = () => {
    setState(prevCount => prevCount + 1)
  }

  const decreaseCount = () => {
    setState(prevCount => prevCount - 1)
  }

  return (
    <>
      <button type="button" onClick={decreaseCount}> - </button>
      <span>{state}</span>
      <button type="button" onClick={increaseCount}> + </button>
    </>
  )
}

export default Component
```
