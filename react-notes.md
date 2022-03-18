# React Notes
## These will be notes that I take while completing the Codecademy "Create a Front-End App with React" Skill Path


### Class objects in Javascript
- Classes are used for object oriented programming (OOP) to model data to fit the real world
- Classes are used to create multiple of similar objects that have the same traits but different values

#### Constructors
- Constructors are methods used to create a new instance of a class
- Constructos can take any amount of arguments

#### Instance
- An instance of a class is an object that contains all of the same properties and methods of the class but it has unique property values
- You create an instance of a class by assigning it to a variable using the `new` keyword
  ```
  const classInstance = new myClass()
  ```

#### Methods
- The creation of methods for classes is very similar to that of objects but you **DO NOT** include commas between them
- Methods are functions built into a class used to perform actions with the class and its values 
- `Getters` and `Setters` are methods used to retrieve or set a specific value of a class
  ```
  // Getter and Setter Example
  class myClass {
      constructor() {
          this._name = 'Value'
      }

      set name(newName) {
          this._name = newName
      }

      get name() {
          return this._name
      }
  }
  ```
- `Methods` are general functions for the class that can be used either as private methods or public methods
  ```
  class myClass {
      foo() {
          console.log('foo')
      }
  }
  ```

#### Inheritance
- When multiple classes share similar properties and have very few differences they are candidates for inheritance
- Inheritance is helpful for reducing the amount of code that you have to write
- To use inheritance, you create a `parent` class (aka `superclass`) with the properties and methods that will be shared by all of the `child` classes (aka `subclass`). The child class inherits all of the properties and methods from the parent class
- To create a child class of a parent class, you use the `extends` keyword in the class declaration
  ```
  class childClass extends parentClass {
      // Child specific info
  }
  ```
- To pass information of a child to the parent class properties, you will use the `super` keyword to call the constructor of the parent class and set the value of the property
- All methods of the parent class are available to the child class but not the other way around
- Any properties specific to the child class will have to have their own getters and setters

#### Static Methods
- Static methods are methods that can be called by the `class` but not by individual instances
- A good example of this is the built in `Date` class.  You can call `Date.now()` to get the current date but you cannot call the `.now()` method from individual instances of the date class


### Runtimes
- A runtime environment is where javascript is executed.  Two of the main javascript runtimes are the `browser` like chrome or firefox and `Node`
#### Browser Runtime
- Web browsers have the ability to run javascript on sites.  Applications created for the browser that run in browser are known as front end applications

#### Node
- The Node runtime environment is a runtime for javascript that runs outside of a browser
- This runtime allowed developers to create a `Fullstack` application all in javascript


### Modules
- Modules are used to create reusable pieces of code that can be exported from one file and imported in another
- Instead of writing the entire program in one file, it is better to break it up into bite sized modules in multiple files.  This helps with readability and reusability

## Intro to JSX
### Why React?
- React is fast and responsive to the user
- React is `modular` meaning you write small, efficient modules that are reused
- Very scalable
- Flexible
- React is very **POPULAR** and can get you a job

### What is JSX
- JSX is an extension for javascript used by React to create components of HTML.  These components are small and efficient.
- JSX elements are treated as Javascript `expressions`.  This means they can be saved to variables, passed to functions, added to objects, etc.
- You write JSX almost exactly like HTML.  You can use `elements` and `attributes`
- You can nest JSX just like in HTML
- JSX expressions **MUST** have only **ONE** outer element.  A common fix is to wrap the expression in a container div

#### Rendering JSX
- To render JSX you call the render function from the `ReactDOM`.  DOM stands for `Data Object Model` and is a library for Javascript used by react
- The `.render()` function parses your JSX, creates a tree of DOM nodes, and adds it to the to the tree of the DOM which renders it on screen
- `.render()` takes 2 arguments.  The first argument is the JSX you want to render while the second argument is the element that you want to act as the container of your JSX.  
  ```
  // A typical call of the render method could look like this:
  ReactDOM.render(<h1>Render me!</h1>, document.getElementById('app'));
  ```
- The first argument of `.render()` doesn't have to be pure JSX.  It just has to evaluate to JSX meaning you can pass a variable containing JSX
- The special thing about the `ReactDOM` is that it **ONLY** updates DOM elements that have been changed
- In HTML it is common to use the `class` attribute of elements but you can't use this in JSX.  JSX uses the `className` attribute.  This is due to `class` being a reserved term in Javascript

### Self closing tags
- In JSX any element that uses a self closing tag like `br` or `img` must use a slash before the ending carat
  ```
  // This is REQUIRED
  <br />
  // This is WRONG
  <br>
  ```
### Use Javascript expressions in JSX
- To use JS expressions in JSX you simply need to put it between curly braces `{}`
  ```
  <h1>2 + 3</h1> // Will render '2 + 3' on the screen
  <h1>{2 + 3}</h1> // Will render '5' on the screen
  ```
- You can access variables within JSX expressions by wrapping them in curly bracecs.  This is how you can make your apps dynamic because when your variables change, the DOM will rerender the component and show it on screen
- You can even set `attributes` of your JSX elements equal to the value of your variables
- JSX elements can have event listeners like `onClick` or `onMouseHover` just like HTML.  You can even set these listeners equal to your own functions
- All JSX event listeners are camelCase instead of lowercase like in regular HTML
- You **CANNOT** inject if statements into JSX.  Instead handle the logic outside of your JSX to handle conditionals
- You **CAN* inject ternary operators into JSX 
- Another way to write a conditional in JSX is to use `&&`. This is best used for conditionals where if a condition is met, it will output the JSX but if it is not met, it does nothing
- A good way to act upon a full list and convert it to JSX is by using the `.map()` function for lists.
- Another way to create JSX without writing JSX is by using the `React.createElement` function
  ```
  const h1 = React.createElement(
    "h1",
    null,
    "Hello, world"
  );
  ```


## React Components
- A react component is a small reusable piece of code that is responsible for one job
- You can define components using either Javascript `class` extension or `functions`
- You define a component once and then you can render them as many times as you want
- Defining a component:
  ```
  class MyComponent extends React.Component {
    render() {
      // your JSX
      return <your jsx>
    }
  }
  ```
- Component names **must** start with a capital letter.  They follow the `UpperCamelCase` naming convention

### The render function
- Within the body of a react component, there exists a required method.  This is the `render()` function.
- The `render()` function must contain a return statement.  Most of the time it will return JSX
- The render function can contain more than just the return statement.  The render function can contain logic before the return to act upon your data and change what is rendered.
  - This logic needs to go within the render function.  
- You can define functions within the class to be called in the render function


### Creating an instance
- If you have a component named `MyComponent` then you will create an instance of it as such:
  ```
  <MyComponent />
  ```
- You can pass properties to React components in the same way you can give attributes to HTML
  ```
  <MyComponent name=<value> />
  ```
- The props can then be accessed within the component using `this.props.<propName>`
  ```
  class MyComponent extends React.Component {
    render() {
      return <h1>{this.props.name}</h1>
    }
  }
  ```

### Event listeners in components
- You can define event listeners for components as if they were functions of the `class`

## Components and Props
### Components in other components
- Components use the render method to return JSX.  One type of JSX that they can return are other React components!
- To include other components in a React component, first you must `import` the component into your file
  ```
  import { Component } from '<file path to component>'
  ```
- In order for you to `import` a component, you must first `export` that component from it's respective file
  ```
  export class Component extends React.Component {
    // component logic
  }
  ```
- The ability to nest components is the true power of react.  Each component on its own is small and insignificant but as you create and render more components, your page will come to life
### Component props
- Not all components are static components.  Most of the time you will want to pass data to your Components in the form of `props`
- You pass props into components the same way you pass attributes to HTML elements
  ```
  <MyComponent propName=<value> />
  ```
- `props` are then referenced in your `class` components in this manner:
  ```
  this.props.propName
  ```
- `props` will **ALWAYS** be the name used to reference the props passed to `class` components.  You cannot access class component props in any way other than `this.props`
- Not only can you use props to be rendered on the screen but you can also pass props to be used to make decisions on what to render
- You can even pass event handling functions as props!  If you create a event handler as a method of your `class` component, you can pass it to a component with:
  ```
  <Component propName={this.handlerName} />
  ```
### Naming props
- You can name props anything that you want as long as you don't assign them a JS restricted name.  
- Name your props with the camelCase convention
- When defining event handlers to be passed as props it is best to name both the prop and the event handler something relevent to what the function does
  - You can even name event handling functions reserved HTML names like `onClick` or `onHover`.  This is because those events are reserved names in `HTML` but when passing a prop to a component, it is JavaScript 

### Children
- Every `class` components props has a property called `children`
- If you used a non self closing component tag, all info passed between the opening and closing tags will be in the `children` property
- This means you can pass more JSX between the opening and closing tags of a component and it will be referenced with `children`

### defaultProps
- What should you do if someone doesn't pass all of the props to your components?
- Normally if the props is missing, then nothing will render in the place of the prop
- You can give your component `class` a property known as `defaultProps`
- Populate `defaultProps` with an object containing the default values that you wish to be displayed if a prop is missing
- You define `defaultProps` **OUTSIDE** of the `class` component with
  ```
  Component.defaultProps = // props object
  ```
-