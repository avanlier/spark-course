In Java, a **method** is a block of code that only runs when it is called. Methods can receive data, known as **parameters**, and they are commonly referred to as **functions**.

### Creating a Method

To create a method, it must be declared within a class and defined with a name followed by parentheses `()`:

```
public class MyClass {
  static void myMethod() {
    // Code to be executed
  }
}
```

In this example:

-   `myMethod()` is the method's name.
-   `static` indicates that the method belongs to the `MyClass` class rather than an instance of `MyClass`. You'll learn more about objects and accessing methods through objects later.
-   `void` means that this method does not return a value. We'll cover return values later in this chapter.

### Calling a Method

To call a method in Java, you write the method's name followed by two parentheses `()` and a semicolon. Here's an example using the `myMethod()`:

```
public class MyClass {
  static void myMethod() {
    System.out.println("I just got executed!");
  }

  public static void main(String[] args) {
    myMethod(); // Call the myMethod() method inside main
  }
}

// Outputs "I just got executed!"
```

### Method Parameters

Methods can receive information in the form of parameters, which are specified after the method name within parentheses. You can include as many parameters as needed, separated by commas. Here's an example of a method that takes a `String` parameter called `fname`:

```
public class MyClass {
  static void myMethod(String fname) {
    System.out.println(fname + " Shao");
  }

  public static void main(String[] args) {
    myMethod("Jesse");
    myMethod("Larry");
    myMethod("Anja");
  }
}

// Outputs:
// Jesse Shao
// Larry Shao
// Anja Shao
```

### Return Values

The `void` keyword, as used in the previous examples, indicates that the method does not return a value. If you want a method to return a value, you can specify a primitive data type (such as `int`, `char`, etc.) instead of `void` and use the `return` keyword inside the method:

```
public class MyClass {
  static int myMethod(int x) {
    return 5 + x;
  }

  public static void main(String[] args) {
    System.out.println(myMethod(3));
  }
}

// Outputs 8 (5 + 3)
```

You can also store the result in a variable:

```
public class MyClass {
  static int myMethod(int x, int y) {
    return x + y;
  }

  public static void main(String[] args) {
    int z = myMethod(5, 3);
    System.out.println(z);
  }
}

// Outputs 8 (5 + 3)
```

### Methods with Conditional Statements

It is common to use conditional statements like `if...else` inside methods to control the flow of execution:

```
public class MyClass {

  static void checkAge(int age) {
    if (age < 18) {
      System.out.println("Access denied - You are not old enough!"); 
    } else {
      System.out.println("Access granted - You are old enough!"); 
    }
  } 

  public static void main(String[] args) { 
    checkAge(20); // Call the checkAge method and pass an age of 20
  } 
}

// Outputs "Access granted - You are old enough!"
```