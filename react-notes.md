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