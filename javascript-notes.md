- [Javascript Notes](#javascript-notes)
  - [Variables](#variables)
    - [Differences between let and var](#differences-between-let-and-var)
  - [String interpolation](#string-interpolation)
  - [Math operators](#math-operators)
    - [Basic operators](#basic-operators)
  - [Logical opterations](#logical-opterations)
    - [Conditional statements](#conditional-statements)
    - [Comparistion operators](#comparistion-operators)
    - [Logical operators](#logical-operators)
    - [Truthy values](#truthy-values)
    - [Ternary Operator](#ternary-operator)
    - [Switch case statements](#switch-case-statements)
  - [Functions](#functions)
    - [Function expressions](#function-expressions)
  - [Arrays](#arrays)
  - [Loops](#loops)
  - [Iterators](#iterators)
  - [Objects](#objects)
    - [Basic Objects](#basic-objects)
    - [Methods](#methods)
    - [Looping through objects](#looping-through-objects)
  - [Advanced objects](#advanced-objects)
    - [Getters](#getters)
    - [Setters](#setters)
    - [Factory Functions (constructors)](#factory-functions-constructors)
    - [Built-in Object Methods](#built-in-object-methods)
# Javascript Notes
I have very little JS experience so I am starting from the beginning with the [codecademy](codecademy.com) javascript course and will be taking my notes initially based off that.  These notes may not go as indepth as other notes for easier subjects such as math operations or conditional statements.
## Variables
- `var`: Var was the variable keyword in pre-ES6 version of JS
- `let`: Let is the preferred way to declare a variable when it is able to be reassigned instead of using var.
- `const`: Const is used to declare variables with constant a constant value.  Consts cannot change.

### Differences between let and var
The following information was found on [stack overflow](https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var)
  - `var` variables are scoped to the entire function body while `let` variables are scoped to their closing block statement denoted by `{ }`
  - `var` variables are hoised meaning that they are initialized as `undefined` before the code is run meaning they are accessible before being declared.  `let` varaibles are not hoisted meaning if they are accessed before being initialized they will throw a `ReferenceError`
  - `var` variables are globally scoped if defined at the top level while `let` variables are not
  - `var` variables are able to be redeclared using the `var` keyword with the original value being replaced with the new value.  `let` variables are not able to be redeclared at the same level of scope with the `let` keyword with it throwing a `SyntaxError`.  If you have a let variable in a higher block/scope you can redeclare that variable in a lower block/scope without changing the higher one

## String interpolation
- When logging to the console the best way to format the output of strings is to use interpolation.  Instead of using quotations for the strings, use back tick marks ` and insert your variables into the string with ${variable}

## Math operators
### Basic operators
- Basic math operations such as `+, -, *, /` are to be expected
- To alter a variable and save it, just do `variableName X= y` where x is the math operator and y is how much you want to change the variable.  Ex `variableName += 2` translates to `variableName = variableName + 2`

## Logical opterations
### Conditional statements
- `if`, `else if`, and `else` statements operate like other coding languages
### Comparistion operators
- Typical comparison operators such as `<`, `>`, `<=`, `>=` are present in javascript
- `==` Checks if the value is equal but not type so `20 == "20"` evaluates to true
- `===` Check if value and type are equal so `20 === "20"` evaluates to false while `20 === 20` ise true
- `!==` checks if value and type are not equal
### Logical operators
- Typical logical operators like `&&`, `||`, and `!` are present in javascript
### Truthy values
- If you have a statement like `if(myVar)` and myVar === `0`, `""`, `''`, `null`, `undefined`, or `NaN` then it will evaluate to false.  If it is anything else it wil evaluate to true
- Below is a way to shorthand default variable assignments using truthys
```
let username = '';
let defaultName = username || 'Stranger';
 
console.log(defaultName); // Prints: Stranger
```
### Ternary Operator
- Simplify if else statements using ternary operators.  A ternary operator takes the form of `expression ? x : y`.  If `expression` evaluates to `true` x will execute but if it is `false` y will execute.
### Switch case statements
- Instead of having a massive chain of else if blocks, just use a switch statement
```
switch (groceryItem) {
  case 'tomato':
    console.log('Tomatoes are $0.49');
    break;
  case 'lime':
    console.log('Limes are $1.49');
    break;
  case 'papaya':
    console.log('Papayas are $1.29');
    break;
  default:
    console.log('Invalid item');
    break;
}
```
## Functions
- Function declarations start with the `function` keyword followed by the `function name` followed by parentheses and the function body
- Function parameters in JS work the same way as any other language
- You can have default parameters by setting the input to a value in the function declaration
```
function greeting (name = 'stranger') {
  console.log(`Hello, ${name}!`)
}
 
greeting('Nick') // Output: Hello, Nick!
greeting() // Output: Hello, stranger!
```
- Returning values works like in other coding languages
### Function expressions
- We can define an anonymous function to calculate the value of a variable.  The variable name will be the identifier and the function will be what the variable is equal to.
```
const calcArea = function(width, height){
  const area = width * height
  return area
}
```
- These function expressions are not hoisted so they cannot be called before they are defined
- Instead of declaring it as a function, ES6 introduced arrow syntax, `=> ()`, that removes the function keyword
- When using arrow syntax, parentheses are only needed if the function has no inputs or if it has more than 1 input.  If it has 1 input, no parentheses are needed
- A function body composed of a single-line block does not need curly braces.  If there are no parentheses, the one line block will evaluate and be automatically returned.
## Arrays
- Arrays in js seem to work the same way they do in python.  They can store any datatype and can store multiple data types in one list.
- JS arrays are zero indexed
- To get length of arrays it's `arrayName.length`
- To append values to the end of the array, it is `arrayName.push(value)`.  If you are adding multiple values just add more values like parameters
- To remove the last item of an array use the pop function. `arrayName.pop()` 
- `arrayName.shift()` removes the first item of the array
- `arrayName.unshift(value)` adds a new item to the beginning of the array
- `arrayName.slice(value)` will slice off the first `value` items of an array.  You can include a second parameter to give the values in an array between specific indexes
- `arrayName.indexOf(val)` will return the index of `val` in the array.  If val doesn't exist it will return `-1`
- All array documents can be found on the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- Arrays can be nested meaning they can contain arrays. If you have arrays within another array, you can access values with `myArr[x][y]`
## Loops
- `for` loops take the form of `for(let x = y; x < z, x++)` similar to C, C++ or Java
- `while` loops are also similar to that of C, C++ and Java
- `do while` loops are used to ensure a task is carried out at least once even if conditions satisfy the while loop to break out
- `break` keyword will stop the execution of a loop regardless of if the condition is satisfied or not
## Iterators
- The `.forEach()` function will loop through and execute the same code on every elemtent of an array
  - For each takes a callback function as an argument to execute on every item in the array
  - `.forEach()` will **ALWAYS** return `undefined`
  - `groceries.forEach(groceryItem => console.log(groceryItem));` wil print out every item to the console
```
const fruits = ['mango', 'papaya', 'pineapple', 'apple'];

// Iterate over fruits below
fruits.forEach(fruit => console.log("I want to eat a " + fruit)) //returns "I want to eat a <fruit>" for each fruit
```
- The `.map()` method is similar to `.forEach()` in that it takes a callback to operate on each element in an array but the difference is that it returns an array
  - This is used to create new arrays based on the current array being operated on
```
const animals = ['Hen', 'elephant', 'llama', 'leopard', 'ostrich', 'Whale', 'octopus', 'rabbit', 'lion', 'dog'];

// Create the secretMessage array below
const secretMessage = animals.map(animal => animal[0])

console.log(secretMessage.join('')); //HelloWorld

const bigNumbers = [100, 200, 300, 400, 500];
const smallNumbers = bigNumbers.map(num => num/100)
// Create the smallNumbers array below
console.log(smallNumbers) // [ 1, 2, 3, 4, 5 ]
```
- The `.filter()` method is also similar to `.forEach()` in that it takes a callback to operate on each element in an array but the difference is that it returns an array while performing some additional operations
  - This is used to filter out some values in the array based on conditions in the callback function
```
const randomNumbers = [375, 200, 3.14, 7, 13, 852];
const smallNumbers = randomNumbers.filter(num => num < 250)
const favoriteWords = ['nostalgia', 'hyperbole', 'fervent', 'esoteric', 'serene'];
const longFavoriteWords = favoriteWords.filter(word => {
  if(word.length > 7)
  {
    return word
  }
})
console.log(smallNumbers) // [ 200, 3.14, 7, 13 ]
console.log(longFavoriteWords) // [ 'nostalgia', 'hyperbole', 'esoteric' ]
```
- The `.findIndex()` function iterates through all elements in the array and returns the **FIRST** index that evaluates to `true`
```
const animals = ['hippo', 'tiger', 'lion', 'seal', 'cheetah', 'monkey', 'salamander', 'elephant'];
const foundAnimal = animals.findIndex(animal => {
  if(animal === 'elephant')
  {
    return animal
  }
})
console.log(foundAnimal) // 7
const startsWithS = animals.findIndex(animal => {
  if(animal[0] === 's')
  {
    return animal
  }
})
console.log(startsWithS) // 3
```
- The `.reduce()` method reduces the array to a single value.  This can be used to perform actions such as adding or multiplying all elements together.  You can add a second argument to the function to have a starting place for the accumulator
```
const newNumbers = [1, 3, 5, 7];
const newSum = newNumbers.reduce((accumulator, currentValue) => {
  console.log('The value of accumulator: ', accumulator);
  console.log('The value of currentValue: ', currentValue);
  return accumulator + currentValue
})
console.log(newSum) //16
const newSum2 = newNumbers.reduce((accumulator, currentValue) => {
  console.log('The value of accumulator: ', accumulator);
  console.log('The value of currentValue: ', currentValue);
  return accumulator + currentValue
}, 10) //Adding 10 to the sum
console.log(newSum2) //26
```

## Objects
### Basic Objects
- Objects can be assigned to variables 
- Use `{}` to designate an object literal
- Fill with unordered data.  Organized into key-value pairs
- Similar to a dictionary in python
```
//Defined like 
let animal = {
  'name': 'Jerry',
  'type': 'Penguin'
}
```
- Access values in the form of `animal.name // Penguin`
- Accessing properties that don't exist will return undefined
- Can create new properties with `objName.propName = <value>`
- Or you can access and edit values with bracket notation `objName[propName]`
```
let returnAnyProp = (objectName, propName) => objectName[propName];
 
returnAnyProp(spaceship, 'homePlanet'); // Returns 'Earth'
```
- `const` objects cannot be edited (i.e. have new properties added) but they are mutable (i.e. property values can be changed)
- To delete properties use `delete objName.propName`
### Methods
- You can add functions to objects as a method.  An example of a method is `console.log()` being a method where `.log()` is the method
```
const alienShip = {
  invade: function () { 
    console.log('Hello! We have come to dominate your planet. Instead of Earth, it shall be called New Xaculon.')
  }
};
```
- You can nest objects inside of other objects.  This looks VERY similar to JSON just with added functions
- Objects are passed by reference.  This means when an object is the argument of a function, the pointer of the object is passed meaning any changes to the object are permanent changes
### Looping through objects
- You can use `for ... in` syntax to loop through nested object in an object
```
let spaceship = {
  crew: {
    captain: { 
      name: 'Lily', 
      degree: 'Computer Engineering', 
      cheerTeam() { console.log('You got this!') } 
    },
    'chief officer': { 
      name: 'Dan', 
      degree: 'Aerospace Engineering', 
      agree() { console.log('I agree, captain!') } 
    },
    medic: { 
      name: 'Clementine', 
      degree: 'Physics', 
      announce() { console.log(`Jets on!`) } },
    translator: {
      name: 'Shauna', 
      degree: 'Conservation Science', 
      powerFuel() { console.log('The tank is full!') } 
    }
  }
}; 
 
// for...in
for (let crewMember in spaceship.crew) {
  console.log(`${crewMember}: ${spaceship.crew[crewMember].name}`);
}
```
##  Advanced objects
- Similar to python you need to use the `this` keywords when accessing variables of an objects within its methods
```
const robot = {
  model: '1E78V2',
  energyLevel: 100,
  provideInfo()
  {
    return `I am ${this.model} and my current energy level is ${this.energyLevel}.`
  }
};
console.log(robot.provideInfo()) //I am 1E78V2 and my current energy level is 100.
```
- **NEVER USE `this` KEYWORD IN ARROW FUNCTIONS IN OBJECTS**
  - The `this` that arrow functions reference are the global `this` as opposed to the object's `this`
  - Javascript does not have privacy built in for objects.  Due to this, the common convention is to include an underscore as the first character of "private" property names (properties that shouldn't be altered)
```
const bankAccount = {
  _amount: 1000
}
```
### Getters
- Getters get and return internal properties of the object
- They use the `get` keyword before the function declaration
```
const robot = {
  _model: '1E78V2',
  _energyLevel: 100,
  get energyLevel()
  {
    if(typeof this._energyLevel === 'number')
    {
      return `My current energy level is ${this._energyLevel}`
    }
    else
    {
      return 'System malfunction: cannot retrieve energy level'
    }
  }
};

console.log(robot.energyLevel) // My current energy level is 100
```
### Setters
- Setters are similar to getters in that they use a keyword.  This keyword is `set`
- Used to set the value of private variables 
- Can be same name as getter
```
const robot = {
  _model: '1E78V2',
  _energyLevel: 100,
  _numOfSensors: 15,
  get numOfSensors(){
    if(typeof this._numOfSensors === 'number'){
      return this._numOfSensors;
    } else {
      return 'Sensors are currently down.'
    }
  },
  set numOfSensors(num)
  {
    if(typeof num === 'number')
    {
      if(num >= 0)
      {
        this._numOfSensors = num
      }
      else
      {
        console.log('Pass in a number that is greater than or equal to 0')
      }
    }
  }
};
robot.numOfSensors = 100
console.log(robot.numOfSensors) // 100
```
### Factory Functions (constructors)
- Factory functions are used to create objects using a function
- These functions can take parameters for properties
```
const monsterFactory = (name, age, energySource, catchPhrase) => {
  return { 
    name: name,
    age: age, 
    energySource: energySource,
    scare() {
      console.log(catchPhrase);
    } 
  }
};
const monster = monsterFactory('Jeff', 23, 'potatoes', 'POTATOES')
```
- ES6 introduced shorthand notation for factory functions called property value shorthand where you can use the input names as the property names/assignment
```
const monsterFactory = (name, age) => {
  return { 
    name,
    age 
  }
};
```
- Destructured assignment is another shorthanded technique for access of variables
```
const { residence } = vampire; 
console.log(residence); // Prints 'vampire.residence'
```
### Built-in Object Methods
- [Link for object methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object#Methods)
- `Object.keys(objectName)` returns an array of the object property keys
- `Object.entries(objectName)` returns an array of arrays containing key value pairs (almost like an array of tuples)
- `Object.assign(target, source)` adds the source to the target and returns.  This will change the target object.
  - To copy an object use `let newObj = Object.assign({}, oldObj)
