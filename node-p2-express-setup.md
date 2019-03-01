# Set Up Express in Node.js

Sourced from Robert Wieruch
https://www.robinwieruch.de/node-js-express-tutorial/

## Step 1: Install and Import Express

`npm install --save express`

index.js:

```javascript
import express from "express";

const app = express();

app.listen(3000, () => console.log("Example app listening on port 3000!"));
```

## Step 2: Routes

index.js:

```javascript
app.get("/", (req, res) => {
  res.send("Hello World!");
});
```

## Step 3: Middleware

### Application Level Middleware: CORS

`npm install --save cors`

```javascript
import "dotenv/config";
import cors from "cors";
import express from "express";

const app = express();

app.use(cors());

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(3000, () => console.log(`Example app listening on port 3000!`));
```

Before production, set up whitelisting for cors
https://github.com/expressjs/cors

## Step 4: Environment Variables

add
`port=3000` to .env

in index.js reference environment for port:

```javascript
app.listen(process.env.PORT, () =>
  console.log(`Example app listening on port ${process.env.PORT}!`)
);
```
