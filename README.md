### feathers
---
https://github.com/feathersjs/feathers

```
npm install @feathersjs/feathers @feathersjs/socketio @feathersjs/express feathers-memory
node app

npm install -g @feathersjs/cli
mkdir my-new-app
cd my-new-app/
feathers generate app
npm start
```

```
const feathers = require('@feathersjs/feathers');
const express = require('@featherjs/express');
const socketio = require('@feathersjs/socketio');
const memory = require('feathers-memory');
const app = express(feathers());
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.configure(express.rest());
app.configure(socketio());
app.use('/messages', memory(
  paginate: {
    default: 10,
    max: 25
  }
));
app.use(express.errorHandler());
app.on('connection', connection => app.channel('everybody').join(connection));
app.publish(data => app.channel('everybody'));
app.listen(3030).on('listening', () => {
  console.log('Feathers server listening on localhost:3030')
});
```

```
```

