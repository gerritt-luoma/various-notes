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
  - `var` variables are able to be redeclared using the `var` keyword with the original value being replaced with the new value.  `let` variables are not able to be redeclared with the `let` keyword with it throwing a `SyntaxError`

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
