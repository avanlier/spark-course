# Abstracting Data with Java: Abstract Classes and Methods

In the world of Java programming, data abstraction is a fundamental concept that involves concealing specific implementation details while presenting only the essential information to users. This essential concept is realized through the utilization of either abstract classes or interfaces, which will be further elaborated upon in the upcoming sections.

## Understanding the `abstract` Keyword

The `abstract` keyword serves as a non-access modifier in Java, applied to both classes and methods. Here's a breakdown of its usage:

### Abstract Class

An abstract class is a restricted class that cannot be directly instantiated to create objects. To access it, you must inherit from another class. Abstract classes may contain a mixture of abstract and regular methods. For instance:

```
abstract class Animal {
  public abstract void animalSound();
  public void sleep() {
    System.out.println("Zzz");
  }
}
```

Attempting to create an object of the `Animal` class directly will result in an error:

```
Animal myObj = new Animal(); // This will generate an error
```

To access and utilize an abstract class, it must be inherited by another class. In the following example, we convert the `Animal` class used in the Polymorphism chapter into an abstract class:

Recall from the Inheritance chapter that we employ the `extends` keyword to inherit from a class:

```
// Abstract class
abstract class Animal {
  // Abstract method (has no body)
  public abstract void animalSound();
  // Regular method
  public void sleep() {
    System.out.println("Zzz");
  }
}

// Subclass (inherits from Animal)
class Pig extends Animal {
  public void animalSound() {
    // The body of animalSound() is provided here
    System.out.println("The pig says: wee wee");
  }
}

class MyMainClass {
  public static void main(String[] args) {
    Pig myPig = new Pig(); // Create a Pig object
    myPig.animalSound();
    myPig.sleep();
  }
}
```

### Abstract Method

Abstract methods, on the other hand, can only exist within an abstract class and do not contain a method body. Instead, the implementation of the method is deferred to subclasses that inherit from the abstract class.

## Benefits of Abstract Classes and Methods

Now, let's delve into the reasons and scenarios for using abstract classes and methods:

### Enhancing Security

One primary motivation for employing abstract classes and methods is to bolster the security of your code. By abstracting away certain implementation details, you can ensure that only the most critical aspects of an object are exposed, safeguarding sensitive or complex internals from direct access. This abstraction of data helps maintain the integrity and stability of your software, making it easier to manage and extend in the long run.