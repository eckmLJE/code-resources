# Set Up Express in Node.js

Sourced from Robert Wieruch
https://www.robinwieruch.de/node-js-express-tutorial/

## Step 1: Install and Import Express

`npm install express`

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
