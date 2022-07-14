- [Kotlin notes](#kotlin-notes)
  - [Why to learn kotlin](#why-to-learn-kotlin)
  - [Kotlin basics](#kotlin-basics)
  - [Formatting conventions](#formatting-conventions)
  - [How Kotlin goes from code to a functioning program](#how-kotlin-goes-from-code-to-a-functioning-program)
  - [Data Types and Variables](#data-types-and-variables)
    - [Declaration and Initialization of Variables](#declaration-and-initialization-of-variables)
    - [Declaring an Immutable Variable](#declaring-an-immutable-variable)
    - [Type Inference](#type-inference)
  - [Using Text Variables](#using-text-variables)
    - [Strings and Characters](#strings-and-characters)
    - [String Concatenation](#string-concatenation)
    - [String Templates](#string-templates)
    - [User Input](#user-input)
    - [Built-in Functions and Properties of Strings](#built-in-functions-and-properties-of-strings)
    - [Character Escape Sequences](#character-escape-sequences)
  - [Using Number Variables](#using-number-variables)
    - [Arithmetic Operators](#arithmetic-operators)
    - [Order of Operations](#order-of-operations)
    - [Augmented Assignment Operators](#augmented-assignment-operators)
    - [Increment and Decrement Operators](#increment-and-decrement-operators)
    - [Math Library](#math-library)
  - [Conditional Expressions](#conditional-expressions)
    - [If statements](#if-statements)
    - [Else statements](#else-statements)
    - [Else-If Statements](#else-if-statements)
    - [Comparison Operators](#comparison-operators)
    - [Equality and Inequality Operators](#equality-and-inequality-operators)
    - [Logical Operators](#logical-operators)
    - [Order of Evaluation](#order-of-evaluation)
    - [Nested Conditionals](#nested-conditionals)
    - [When Expressions](#when-expressions)
    - [Range](#range)
  - [Collections](#collections)
    - [Lists](#lists)
    - [Sets](#sets)
    - [Maps](#maps)
  - [Loops](#loops)
    - [For Loops](#for-loops)
    - [Control the iteration of a for loop](#control-the-iteration-of-a-for-loop)
    - [Iterating through collections](#iterating-through-collections)
  - [Functions](#functions)
    - [Creating and Calling functions](#creating-and-calling-functions)
    - [Return Statements](#return-statements)
    - [Single Expression Functions](#single-expression-functions)
    - [Function Literals](#function-literals)
  - [Classes](#classes)
    - [Creating Classes](#creating-classes)
    - [Init Block](#init-block)
    - [Member Functions](#member-functions)
# Kotlin notes
I have very little kotlin experience at the time of writing this.  I will be following [codecademy's kotlin course](https://www.codecademy.com/learn/learn-kotlin) while writing these notets.  Due to experience with other languages this might not be fully detailed.
## Why to learn kotlin
- Compatible with java
- General purpose coding language
- Concise syntax with additional safety features
- Google's preferred android development language

## Kotlin basics
- Kotlin requires a main function to run
  - Without a main function the program will throw an error because it won't know where to start 
- Similar to JavaScript, semicolons are optional in Kotlin
- You can print text to the console through the `println(<expression>)` command
  - There is also the `print(<expression>)` command which does the same thing as `println` without adding a new line at the end
- When Kotlin is ran it is compiled to machine code that can be read by the `Java Virtual Machine (JVM)`  which then handles the execution of the code
- You can write comments using the same syntax as JavaScript or C with single line comments being `//` and multi line comments being `/* */`

## Formatting conventions
- Kotlin indentation typically uses a tab size of 4 spaces as opposed to the default of 2 spaces on many IDEs 
  - Improper indentation won't cause an error like in Python but it does make reading the code much harder
- When writing comments add a space between the beginning or end of comments 
  - Single line comments should be formatted as `// comment`
  - Multi line comments should be formatted as `/* comment */`
- The opening curly bracket should be on the same line as the entrance to the block of code it contains while the ending curly bracket should be on it's own line in line with the start of the block of code 
  ```
  if(condition){
    ...
  }
  ```

## How Kotlin goes from code to a functioning program
- The code first is checked over by the compiler to verify that there are no errors within the code 
- If no errors are found, the compiler then translates the `source Kotlin code ` to `Java Bytecode` in the form of `.class` files that are then passed on to the `JVM`
- Kotlin is a statically compiled language meaning the code is translated all types are checked before run time.  When an error is found it will display the corresponding error message to the terminal and terminate the rest of the program.
- If the IDE being used doesn't have a built in converter between Kotlin and Java then the bash terminal can be used.
  - To compile and save the kotlin code in the bash terminal and save it to a `.jar` file you can run 
    ```
    $ kotlinc example.kt -include-runtime -d example.jar
    ```
  - `kotlinc` is the compiler being used to compile the Kotlin code to byte code
  - `-include-runtime` is a flag that makes the compiler save the compiled code in a runnable `.jar` file
  - `.jar` files are a file format that represent many Java files that have been compiled and zipped into one file
  - `-d` denotes the output file for the compiled code
  - Once the Kotlin code has been compiled into the `.jar` file you can run it with
    ```
    $ java -jar example.jar
    ```
  - `java` is the command that launches java code.  It starts the JVM and loads the .class file, and launches the code written in the `main()` function
  - `-jar` is a flag that instructs the JVM to execute the code from within a `.jar` file
  - **IMPORTANT:** Similar to any other compiled language, if you make any changes to your code you **MUST** rebuild your code 

## Data Types and Variables
### Declaration and Initialization of Variables
- To declare and initialize a variable Kotlin uses the form
  ```
  var varName : dataType = varValue
  ```
- The information of the variable on the left side of the equals sign is the `declaration` of the variable. This is where we declare the name and type of the variable
  - Kotlin variable naming conventions use the `camelCase` format where the first word is lowercase and all subsequent words have their first letter capitalized.  Not following this naming convention will not cause errors but it will decrease the readability of the code
  - The first letter of the data type **MUST** be upper case i.e. `Int` or `String`
- The information on the right side of the equals sign is the `initialization` of the variable.  This is where the variable is actually given its value
  - Variables to not need to be initialized when they are created.  They can be declared on one line and initialized later
    ```
    var numExample : Int // declaration of numExample
    numExample = 3 // initialization of numExample
    println(numExample) // 3
    ```
### Declaring an Immutable Variable
- Sometimes we don't want the value of a variable to change much like a `const` in Javascript.  We denote this using the `val` keyword instead of the `var` keyword
  ```
  val valName : dataType = value
  ```
- The rule of Kotlin is that if you are **CERTAIN** that the variable will change, use `var` but use the `val` keyword in all other cases
- The compiler will throw an error if you attempt to reassign the value of an immutable variable

### Type Inference
- The compiler is smart enough to infer the datatype of a variable during its declaration and initialization meaning you don't always have to include the datatype in the declaration
  ```
  val someBool : Boolean = true // valid declaration
  val someBool = true // valid declaration
  ```
- Regardles of how the variable was declared, variables can **NEVER** change their type throughout the program.  Any attempt to do so will result in an error. An example is that you can't assign a boolean to a variable of String type 

## Using Text Variables
### Strings and Characters
- `String` datatypes are a collection of characters wrapped in `double quote` marks. The characters in a string can be a combination of digits, letters, symbols, and whitespaces like spaces, tabs, or newlines
  ```
  val someString : String = "Coding123!"
  ```
- `Char` datatypes are a single character wrapped in `single quote` marks.  They can be the same types of characters as `String` variables
  ```
  val someChar : Char = 'C'
  ```
### String Concatenation
- You can concatenate strings together using the `+` operator
  ```
  "Strings" + " " + "are neat" = "Strings are neat"
  ```

### String Templates
- String templates are very similar to `string interpolation` in JavaScript and `f strings` in Python
- String templates use `$` followed by variable names to add the value of the variable into the string.  For an expression like a list size, use curly brackets `${val}`
  ```
  val variableName : Int = 3
  "The value is $variableName" -> "The value is 3"
  ```
- String templates are much easier to read and faster to write than string concatenation

### User Input
- User input is a very important part of programming because it allows the user to interact with the programs we write
- To take in a user input we use the `readLine()` function which pauses the program until an input is given by the user.  Once the `enter` key is pressed the `readLine()` function returns whatever was typed into the console as a `String`

### Built-in Functions and Properties of Strings
- This will only cover one used function and property of String datatypes but the full documentation for all datatypes can be fount [here](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-string/)
- `Properties` provide information on a particular value of the variable it is being called on
  - `Strings` only have one property which is their `length`
    ```
    val someString = "yeet"
    println(someString.length) // 4
    ```
- `Functions` are used to perform specific tasks on the variable that they are called on.  You call these functions by appending `.functionName()` to the end of the variable name
  - The `.capitalize()` function for strings ensures the first character in the string is capitalized
    ```
    var someString : String = "cu boulder"
    println(someString.capitalize()) // Cu boulder
    ```

### Character Escape Sequences
- Character escape sequences are used to format strings such as add new lines and tabs
  - `\n` Adds a new line
  - `\t` Adds a tab
  - `\r` Adds a carriage return
  - `\'` Adds a single quote
  - `\"` Adds a double quote 
  - `\\` Adds a backslash 
  - `\$` Adds a dollar sign

## Using Number Variables
### Arithmetic Operators
- Kotlin supports the classic arithmetic operators like any other coding language
  - `+` - Addition
  - `-` - Subtraction
  - `*` - Multiplication
  - `/` - Division
  - `%` - Modulus

### Order of Operations
- It is important to remember the order of operations of math when writing code.  Kotlin uses an order of operations similar to that of `PEMDAS` but instead it is
    1. Parentheses
    2. Multiplication
    3. Division
    4. Modulus
    5. Addition
    6. Subtraction
- Exponents are not included in the order of operations for Kotlin because it lacks an exponent operator.  Instead, Kotlin uses the `.pow()` function for exponents

### Augmented Assignment Operators
- Augmented assignment operators performs an operation on a variable and reassign the variable to the output of the operation.
    ```
    x = x + y
    x += y // these lines mean the same thing
    ```
- You can use augmented assignment for any of the mathmatical operators

### Increment and Decrement Operators
- You can increment or decrement a variable using either the `++` operator or the `--` operator
- Perform the same function as `+=1` and `-=1`
    ```
    var x = 6
    x++ // 7
    x-- //6
    ```

### Math Library
- The Math library is a library that can be used to perform complex mathematical calculations that can't easily be done with the basic arithmetic operators
- `Math.pow(x,y)` is a function that raises x to the y power.  It takes in and returns a double
- `Math.min(x,y)` returns the smaller value between x and y
- `Math.max(x,y)` returns the larger value between x and y
- `Math.random()` returns a random float between 0 and 1
- `Math.round(x)` takes a double as an input and rounds to the nearest Int

## Conditional Expressions
- Conditional expressions are expressions that are evaluated down to a `true` or a `false`

### If statements
- If statements will check a conditional expression and if it evaluates to true, it will execute the block of code contained in it
    ```
    if(x){
        // internal block
    }
    ```
### Else statements
- If the conditional of an `if` statement evaluates to false and want your program to execute specific code only when this happens, you can follow your if statement with an else statement
    ```
    if(x){
        // if block
    } else {
        //else block
    }
### Else-If Statements
- Sometimes conditional expressions can't be represented with just an if/else block and there may be more specific scenarios that need to be checked.  You can use else-if statements to add more conditional expressions to be checked.  You can use as many else if statements as you want
    ```
    if(x > 5){
        // if block
    } else if(x < 4){
        // else if block
    } else{
        // else block
    }

### Comparison Operators
- You can use comparison operators in conditional statements to compare one value with another to evaluate it to a boolean
- These comparison operaters include `<`, `>`, `>=`, and `<=`

### Equality and Inequality Operators
- You can use (in)equality operators to determine if two values are or aren't equal.  The equality operator is `==` and the inequality operator is `!=`

### Logical Operators
- Logical operators evaluate the relationship between two booleans/expressions to return a true or false.
- The `and` operator is denoted by `&&` and will only return true if both sides of the and are true 
    ```
    if(x && y) //only true if x and y are true
    ```
- The `or` operator is denoted by `||` and returns true if either of the sides are true
    ```
    if(x || y) // true if either are true
    ```
- The `not` operator is denoted by `!` and returns the opposite of the inverse of the expression
    ```
    var x = true
    var y = !x //false
    ```

### Order of Evaluation
- The `Order of Evaluation` is similar to that of the `Order of Operations` except it is for complex boolean expressions
- The order follows:
    1. Boolean expressions within a set of parentheses
    2. NOT - `!`
    3. AND - `&&`
    4. OR - `||`

### Nested Conditionals
- It is possible to contain conditional expressions within other conditional expressions to achieve more precise logical solutions
    ```
    if(x){
        if(y){
            // if x && y
        }
        else {
            // if x && !y
        }
    } else {
        if(y){
            // if !x && y
        } else {
            // if !x && !y
        }
    }
    ```

### When Expressions
- `when` expressions are similar to switch statements in Python or JavaScript in that you input a value and check specific cases and act on those cases
- State the value cases and point towards the code to be executed with an arrow `->`
- For all unspecified cases use `else`.  Similar to the `default` for JavaScript
    ```
    var x = 1
    when(x){
        1 -> println("Small")
        2 -> println("Medium")
        3 -> println("Large")
        else -> println("Not an accepted number")
    }
    ```

### Range
- Kotlin can create ranges of values between x and y using `x..y`
- You can check if a value is in a range by using the `in` keyword
    ```
    if(z in x..y)
    ```
- This can be used for both numbers and characters

## Collections
### Lists
- Lists are a collection of values stored in an orderly fashion
- Lists can be `mutable` and `immutable` by using either of the `var` and `val` keywords.  Mutability decided by the keyword `listOf` or `mutableListOf`
  ```
  var/val exList = listOf(val1, val2, val3 ..., valN) // Immutable list
  var/val exList = mutableListOf(val1, val2, val3 ..., valN) // Mutable list
  ```
- The type of list can be inferred by the compiler or you can declare it yourself
  ```
  var/val stringList = List<String>
  ```
- Lists in Kotlin start with an index of 0.  Values are accessed in a similar way to Java or Python with the syntax `listName[index]`.  Accessing an element with an index that doesn't exist will throw an out of bounds error
- You can change the value at a particular index in a mutable list with `mutableList[index] = value`
- The size property of lists works much like the length property for strings in that it returns the number of elements 
  ```
  println(someArray.size) // num of elements
  ```
- Lists have built in functions that will allow you to perform various operations on them.  
  - The `.contains(val)` function that will check if a list contains a value and will return a boolean
  - The `.random()` function will return a random value from the list
- Mutable lists will have additional functions that have write access to the list
  - The `.add(val)` will append the value to the end of the list
  - The `.remove(val)` will remove the value.  If it doesn't exist it will return false

### Sets
- Sets are an unordered collection of unique elements.  Sets cannot have duplicate data stored in them
- Sets can also be `mutable` or `immutable`
  - Immutable sets are declared with the `setOf` keyword
    ```
    var/val immutableSet = setOf(val1, val2, ..., valN)
    ```
  - Mutable sets are declared with the `mutableSetOf` keyword 
    ```
    var/val mutableSet = mutableSetOf(val1, val2, ..., valN)
    ...
    or
    ...
    var/val mutableSet = mutableSetOf<Type>() // declares empty set
    ```

- You access elements in a set using the `elementAt(index)` function to access a value at index 
- If you access an element that doesn't exist, Kotlin will throw a `NullPointerException` error.  To ensure that doesn't happen, you can use the `elementAtOrNull(index)` function to get an element at an index.  If it doesn't exist it returns `null`
- You can use the `.add(val)` function to add one value to a set, the `.addAll(<list>)` will add all values in a list to a set, and the `.clear()` function will clear a set
- Additional set functions
  - `.first()` will return the first value of a set
  - `.last()` will return the last value of a set
  - `.sum()` will sum the elements of a set

### Maps
- Maps are a collection of key-value pairs much like JSON or Python dictionaries
- You create immutable maps by using the `mapOf` keyword 
  ```
  val/var immutableMap = mapOf(key1 to val1, key2 to val2, key3 to val3) // the to keyword is needed for every one
  ```
- You create mutable maps by using the `mutableMapOf` keyword
  ```
  val/var mutableMap = mutableMapOf(key1 to val1, key2 to val2, key3 to val3)
  ```
  - You can edit values at keys with mutable maps
- You retrieve the `value` at `key` with `mapName[key] // value`
- You can get all keys at once with `mapName.keys`
- You can get all values at once with `mapName.values`
- You can add values to a map using the `.put(key, value)` function that will add `value` to `key`
- You can remove values of a map using the `.remove(key)` function that will remove the key value pair bound to `key` from the map

## Loops
### For Loops
- For loops are used to loop a **KNOWN** amount of times
- A definition of a for loop:
  ```
  for(i in x..y) {
    println(i) // x and y are ints. can be int literal or expression
  }
  ```
### Control the iteration of a for loop
- To create a `reverse` range, use the `downTo` keyword keyword
  ```
  for(i in x downTo y) {
    println(i) // iterate from x down to y
  }
  ```
- To create a range excluding the upper boundary use thte `until` keyword
  ```
  for(i in x until y) {
    println(i) // iterates from x to (y-1)
  }
  ```
- To iterate by a non 1 value, use the `step keyword`
  ```
  for(i in x..y step z) {
    println(i) // iterates from x to y with a z stepsize
  }
  ```
### Iterating through collections
- You can use the structure of a collection as an iterator for a for loop
  ```
  val numbers = listOf(x, y, z)
  for (num in numbers) {
    println(num)
  }
  ...
  x
  y
  z
  ```
- To iterate through the `indices` of a collection use
  ```
  val numbers = listOf(x, y, z)
  for (index in numbers.indices) {
    println(index)
  }
  ...
  0
  1
  2
  ```
- You can get the `index` and `element` by using the `.withIndex()` function
  ```
  ```
  val numbers = listOf(x, y, z)
  for ((index, num) in numbers.withIndex()) {
    println("value: $num, index: $index")
  }
  ...
  value: x, index: 0
  value: y, index: 1
  value: z, index: 2
  ```

### Iterating Through Maps
- You can loop through they key value pairs of a map by looping through the `items` of a map
  ```
  for(item in mapOfItems){
    println("${item.value} ${item.key}")
  }
  ```
- You can also destructure the key value pairs into their own variables with
  ```
  for((itemKey, itemValue) in mapOfItems) {
    println("$itemKey $itemValue)
  }
  ```
- You can also get the keys and values to loop through by using the `.keys` and `.values` properties of maps

### While loops
- While loops are used when you are looping an unknown number of times
- They are similar to if statements in that they check a condition and if it is true, it will execute the block of code contained by the while loop
- If the condition is false when the code first reaches the while loop, the while loop will never execute 

### Do While Loops
- Do while loops are similar to that of while loops but they will always execute at lease once even if the condition of the while loop starts off false
  ```
  val condition = false
  do {
    print("This happens once")
  } while(condition)
  ...
  This happens once
  ```
### Nested Loops
- You can nest any kind of loop any number of times.  Be careful as adding loops will add to runtime and can cause slow code if not done properly

### Jump Expressions
- Jump expressions are used to change the standard behavior of loops by exiting a loop early or skipping a single repetition
- The `break` expression is used to exit a loop at a particular iteration
- The `continue` expression will skip the rest of the current iteration of the loop but will keep the loop going if there are any more iterations
  - This can be used to improve performance by removing unneeded operations in loops

### Labeled Jump Expressions
- In order to use jump expressions within nested loops, you can label outer loops of nested loops to execute jump expressions from inside inner loops
  ```
  val values = listOf(1,2,3)
  outer@ for(num1 in game) {
    for(num2 in game) {
      if(num1 == 2) {
        break@outer
      }
    }
  }

## Functions
### Creating and Calling functions
- The declaration of functions contains various bits of information regarting the inputs and outputs of functions
  ```
  fun functionName(arg1: Type): returnType {
    // body
  }
  ```
- `Arguments` are pieces of data that are used as inputs for functions in order to produce dynamic results
- You can have any number of arguments
- You can `name` or set `default` values for arguments.
  - `Naming` arguments means you can reference the argument name while calling the function to improve readability
  - `Default` arguments are set as a default value during the function declaration

### Return Statements
- Functions have the ability to return a value from a function to then be acted on later

### Single Expression Functions
- Single expression functions are functions that can be written with a single line of code

### Function Literals
- Function literals are unnamed functions that are treated as a value assigned to variables.  These can be passed as arguments or returned from functions as well
  ```
  val example = fun(arg1: type, arg2: type): type {
    // body
  }
  ```
- A much more concise way of doing this is through the use of lambda expressions
  ```
  val example = { arg1: type, arg2: type -> //body}
  ```

## Classes
### Creating Classes
- Classes in Kotlin are declared at the top of the file and outside of the main
  ```
  class Name {
    //body
  }
- In the class body you can define variables, constructors, and methods
- You create an instance of a class by setting a variable equal to the constructor of your class
  ```
  val myClass = className()
  ```
### Primary Constructor
- To pass variables to the constructor of a class, you must change the declaration of the class to take variables
  ```
  class myClass(var arg1: type, var arg2: type) {
    //body
  }

### Init Block
- The `init` block is used for initializing classes with additional logic
  ```
  class myClass(var arg1: type, var arg2: type) {
    var item: type

    init {
      // some logic to assign a value to item or some other logic depending on the arguments
    }
  }

### Member Functions
- Member functions are functions defined within a Class.  These extend the use of classes and objects to make them functional
