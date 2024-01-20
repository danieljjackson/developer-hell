# Next
The `Next` documentation can be found here: `https://nextjs.org/docs`

The documentation below relate to `Next` version `14.0.4`.

## Browser Support

+ `Chrome` 64 or later
+ `Edge` 79 or later
+ `Firefox` 67 or later
+ `Opera` 51 or later
+ `Safari` 12 or later

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

### Dynamic Routing & Routes
Dynamic routing allows a single page to be used to dynamically render data and content based on the route provided. As an example, we created a `product` page with a `dynamic route` of `productId` to show details about each product based on the `ID` passed into the URL/route. The dynamic route is created by generating a folder named with the `dynamic route` in square brackets, as with `[productId]`. This is called the `dynamic seqment` that is used to create dynamic routes. 

The file structure in our application looks like this:

```
public /
src /
  app /
    layout.js
    page.js
    about /
    components /
    products /
      page.js
      [productId] /
        page.js
```

Our `product` page - `src/app/products/page.js` - looks like this:

```javascript
export default function Products() {
  return (
    <>
      <h1>Products List</h1>

      <h2>Product 1</h2>
      <h2>Product 2</h2>
      <h2>Product 3</h2>
    </>
  )
}
```

The `products` page can be viewed here: `http://localhost:3000/products`

Our dynamic route - `src/app/products/[productId]/page.js` - looks like this:

```javascript
export default function ProductDetails({ params }) {
  return <h1>Details about the product {params.productId}</h1>
}
```

The `product details` dynamic page/route can be viewed here with different `ID` values being passed into the URL. For example: `http://localhost:3000/products/1`, `http://localhost:3000/products/2`, or `http://localhost:3000/products/250`.

Every page in the `app router` receives `route parameters` as a `prop`. This can be destructured as `params` in the function. The `params object` contains the `route parameters` as `value pairs`. So we can use the `params.productId` value to get the ID from the URL.

### Custom 404 Page
To create a `404 (not found) page` in our application, we need to add a `not-found.js`, or `not-found.tsx` if using TypeScript, page within the `src/app/` directory. To simplify, our code could look like this:

```javascript
export default function NotFound() {
  return <h1>Page Not Found</h1>
}
```

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

We can also include the `meta description` here:

```javascript
export const metadata = {
  title: `Test App`,
  description: `Generated by Next`
}
```

This will render `<title>Test App</title>` and a `meta description` for every page/route in our application. It is better to use the `Metadata API` to automatically handle this.

## Components
`Server components` and `Client components` were introduced from `Next` version `13`. By default, `Next` uses `Server components` allowing server rendering to be implemented without any additional configuration.

+ A `Server component` is a component that is fetched and rendered **ON THE SERVER**
+ A `Client component` is a component that is fetched and rendered **ON THE CLIENT (BROWSER)**

When a user requests a web page from a server, the server responds and sends data to the browser. The browser then downloads the JavaScript and builds the web page. The browser has to install all the necessary JavaScript, including any `npm` packages, to build the web page. This can increase the loading time and impact the experience for the user. A server component is built on the server and returns HTML, removing the need to download JavaScript files, as with client components. This reduces the rendering time and improves the user experience.

An example of components:

+ `Navbar` - this would be a `Server component`
+ `Sidebar` - this would be a `Server component`
+ `Main` - this would be a `Server component`
+ `Search` - this would be a `Client component`
+ `Button` - this would be a `Client component`

`Server components` are used for:

+ To `Fetch data`
+ Access `backend resources` directly
+ Keep sensitive data on the server, such as `access tokens` and `API keys`
+ Reduce `client-side JavaScript`

Here are some of the benefits of using `Server components`:

+ `Data Fetching`: using `Server components` allows us to move data fetching to the server, closer to the data source. This helps to improve performance and reducing the time it takes to fetch any data needed for rendering. This helps to reduce the number of requests the client needs to make.
+ `Security`: allows sensitive data and logic to remain on the server, such as `tokens` and `API keys`, without exposing them to the client.
+ `Caching`: By rendering on the server, the result can be cached and reused on subsequent requests across users. This improves performance and reduces the amount of rendering and data fetching done on each request.
+ `Bundle size`: allows large dependencies on the server to reduce the impact on the client when using JavaScript bundles. This reduces the size of the bundle required to be downloaded by the client (browser), which is then required to download, parse and execute.
+ `Initial Page Load`: we can generate HTML to allow users to view the page immediately without waiting for the client to download, parse and execute the JavaScript needed to render the page. This also improves `First Contentful Paint (FCP)`.
+ `Search Engine Optimisation (SEO)`: rendered HTML can be used by search engine bots to index our pages. This also benefits social media to generate previews of pages.
+ `Streaming`: we can split the rendering of `Server components` into chunks and stream them to the client as they become available. This allows the user to see parts of the page earlier without having to wait for the entire page to be rendered on the server.

`Next` recommends using `Server components` until we need to use `Client components`. React hooks, such as `useState()`, `useEffect()`, and `useContext()`, are only available when using `Client components`. Furthermore, if we need to access browser-related features such as `onClick`, `window`, or `browserAPI`, these also need to be `Client components`.

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

## Static Assets
`Next` can serve static assets like `images`, under a folder called `public` in the root directory. Files in this `public` directory, can be referenced from within the code starting from the base URL (`/`).

This folder is also useful for adding additional assets and files such as `robots.txt`, `favicon.ico`, static files such as `.html` and `Google Site Verification`.

```
public /
  image.svg
  robots.txt
src /
  app /
    layout.js
    page.js
    about /
    components /
```

Only assets that are in the `public` folder at `build time` will be served by `Next`.

## Images
The `Next` `Image` component extends the HTML `<img>` element with features for automatic image optimisation. The component first needs to be imported:

```javascript
import Image from 'next/image'
```

### Local Images
To use local images, we import the image as a `.jpg`, `.png`, `.svg`, or `.webp` image file. `Next` will automatically determine the `width` and `height` of the image based on the file being imported. These values are used to prevent `Cumulative Layout Shift (CLS)` while the image is being loaded. The import is static so the image can be analyzed at build time.

The local images are to be found in the `public/` folder.

```javascript
// app/src/about/page.js

import Image from 'next/image'

import profilePicture from '../public/author.png'

export default function About() {
  return (
    <>
      <Image
        src={profilePicture}
        alt="Portrait of the author."
      />
    </>
  )
}
```

### Remote Images
To use remote images, the `src` property should be a URL string. `Next` does not have access to remote files during the build process, so a remote image will need the `width` and `height` props to be added manually. The `width` and `height` attributes are used to infer the correct aspect ratio of the image and to avoid layout shift from the image loading in.

```javascript
// app/src/about/page.js

import Image from 'next/image'

export default function About() {
  return (
    <>
      <Image
        src="https://s3.amazonaws.com/my-bucket/profile.png"
        alt="Portrait of the author."
        width={500}
        height={500}
      />
    </>
  )
}
```

To allow images to be optimised, we need to define a list of supported URLs in the `next.config.js` file. The following configuration will only allow images from a specified Amazon S3 bucket.

```javascript
// next.config.js

/** @type {import('next').NextConfig} */
const nextConfig = {}

module.exports = {
  images: {
    remotePatterns: [
      {
        protocol: `https`,
        hostname: `s3.amazonaws.com`,
        port: ``,
        pathname: `/my-bucket/**`,
      },
    ],
  },
}
```

## Fetching Data
Within our application, we usually want to fetch data from an `API endpoint` and/or a `database`. `Next` extends the native `Fetch API` to allow us to configure the caching and revalidating behavior for each fetch request on the server.

## Connect to a CMS (Content Management System)

### Connect to Storyblok
Once our `Next` application is setup, we need to install `Storyblok's React SDK` package to allow our `Next` application to interact with `Storyblok`. This package will be installed as a `dependency` and listed in the `package.json` file.

```shell
npm install @storyblok/react
```
