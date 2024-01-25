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
