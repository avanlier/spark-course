## Java Classes

### I. Classes and Objects

Java is an object-oriented programming language, which means that programs are constructed around objects and their interactions. Objects encapsulate both state and behavior.

In Java, everything is centered around classes and objects, each having their own attributes and methods. For instance, in real life, a car is an object with attributes like weight and color, and methods like drive and brake.

The core concept in object-oriented programming is the class.

A class is a set of instructions that define how an instance behaves and what data it holds.

```
Here is a Java class definition:

public class Car {
  // The scope of the Car class starts after the curly brace

  public static void main(String[] args) {
    // The scope of main() starts after the curly brace

    // Program tasks

  }
  // The scope of main() ends after the curly brace

}
// The scope of the Car class ends after the curly brace

```

Let's illustrate with another example: a savings account at a bank.

What should a savings account know?

-   The balance of money available.

What should a savings account do?

-   Deposit money.
-   Withdraw money.

![1](https://s3.amazonaws.com/codecademy-content/courses/learn-java/revised-2019/diagram+of+an+object-02.png)

1.  **Creating a Class**

```
public class MyClass {
  int x = 5;
}
```

**Note**: In Java, class names should always start with an uppercase letter, and the Java file name should match the class name.

2.  **Creating Objects** - Instances of a Class

```

public class MyClass {
  int x = 5;
  int y = 10;

  public static void main(String[] args) {
    MyClass myObj1 = new MyClass();  // Object 1
    MyClass myObj2 = new MyClass();  // Object 2
    System.out.println(myObj1.x);
    System.out.println(myObj2.y);
  }
}

```

You can also create an object of a class and access it from another class. This approach is often used for better organization of classes (one class contains attributes and methods, while another holds the `main()` method, which is the executable code).

```

// In MyClass.java
public class MyClass {
    int x = 5; // Attribute in the MyClass class
}

// In OtherClass.java
public class OtherClass {
    public static void main(String[] args) {
        MyClass myObj = new MyClass();
        System.out.println(myObj.x);
    }
}

```

### II. Class Attributes, Variables, and Fields

1.  **Accessing Attributes**

You can access attributes by creating an object of the class and using the dot syntax (`.`):

```
public class MyClass {
  int x = 5;

  public static void main(String[] args) {
    MyClass myObj = new MyClass();
    System.out.println(myObj.x);
  }
}

```

2.  **Modifying Attributes**

Set the value of `x` to 66:

```

public class MyClass {
  int x;

  public static void main(String[] args) {
    MyClass myObj = new MyClass();
    myObj.x = 66; // Now, x is 66
    System.out.println(myObj.x);
  }
}

```

Override existing values:

```

public class MyClass {
  int x = 11;

  public static void main(String[] args) {
    MyClass myObj = new MyClass();
    myObj.x = 55; // Now, x is 55
    System.out.println(myObj.x); 
  }
}

```

If you don't want the ability to override existing values, declare the attribute as `final`:

The `final` keyword is useful when you want a variable to always hold the same value, such as PI (3.14159...).

```

public class MyClass {
  final int x = 10;

  public static void main(String[] args) {
    MyClass myObj = new MyClass();
    // The following line will generate an error: cannot assign a value to a final variable
    // myObj.x = 25; 
    System.out.println(myObj.x); 
  }
}

```

If you create **multiple objects of the same class**, you can change the attribute values in one object without affecting the attribute values in the others:

```

public class MyClass {
  int x = 5;

  public static void main(String[] args) {
    MyClass myObj1 = new MyClass();  // Object 1
    MyClass myObj2 = new MyClass();  // Object 2
    myObj2.x = 25;
    System.out.println(myObj1.x);  // Outputs 5
    System.out.println(myObj2.x);  // Outputs 25
  }
}

```

### III. Class Methods

1.  **Creating and Calling a Method**

Create a method named `myMethod()` in MyClass:

```

public class MyClass {
  static void myMethod() {
    System.out.println("Hello World!");
  }

  public static void main(String[] args) {
    myMethod(); // Outputs "Hello World!"
  }
}

```

`myMethod()` prints a message (the action) when it is **called**. To call a method, simply write the method's name followed by parentheses `()` and a semicolon.

2.  **Static vs. Public**

You will often encounter Java programs that have either static or public attributes and methods.

Here's a comparison between static and public methods:

```

public class MyClass {
  // Static method
  static void myStaticMethod() {
    System.out.println("Static methods can be called without creating objects");
  }

  // Public method
  public void myPublicMethod() {
    System.out.println("Public methods must be called by creating objects");
  }

  // Main method
  public static void main(String[] args) {
    myStaticMethod(); // Call the static method
    // myPublicMethod(); This would result in a compilation error

    MyClass myObj = new MyClass(); // Create an object of MyClass
    myObj.myPublicMethod(); // Call the public method on the object
  }
}

```

**Example**:

```

// Create a Car class
public class Car {
 
  // Create a fullThrottle() method
  public void fullThrottle() {
    System.out.println("The car is going as fast as it can!");
  }

  // Create a speed() method and add a parameter
  public void speed(int maxSpeed) {
    System.out.println("Max speed is: " + maxSpeed);
  }

  // Inside main, call the methods on the myCar object
  public static void main(String[] args) {
    Car myCar = new Car();     // Create a myCar object
    myCar.fullThrottle();      // Call the fullThrottle() method/function
    myCar.speed(200);          // Call the speed() method/function
  }
}

// Output:
// The car is going as fast as it can!
// Max speed is: 200

```

**Note**:

-   The `main()` method is a built-in Java method that runs your program, and any code inside `main` is executed.
-   The dot (`.`) is used to access the attributes and methods of an object.
-   To call a static method in Java, you write the method name followed by parentheses `()`.
-   To call a public method in Java, you use the syntax `object_name.method_name()`.
-   The class name must match the filename (e.g., `Car` in `Car.java`).