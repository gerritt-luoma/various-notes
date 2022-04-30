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
