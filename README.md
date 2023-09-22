# Create a React App

This is a React App created manually without building tools.

Based on this [post](https://dev.to/ivadyhabimana/how-to-create-a-react-app-without-using-create-react-app-a-step-by-step-guide-30nl) from [dev.to](https://dev.to/)

## Steps

1. ### Initialize a Node App

> npm init -y

2. ### Install Babel dependencies

> npm install --save-dev @babel/core babel-loader @babel/cli @babel/preset-env @babel/preset-react

3. ### Install Webpack dependencies

> npm install --save-dev webpack webpack-cli webpack-dev-server

4. ### Install HtmlWebpackPlugin

The HtmlWebpackPlugin is the package that simplifies the creation of HTML files to serve your Webpack bundles. When Webpack bundles all our files, it can generate a single JavaScript (known as a bundle) that will be served along our HTML file.

> npm install --save-dev html-webpack-plugin

5. ### Install React dependencies

> npm install react react-dom

6. ### Add React files

Create a `public` folder and in the created folder create an `index.html` file and add the following code in it:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React App</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

This will be the entry HTML file for our app and our whole React application will live in that `div` with id `root`

Create an `src` folder and create an `App.js` file in it and add the following code:

```jsx
import React from "react";

export default function App() {
  return (
    <div>
      <h1>Hello World: This is a React App</h1>
    </div>
  );
}
```

Back in the root folder create an `index.js` which will be the entry of our app. Add the following code:

```javascript
import React from "react";
import { createRoot } from "react-dom/client";
import App from "./src/App.js";

const container = document.getElementById("root");
const root = createRoot(container);
root.render(<App />);
```

7. ### Configure Babel

In the root folder create a file named `.babelrc` and add the following code

```json
{
  "presets": ["@babel/preset-react"]
}
```

8. ### Configure Webpack

   Create a file named `webpack.config.js` and add the following code

```javascript
const HtmlWebpackPlugin = require("html-webpack-plugin");
const path = require("path");

module.exports = {
  entry: "./src/index.js",
  mode: "development",
  output: {
    path: path.resolve(__dirname, "./dist"),
    filename: "index_bundle.js",
  },
  target: "web",
  devServer: {
    port: "3000",
    static: {
      directory: path.join(__dirname, "public"),
    },
    open: true,
    hot: true,
    liveReload: true,
  },
  resolve: {
    extensions: [".js", ".jsx", ".json"],
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: "babel-loader",
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, "public", "index.html"),
    }),
  ],
};
```

9. ### Add scripts in package.json

```json
"scripts": {
    "start": "webpack-dev-server .",
    "build": "webpack ."
  }
```

10. ### Start your application

> run `npm start` to start the application

---

## Optional step

### Avoid import React in every JSX file

Add this config in the `.babelrc` file:

```json
{
  "presets": [
    [
      "@babel/preset-react",
      {
        "runtime": "automatic"
      }
    ]
  ]
}
```
