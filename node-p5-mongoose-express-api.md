# Creating a REST API with Express.js and MongoDB

https://www.robinwieruch.de/mongodb-express-node-rest-api/

## Change dummy data reference in index.js to use mongo

```javascript
app.use(async (req, res, next) => {
  req.context = {
    models,
    me: await models.User.findByLogin("rwieruch")
  };
  next();
});
```

## Update Routes

### src/routes/session.js

```javascript
import { Router } from "express";

const router = Router();

router.get("/", async (req, res) => {
  const user = await req.context.models.User.findById(req.context.me.id);
  return res.send(user);
});

export default router;
```

### src/routes/user.js

```javascript
import { Router } from "express";

const router = Router();

router.get("/", async (req, res) => {
  const users = await req.context.models.User.find();
  return res.send(users);
});

router.get("/:userId", async (req, res) => {
  const user = await req.context.models.User.findById(req.params.userId);
  return res.send(user);
});

export default router;
```

### src/routes/message.js

```javascript
import { Router } from "express";

const router = Router();

router.get("/", async (req, res) => {
  const messages = await req.context.models.Message.find();
  return res.send(messages);
});

router.get("/:messageId", async (req, res) => {
  const message = await req.context.models.Message.findById(
    req.params.messageId
  );
  return res.send(message);
});

router.post("/", async (req, res) => {
  const message = await req.context.models.Message.create({
    text: req.body.text,
    user: req.context.me.id
  });

  return res.send(message);
});

router.delete("/:messageId", async (req, res) => {
  const message = await req.context.models.Message.findById(
    req.params.messageId
  );

  let result = null;
  if (message) {
    result = await message.remove();
  }

  return res.send(result);
});

export default router;
```
