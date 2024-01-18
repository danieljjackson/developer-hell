# Next
The `Next` documentation can be found here: `https://nextjs.org/docs`

The documentation below relate to `Next` version `14.0.4`.

## Installation
`Next` requires `macOS`, `Windows` or `Linux` operating systems and `Node.js` version `18.17` or later to be installed.

It is recommended to install `Next` using the `create-next-app`, which sets up everything automatically. Follow the prompts in the terminal to configure the application.

```shell
$ npx create-next-app@latest
```

This will install the following dependencies:

+ `react`
+ `react-dom`
+ `next`

`Next` ships with `TypeScript`, `ESLint` and `TailwindCSS` configured by default.

Once installed, change directory to the folder created by the installation process and start the development server using:

```shall
$ npm run dev
```

The `Next` application will be available to view on `localhost` within a browser window/tab at: `http://localhost:3000/`.

There are a number of scripts we can run when using `Next`:

+ `dev`: runs `next dev` to start `Next` in development mode.
+ `build`: runs `next build` to build the application for production use.
+ `start`: runs `next start` to start a `Next` production server.
+ `lint`: runs `next lint` to set up the `Next` built-in ESLint configuration.

## Directories
With new applications, it is recommended to use the `App Router`. This allows us to use React's latest features and is an evolution of the `Page Router`.

Create an `app/` folder, then add a `layout.js` (or `layout.tsx` if using TypeScript), and `page.js` (or `page.tsx` if using TypeScript) files to this folder. These will be rendered when the user visits the root of the application (`/`).

If we forget to create the `layout.js` (or `layout.tsx`) file, `Next` wil automatically generate the file when we run the development server using `next dev` (`npm run dev`).

The file structure should look something like this - if we're using the `src` directory:

```
src /
  app /
    layout.js
    page.js
```

If the application has been installed using the `create-next-app` tool and we have selected to have a `src` directory, then this will generate an `app` folder with the following files by default:

```
src /
  app /
    favicon.ico
    globals.css
    layout.js
    page.js
    page.module.css
```

### Layout
The code within the root layout `layout.js` file within the `src/app/` folder, can be simplified to this to begin our application:

```javascript
export default function RootLayer({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
```

This is the `Root layout` and is always required. It is usually found within the `app/` or `src/app/` directory and applies to all routes. This layout enables us to modify the initial HTML returned from the server. The root layout itself must always define the `<html>` and `<body>` tags.

Only the `Root layout` can contain `<html>` and `<body>` tags.

The `Root layout` can also use the `built-in SEO support` to manage `<head>` HTML elements, such as the `<title>` tag.

The following is already added to each route by default:

```html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
```

### Homepage
We can create a homepage using the `page.js` file within the `src/app/` folder. This will be rendered when we navigate to the root of the application (`/`).

```javascript
export default function Home() {
  return <h1>Hello, World</h1>
}
```

## Routing & Pages
A `page` is UI that is unique to a route and is always the `leaf` of the `route subtree`. The first page, often the `homepage`, is created by adding a `page.js` file inside the `app/` or `src/app` directory. This can then be viewed on the route (`/`).

If we want to create a further page, such as the `About` page, we can create a page in a directory of `app/about/` or `src/app/about/` and add the `page.js` file here. This will create the UI for the `/about` URL.

```javascript
// src/app/about/page.js

export default function About() {
  return <h1>About</h1>
}
```

On `localhost`, this page can be viewed here: `http://localhost:3000/about`.

### Nested Layouts
Once a route/page has been created, layouts defined inside a folder - for example, `app/about/layout.js` or `src/app/about/layout.js` - will apply to the specific route/page and render when those segments are active. These files are `nested`, meaning they wrap child layouts via their `children` prop.

Here's the updated file structure:

```
src /
  app /
    layout.js
    page.js
    about /
      layout.js
      page.js
```

The `nested layout` of `src/app/about/layout.js` or `src/app/about/layout.tsx` (if using `TypeScript`), will look like this:

```javascript
export default function AboutLayout({ children }) {
  return <section>{children}</section>
}
```

When viewing the `About` page - `src/app/about/page.js`, the content of the page will be wrapped with a `<section>` tag, but on the `Homepage` - `src/app/page.js`, this is not applied. Both pages will share the layout found in the `Root layout` file - `src/app/layout.js`.

+ `Homepage`: `http://localhost:3000/`
+ `About`: `http://localhost:3000/about`

### Links
There are three ways to navigate between routes in `Next`:

+ Using the `<Link>` component
+ Using the `useRouter` Hook
+ Using the native `History API`

#### `<Link>` Component
The `<Link>` component is built-into Next and extends the HTML `<a>` tag to provide prefetching and client-side navigation between routes. It is the primary and recommended way to navigate between routes in `Next`.

This component is imported from `next/link` and we use the `href` prop to the component.

```javascript
import Link from 'next/link'

export default function Home() {
  return <Link href="/about">About</Link>
}
```

## Updating & Modifying the `<head>`
To update the `<head>` section of a page(s)/route, we can use the `built-in SEO support`. Metadata can be defined by exporting a `metadata object` or `generateMetadata function` in a `layout.js` or `page.js` file.

In this example, we add a `<title>` tag to every page by default when using the `metadata object` in the `Root layout` file - `src/app/layout.js`.

```javascript
export const metadata = {
  title: `Test App`
}

export default function RootLayer({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
```

This will render `<title>Test App</title>` for every page/route in our application. It is better to use the `Metadata API` to automatically handle this.

## Components
`Server components` and `Client components` were introduced from `Next` version `13`. By default, `Next` uses `Server components` allowing server rendering to be implemented without any additional configuration.

+ A `Server component` is a component that is fetched and rendered **ON THE SERVER**
+ A `Client component` is a component that is fetched and rendered **ON THE CLIENT (BROWSER)**

It may always be best to add reusable React components into a directory within the `src` folder to make them easier to find - such as `src/app/components/`

To use a `Client component`, use the `"use client"` directive at the top of the file, above any imports. A `Button` component would be an example of a `Client component`.

As an example, here's adding a `Button` component which is within a file of `src/app/components/button/index.jsx`:

```
src /
  app /
    layout.js
    page.js
    about /
      layout.js
      page.js
    components /
      button /
        index.jsx
```

A simple `Button` component code may look like this, here using the `'use client'` directive to set this to be a `Client component`:

```javascript
// app/src/components/button/index.jsx

'use client'

const Button = ({ children }) => {
  return (
    <button>{children}</button>
  )
}

export default Button
```

We can then import this component into our pages/routes. Here's the `Button` component being imported into the `About` page/route. Notice how we use the `fragement` of `<>` and `</>` to allow multiple elements/components to be rendered.

```javascript
// app/src/about/page.js

import Link from 'next/link'

import Button from '../components/button'

export default function About() {
  return (
    <>
      <Link href="/">Home</Link>
      <Button>Example Button</Button>
    </>
  )
}
```
