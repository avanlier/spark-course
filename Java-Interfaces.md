## Introduction to Java Interfaces

In Java, another approach to achieving abstraction is through the use of interfaces.

An `interface` serves as a completely "**abstract class**" that serves the purpose of grouping related methods with empty bodies:

```
// Example of an interface
interface Animal {
  public void animalSound(); // Interface method (lacks a body)
  public void run(); // Interface method (lacks a body)
}
```

To access the methods defined in an interface, another class must "implement" the interface, using the `implements` keyword instead of `extends`. The body of the interface methods is provided by the implementing class:

```
// Example of interface usage
interface Animal {
  public void animalSound(); // Interface method (lacks a body)
  public void sleep(); // Interface method (lacks a body)
}

// The "Pig" class implements the "Animal" interface
class Pig implements Animal {
  public void animalSound() {
    // The body of the animalSound() method is provided here
    System.out.println("The pig says: wee wee");
  }
  public void sleep() {
    // The body of the sleep() method is provided here
    System.out.println("Zzz");
  }
}

class MyMainClass {
  public static void main(String[] args) {
    Pig myPig = new Pig();  // Create a Pig object
    myPig.animalSound();
    myPig.sleep();
  }
}
```

**Key Notes on Interfaces**:

-   Similar to **abstract classes**, interfaces cannot be used to instantiate objects (in the example above, it's not possible to create an "Animal" object in the `MyMainClass`).
-   Interface methods do not have method bodies; the implementing class provides the method implementations.
-   When implementing an interface, you must override all of its methods.
-   Interface methods are, by default, abstract and public.
-   Interface attributes are, by default, public, static, and final.
-   Interfaces cannot contain constructors, as they cannot be used for object creation.

**Why and When to Use Interfaces**:

1.  **Security**: Interfaces enable the hiding of specific details, showing only the essential aspects of an object (interface).
    
2.  **Multiple Inheritance**: Java does not support "multiple inheritance" (a class can inherit from only one superclass). However, interfaces allow a class to implement multiple interfaces by separating them with commas.
    

### Implementing Multiple Interfaces

To implement multiple interfaces, list them separated by commas:

```
interface FirstInterface {
  public void myMethod(); // Interface method
}

interface SecondInterface {
  public void myOtherMethod(); // Interface method
}

// DemoClass "implements" both FirstInterface and SecondInterface
class DemoClass implements FirstInterface, SecondInterface {
  public void myMethod() {
    System.out.println("Some text..");
  }
  public void myOtherMethod() {
    System.out.println("Some other text...");
  }
}

class MyMainClass {
  public static void main(String[] args) {
    DemoClass myObj = new DemoClass();
    myObj.myMethod();
    myObj.myOtherMethod();
  }
}
```
In this way, a class can implement multiple interfaces, allowing for greater flexibility in defining its behavior.