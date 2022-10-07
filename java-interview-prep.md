# Java Interview Prep
These notes are taken based off the Codecademy "Pass the Technical Interview with Java" course.

- [Java Interview Prep](#java-interview-prep)
  - [Scope in Java](#scope-in-java)
    - [Intro to Scope](#intro-to-scope)
    - [Access Modifiers](#access-modifiers)
    - [Static](#static)
    - [Method Overriding and Overloading](#method-overriding-and-overloading)
    - [Instance Variables](#instance-variables)
  - [Additional Java Concepts](#additional-java-concepts)
    - [Type Casting](#type-casting)
    - [Dictionaries](#dictionaries)

## Scope in Java
### Intro to Scope
- `Scope` defines where a certain variable and/or method is accessible within your program
- Variables can be defined with 3 levels of scope:
  1. `Class level scope`: Any variable declared within a class will be accessible by all methods within the class itself.  Depending on the `access modifier` (i.e. `public` or `private`) it can sometimes be access from outside of the method as well
  2. `Method level scope`: Any variable declared within a method is only able to be accessed within the method and nowhere else
  3. `Block level scope`: Any variable declared within a loop will only be accessible within the loop itself.  You can only access a variable after a loop if it was declared before the loop

### Access Modifiers
- Java currently has 4 `Access Modifiers` that are used to restrict the availability/accessibility of the method/variable it is used to modify.
- These modifiers are only used within classes and not within methods.
  1. `private`: This is the **most** restrictive modifier.  Private is used to restrict the method/variable to only be used within the class and nowhere else.
  2. `default`: This allows access from within the current `package` only.  If there is no modifier explicitly set, variables/methods will take this modifier by default
  3. `protected`: This will only allow access from within the current `package` unless it is access by a child class from outside of the package
  4. `public`: This is the **least** restrictive modifier.  This allows access to the class/method/variable from not only within the class itself but outside as well.

### Static
- `static` is a keyword that is added after the `access modifier` of a method or variable that indicates the declared entity is the same across all instances of the class and is able to be accessed even before an instance of that class is created


### Method Overriding and Overloading
- `Method Overriding`: A feature of Java that allows a subclass to have a method with the same name and parameters declared in the parent class.
  - Very handy because it allows the child class to have a specific behavior of that method that can differ from the parent class

- `Method Overloading`: A feature of java that allows classes/subclasses to have methods with the same name but take different parameters.  These overloaded methods are distinguished by the number of parameters they take

- `Constructor Overloading`: Similar to method overloading.  This is when a class has multiple constructors that all take different arguments.  Very useful when you want to change the instantiation of a class based off what data you have available at the time

### Instance Variables
- `Instance Variables`: The data/variables that are associated with a class object

```
public class Car {
    public String color;
    public int speed;

    public Car(String carColor, int carSpeed) {
        // Instantiate instance variables in constructor
        color = carColor;
        speed = carSpeed;
    }
    public static void main(String[]args) {
        Car carObject = new Car("red", 50);
    }
}
```
- In the example above, `color` and `speed` are the instance variables of the class
- When dealing with instance variables of a class, it is very important to use the `this` keyword to prevent ambiguity.  In the example above, `color` and `speed` could easily be confused for variables within a method.  Instance variables should instead be referenced with `this` as in the example below

```
public class Car {
    public String color;
    public int speed;

    public Car(String color, int speed) {
        // Use keyword this to instantiate variables
        this.color = color;
        this.speed = speed;
    }
}
```
- There are 2 other frequent uses of the keyword `this`
  1. You must use `this` when attempting to call an internal method of a class from inside itself. Example:
    ```
    public class Car {
        public String color;
        public int speed;

        public Car(String color, int speed) {
            this.color = color;
            this.speed = speed;
            // Use keyword this to call class method, race()
            this.race(speed);
        }

        public void race(int speed) {
            System.out.println("Raced at " + speed + " mph");
        }
    }
    ```
  2. When using `constructor overloading` you must call the overloaded constructor using `this`.  `this` must always be the first line within the constructor since it is creating the class instance
    ```
    public class Car {
        public String color;
        public int speed;
        public static String defaultColor = "black";
        public static int defaultSpeed = 30;

        public Car() {
            this(defaultColor, defaultSpeed);
        }

        public Car(String color, int speed) {
            this.color = color;
            this.speed = speed;
        }
    }
    ```

## Additional Java Concepts
### Type Casting
- `Type Casting` is the process of converting the value of one primitive data type to another primitive data type
- Data types can be considered as `lower` or `higher` depending on the amount of data that they store
- Lowest to highest primitive data types: Byte-->Short-->Int-->Long-->Float-->Double
- `Narrowing Type Casting`: When manually converting from a higher data type to a lower data type there will be a loss in data.  Example:
  ```
  double decimalNumber = 1.99;
  System.out.println(decimalNumber);
  int integerNumber = (int) decimalNumber;
  System.out.println(integerNumber);

  // output
  1.99
  1
  // here we can see we lost almost a full integer because when explicitly converting from double to int, anything past the decimal is just chopped off (just like in c/c++)
  ```
- `Widening Type Casting`: Java can automatically convert lower data types to higher data types and where will be no loss in data.  Example:
  ```
  int integerNumber = 1;
  System.out.println(integerNumber);
  double decimalNumber = (double) integerNumber;
  System.out.println(decimalNumber);

  // output
  1
  1.00
  // Java just added double 0's after the decimal
  ```
- `Other Types of Casting`: Casting can also be performed on non primitive data types such as `String` or `Object`.
- A very important thing to remember is that in Java, all classes are technically sub classes of the `Object` class

### Dictionaries
- In Java, a `Dictionary` is an abstract class that stores data using key-value pairs like a hash map
- When using a key you can retrieve the data that is associated with that key
- `Dictionary` is actually an abstract parent of the `Hashtable` class with the main difference being that `Hashtable` doesn't allow `null` to be a key