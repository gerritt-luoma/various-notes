# Node Notes
## Basics
- Node is a server runtime for javascript.  It provides the ability to run JavaScript programs on your computer instead of just in the browser/embedded in html
- In order to run a javascript simply run `node <filename>`
- Node runs as an event loop which is best described [here](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)

### Accessing the Process Object
- While node is running it will have a global `process` object that has useful methods and information on the current process
- One of the more used process attributes is `process.env`.  This stores information about the current working environment the process is running in
  - Example: `process.env` has a `PWD` property that stores the current working directory of the process
- A common environment variable stored in `process.env` is `NODE_ENV` which denotes whether the application should be running with a `production` or `development` environment
- Another attribute is `process.memoryUsage()` which returns the CPU demands of the process
- You can also access the arguments passed when starting the program.  You can access these with `process.argv` which is an array of the arguments passed

### Core and Local Modules
- `Modularity` is a software design principle where a program is broken into distinct parts (`modules`) providing single pieces of overall functionality.  These `modules` are used together to create the full program
- Modularity is necessary for creating scalable programs because it breaks the program into manageable chunks
- Node has many modules built in to reduce overhead on developers when starting out
- Unlike ES6, you **must** use the `require` method to import modules into a file
- For built in or installed modules, you assign a variable to the output of `require(<name of module>)`
- For your own custom modules you assign a variable to the output of `require(<filepath to module>)`

### Node Package Manager
- The **N**ode **P**ackage **M**anager allows you to download and install third party modules to use in your projects
- NPM is an online collection of software where developers can share the code they've written to be used by other developers
- NPM is used to install things like `express` or `react` to your project

### Event-Driven Architecture
- When coding normal programs, one will typically know the flow of code and when certain events will happen.  When developing for the web, however, we won't know when specific events will occur and need to plan around that
- An example of not knowing when an even will occur is a user clicking a button to submit a form
- Node provides an `EventEmitter` class in the `events` core module.  These emitters can emit or receive events that trigger new code to be called
- Example:
  ```
  let events = require('events')
  let listenerCallback = (data) => {
    console.log('Celebrate ' + data);
  }

  const myEmitter = new events.EventEmitter(); // creates the emitter

  myEmitter.on('celebration', listenerCallback); // creates the callback for the 'celebration' event

  myEmitter.emit('celebration', 'this is a string'); // emits the 'celebration' event
  ```

### Asynchronous JavaScript with Node
- When working on server-side development, we are typically performing tasks that consume quite a bit of time like reading files or querying databases.  With normal development, this would halt the execution of our code and make it increadibly slow
- With Node's event loops, we are able to denote which code we want to be asynchronous and which we want to be synchronous.  It enables our time consuming code to be handled in a non blocking way
- You can use `async/await` with newer versions of Node

### Errors
- The Node environment has all standard JavaScripterrors as well as the `error` class for creating new instances of errors.  We can generate errors and `throw` them to handle and log them
- Many Node APIs uses `error-first callback functions` that have an error as the first argument of the funciton and data as the second
  - If the error argument is undefined, proceed as normal, else handle error

### Filesystem
- All data on a computer is organized and accessed through a filesystem.  When JavaScript is running on a browser it is very important for a script to only have limited access to the user's filesystem
- Reducing the access to the filesystem is known as `sandboxing` which protects users from malicious programs
- Backend code **must** have less restricted interaction with the file system
- The Node `fs` module is used to interact with the filesystem from your program
- All methods in `fs` have both an synchronous version and an asynchronous version
- An example of reading a file:
    ```
    const fs = require('fs');
    
    let readDataCallback = (err, data) => {
    if (err) {
        console.log(`Something went wrong: ${err}`);
    } else {
        console.log(`Provided file contained: ${data}`);
    }
    };
    
    fs.readFile('./file.txt', 'utf-8', readDataCallback);
    ```

## Express
- Express is a Node module that can be used for anything from static file servers to REST api to full production servers
### How to start a server
- First, you must require the `express` module and create the `app`.  Once you have these in your file, you can then start listenin on a port to start the server
  ```
  // Import the express library here
  const express = require('express');
  // Instantiate the app
  const app = express();

  const PORT = process.env.PORT || 4001;

  // Start listening on the port
  app.listen(PORT, () => {
    console.log(`Server is now ilstening on port ${PORT}`);
  });
  ```
### How to create a route
- After the server starts listening, it can take nearly any request
- We specify how we take these requests by creating `routes`
- A `route` is the path after the hostname and port of a url
  - Ex: localhost:3000`/this/is/the/path`
- Since each request will be associated with an HTTP verb (i.e. GET, POST, DELETE, etc) our app can have each verb for each `route`
- An example of a `GET` for the route `/expressions`:
  ```
  app.get('/expressions', (req, res, next) => {
    console.log(req);
  });
  ```
- The first argument for these functions is a string containing the `route` for the request
- The second argument is a callback function for when a request is received.  The arguments are the request (`req`), the response (`res`), and the `next` middleware function

### How to send a response
- Once we create our route, we must create the response.  HTTP has a **one request one response** rule where you must always send exactly one response to a request
- Express servers send responses using the send method of the response object with `res.send(<data to send>)`
  ```
  app.get('/expressions', (req, res, next) => {
    console.log(req);
    const data = { name: 'Gerritt' };
    res.send(data.json());
  });
  ```

### Dynamic routing
- Routing becomes much more powerful with dynamic routing.  The `/expressions` route mentioned previously is a static route meaning it has only one set of functionality for each verb
- You can use `route parameters` to create a dynamic route that can allow users to pass different values to the same route to achieve different results
- `Route Parameters` are route path segments that begin with a semi-colon.  These act as wildcards that match any text at that segment of the path.  An example is `/expressions/:id` which would allow someone to access a specific expression id
- Express parses all `route parameters`, extracts their values, and attaches them to the request object as an object themselves found at `req.params`
- The keys of `req.params` will match the `route parameters` of your route

### Sending status codes
- Express allows for setting [status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) before sending the response to any given request
- These status codes provides the client with information on how the request was handled
- You can set the `status code` of a response object by using the `.status()` method of the response
- For ease of use, other response methods can be chained onto `.status()`.  An example would be `res.status(<code>).send(<data>)`
  ```
  app.get('/expressions/:id', (req, res, next) => {
    const expression = getElementById(req.params.id, expressions);
    if(expression) {
      res.status(200).send(expression);
    } else {
      res.status(404).send('Expression not fount');
    }
  });
  ```

### Additional HTTP methods
- Three other incredibly important HTTP verbs other than `GET` are `POST`, `PUT`, and `DELETE`
  - `POST` requests are used to create new resources/entries in the database
  - `PUT` requests are used to update the resources already in the database
  - `DELETE` is pretty self explanatory.  It deletes the requested resource
- The express `app` has methods for all HTTP verbs.  If you want to support a `GET` and a `POST` on the same route, you will have to have:
  ```
  // GET method for route
  app.get('/route/to/endpoint', (req, res, next) => {
    ...
  });
  // POST method for route
  app.post('/route/to/endpoint', (req, res, next) => {

  });
  ```

### How to use queries
- `Query strings` appear at the end of URL paths and are indicated with a question mark
- These query strings are formatted as `?query_1=val1&query_2=val2...&queryN=valN` and are appended to the end of a route parameter
- These strings aren't considered part of the route path and are parsed into an object found at `req.query` in the request object


## Express Routers
- Using express in a single file gets very cumbersome very fast as your project begins to expand
- Express routers allows you to split your express routes into many files to keep the files smaller and more manageable
- An express router provides a subset of the express methods
- To create an instance of a router, you must invoke the `.Router()` method in the top level file of your project (The main app file)
- To then use the router, you need to mount a certain `route path` in the first argument of the `app.use()` method, and provide the router as the second argument
  ```
  // create the router
  const expressionsRouter = express.Router();

  // mount the route to it
  app.use('/monsters', expressionsRouter);
  ```

### Using multiple router files
- You will typically want to have each router in its own dedicated file and simply require them in the main file
- This keeps our code short, clean, and separated
  ```
  // expressions.js
  const express = require('express');
  const expressionsRouter = express.Router();

  expressionsRouter.get('/', (req, res, next) => {
    res.send(expressions);
  });

  module.exports = expressionsRouter;
  ```
  ```
  // app.js
  const express = require('express');
  const app = express();
  const expressionsRouter = require('./expressions.js');

  app.use('/expressions', expressionsRouter);
  ```

## Express Middlewares
- One coding principle to follow to help reduce bugs and improve readability is the **D**on't **R**epeate **Y**ourself (DRY) principle.  Your goal is to use as little code as possible to get your tasks done
- When coding express routes you may find yourself writing the same code over and over which opens the door for silly bugs
- You can have the same code run before every request by using `middleware`
- `Middleware` is code that runs between the server receiving a request and sending the response
- `Middleware` can perform certain logic on the `req` and `res` objects such as:
  - Perform logic based on the request
  - Attach info to the response
  - Give a status to the response
  - Send the response to the user
- You denote a middleware by using the `app.use()` method
  ```
  // this simple middleware just logs that a request was received
  app.use((req, res, next) => {
    console.log('Request received');
  });
  ```

### Using the next() function
- The previous code example is great for logging but it will cause one fatal flaw in our code.  It will not go on to the next function used for processing the request to our server! 
- To fix this, we add a call to the `next()` function.  This is the third argument in all of our route callback functions

### app.use() for specific routes
- The `app.use()` method can take an option first argument of a route to specify the middleware should only be ran on that specific route
- This is very useful for adding additional logging or checking specific values of the request
- If the route of the middleware is `/expressions` it will only run on requests to the `/expressions` route.  It will not run for any additional routes such as `/expressions:id`

// finished express