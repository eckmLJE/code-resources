# Node.js + Babel Basic Setup

Sourced from Robert Wieruch
https://www.robinwieruch.de/minimal-node-js-babel-setup/

## Step 1: Create Direcotry and initialize npm

`npm init -y`
Initialize node project w/ defaults

```bash
npm config list

npm set init.author.name "<Your Name>"
npm set init.author.email "you@example.com"
npm set init.author.url "example.com"
npm set init.license "MIT"
```

## Step 2: Create entry point index.js

```bash
mkdir src
cd src
touch index.js
```

## Step 3: Install nodemon and add to npm start

nodemon will re-start server on code save, but it will not refresh browser.

Will need webpack dev server to achieve this

`npm install nodemon --save-dev`

Update package.json start script w/ nodemon

```json
{
  ...
  "main": "index.js",
  "scripts": {
    "start": "nodemon src/index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  ...
}
```

## Step 4: Install Babel

`npm install @babel/core @babel/node --save-dev`

```json
{
  ...
  "main": "index.js",
  "scripts": {
    "start": "nodemon --exec babel-node src/index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  ...
}
```

Add most recent babel presets

`npm install @babel/preset-env --save-dev`

Add .babelrc config file

`touch .babelrc`

In .babelrc:

```json
{
  "presets": ["@babel/preset-env"]
}
```

## Step 5: Set up environment variables

First set up environment file

`touch .env`

`MY_SECRET=mysupersecretpassword`

Install dotenv library for important environment variables

`npm install dotenv --save`

import at top of index.js

```javascript
import "dotenv/config";
```

Test by referencing secret variable in .env file and running npm start

```javascript
console.log("Hello Node.js project.");

console.log(process.env.MY_SECRET);
```


