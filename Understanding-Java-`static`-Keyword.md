## Table of Contents

1.  Introduction
2.  The `static` Keyword
3.  Static Variables
4.  Static Methods
5.  Static Blocks
6.  Static Import
7.  Examples
8.  Conclusion
9.  References

## 1. Introduction

In Java, the `static` keyword is used to define properties and methods that belong to a class rather than to instances (objects) of that class. `static` members are shared across all instances of the class and can be accessed without creating an object of the class. This lab document will explore the various aspects of the `static` keyword in Java.

## 2. The `static` Keyword

The `static` keyword is used to declare static members (variables, methods, and blocks) within a class. These members are associated with the class itself, not with instances of the class. The key characteristics of `static` members are:

-   They are shared among all instances of the class.
-   They can be accessed using the class name rather than an object reference.
-   They are initialized only once when the class is loaded into memory.

## 3. Static Variables

Static variables, also known as class variables, are used to store data that is common to all instances of the class. They are declared with the `static` keyword and are typically used for constants or shared data.

**Syntax:**

```
public class MyClass {
    static int staticVariable;
}
```

## 4. Static Methods

Static methods are methods that can be called on a class itself, rather than on an instance of the class. They are often used for utility functions that don't depend on the state of the object.

**Syntax:**

```
public class MyClass {
    static void staticMethod() {
        // Static method code
    }
}
```

## 5. Static Blocks

Static blocks are used to initialize static variables or perform one-time initialization tasks when the class is loaded into memory. They execute before the class's constructor is called.

**Syntax:**

```
public class MyClass {
    static {
        // Static block code
    }
}
```

## 6. Static Import

Static import is a feature that allows you to access `static` members of a class directly without specifying the class name. It simplifies code but should be used sparingly to avoid confusion.

**Syntax:**

```
import static packageName.className.staticMember;
```

## 7. Examples

### Example 1: Static Variable

```
public class Circle {
    static final double PI = 3.14159265359; // Static constant
    
    static double calculateArea(double radius) {
        return PI * radius * radius;
    }
    
    public static void main(String[] args) {
        double radius = 5.0;
        double area = Circle.calculateArea(radius);
        System.out.println("Area of the circle: " + area);
    }
}
```

**Explanation:**

-   In this example, we have a class named `Circle`.
-   Inside the `Circle` class, there is a `static final` variable named `PI`, which is a constant representing the value of pi (π). The `static final` keyword combination makes `PI` a constant, and it is common to use uppercase letters for constants in Java.
-   The class also contains a `static` method called `calculateArea(double radius)`. This method calculates the area of a circle using the provided radius and the `PI` constant.
-   In the `main` method, we create an instance of the `Circle` class (even though it's not required because the methods and variables we're using are `static`).
-   We call the `calculateArea` method, passing a radius of `5.0`, and store the result in the `area` variable.
-   Finally, we print the calculated area to the console.

**Note:**

-   The `PI` variable is declared as `static final` because it is a constant value that should not be modified.
-   The `calculateArea` method is declared as `static` because it doesn't rely on the state of any specific `Circle` object and can be called directly on the class itself.

### Example 2: Static Method

```
public class MathUtils {
    static int multiply(int a, int b) {
        return a * b;
    }
    
    public static void main(String[] args) {
        int result = MathUtils.multiply(5, 3);
        System.out.println("Result: " + result);
    }
}
```

**Explanation:**

-   In this example, we have a class named `MathUtils`.
-   Inside the `MathUtils` class, there is a `static` method called `multiply`, which takes two integers `a` and `b` as parameters and returns their product.
-   In the `main` method, we call the `multiply` method by referencing it with the class name `MathUtils`. We pass `5` and `3` as arguments.
-   The result of the multiplication is stored in the `result` variable, and we print the result to the console.

**Note:**

-   The `multiply` method is declared as `static` because it performs a mathematical operation and doesn't need to be associated with specific `MathUtils` objects.

### Example 3: Static Block

```
public class Configuration {
    static String environment;

    static {
        // Initialize environment from configuration file
        environment = readEnvironmentFromConfigFile();
    }

    private static String readEnvironmentFromConfigFile() {
        // Read environment from a file
        return "Production";
    }

    public static void main(String[] args) {
        System.out.println("Current Environment: " + Configuration.environment);
    }
}
```

**Explanation:**

-   In this example, we have a class named `Configuration`.
-   Inside the `Configuration` class, there is a `static` variable named `environment`, which is used to store the current environment (e.g., "Production" or "Development").
-   There is also a `static` block, indicated by `static { ... }`, which is used for one-time initialization tasks when the class is loaded into memory. In this block:
    -   The `readEnvironmentFromConfigFile` method is called to read the environment from a configuration file.
    -   The result is assigned to the `environment` variable, initializing it with the environment value.
-   In the `main` method, we simply print the current environment value.

**Note:**

-   The `static` block is executed once when the class is loaded into memory, ensuring that the `environment` variable is initialized before it's used.
-   This is a common pattern for performing class-level initialization tasks.

These examples illustrate how the `static` keyword is used to define static variables, static methods, and static blocks in Java, allowing us to work with class-level data and behavior without needing to create instances of the class.

## 8. Conclusion

In this lab document, we have explored the `static` keyword in Java, which allows us to define static variables, static methods, and static blocks within a class. Static members are associated with the class itself and are shared among all instances of the class. Understanding and using `static` members can help simplify code and improve performance in certain scenarios.

## 9. References

-   Oracle Java Documentation: [Static Members](https://docs.oracle.com/javase/tutorial/java/javaOO/classvars.html)
-   Java Tutorials: [Static Import](https://docs.oracle.com/javase/tutorial/java/package/staticimport.html)