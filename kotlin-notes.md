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
- String templates use `$` followed by variable names to add the value of the variable into the string
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