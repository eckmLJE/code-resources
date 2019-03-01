# SETUP MONGODB WITH MONGOOSE IN EXPRESS

https://www.robinwieruch.de/mongodb-express-setup-tutorial/

MongoDB Windows Installation Guide:
https://www.robinwieruch.de/mongodb-windows-setup/

## Installation

npm install --save mongoose

## Create Schemas & Model

### src/models/user.js

```javascript
import mongoose from "mongoose";

const userSchema = new mongoose.Schema({
  username: {
    type: String,
    unique: true
  }
});

userSchema.statics.findByLogin = async function(login) {
  let user = await this.findOne({
    username: login
  });

  if (!user) {
    user = await this.findOne({ email: login });
  }

  return user;
};

userSchema.pre("remove", function(next) {
  this.model("Message").deleteMany({ user: this._id }, next);
});

const User = mongoose.model("User", userSchema);

export default User;
```

### src/models/message.js

```javascript
import mongoose from "mongoose";

const messageSchema = new mongoose.Schema({
  text: {
    type: String,
    required: true
  },
  user: { type: mongoose.Schema.Types.ObjectId, ref: "User" }
});

const Message = mongoose.model("Message", messageSchema);

export default Message;
```

### src/models/index.js

```javascript
import mongoose from "mongoose";

import User from "./user";
import Message from "./message";

const connectDb = () => {
  return mongoose.connect(process.env.DATABASE_URL);
};

const models = { User, Message };

export { connectDb };

export default models;
```

### Add database url to .env config file

```
DATABASE_URL=mongodb://localhost:27017/node-express-mongodb-server
```

## Hook up to express application

```javascript

import models, { connectDb } from './models';

const eraseDatabaseOnSync = true;

connectDb().then(async () => {
  if (eraseDatabaseOnSync) {
    await Promise.all([
      models.User.deleteMany({}),
      models.Message.deleteMany({}),
    ]);

    createUsersWithMessages();
  }

  app.listen(process.env.PORT, () =>
    console.log(`Example app listening on port ${process.env.PORT}!`),
  );
});

const createUsersWithMessages = async () => {
  ...
};
```

### Create seed data with createusersWithMessages()

```javascript
const createUsersWithMessages = async () => {
  const user1 = new models.User({
    username: "rwieruch"
  });

  const user2 = new models.User({
    username: "ddavids"
  });

  const message1 = new models.Message({
    text: "Published the Road to learn React",
    user: user1.id
  });

  const message2 = new models.Message({
    text: "Happy to release ...",
    user: user2.id
  });

  const message3 = new models.Message({
    text: "Published a complete ...",
    user: user2.id
  });

  await message1.save();
  await message2.save();
  await message3.save();

  await user1.save();
  await user2.save();
};
```
