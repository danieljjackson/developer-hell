# Next

The `Next` documentation can be found here: `https://nextjs.org/docs`

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

### Homepage
We can create a homepage using the `page.js` file within the `src/app/` folder. This will be rendered when we navigate to the root of the application (`/`).

```javascript
export default function Home() {
  return <h1>Hello, World</h1>
}
```
