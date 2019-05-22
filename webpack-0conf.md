# webpack

`npm i --save-dev webpack webpack cli`

## package.json

```json
"scripts": {
  "build": "webpack --mode production"
}
```

# babel

`npm i @babel/core babel-loader @babel/preset-env --save-dev`

## .babelrc

```json
{
  "presets": ["@babel/preset-env"]
}
```

## webpack.config.js

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  }
};
```

# webpack dev server

`npm i webpack-dev-server --save-dev`

## package.json

```json
"scripts": {
  "start": "webpack-dev-server --mode development --open",
  "build": "webpack --mode production"
}
```

## webpack.config.js

Add index.html and style.css to `./dist/`

```javascript
var path = require("path");

module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  },
  devServer: {
    contentBase: path.join(__dirname, "dist"),
    compress: true,
    port: 9000
  }
};
```
