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

