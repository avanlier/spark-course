## Table of Contents

1.  Introduction
2.  Java Collections Framework
3.  Collection Interfaces
    -   List
    -   Set
    -   Queue
4.  Collection Classes
    -   ArrayList
    -   LinkedList
    -   HashSet
    -   TreeSet
    -   HashMap
    -   TreeMap
5.  Collections Utility Class
6.  Java Tuple
7.  Examples
8.  Conclusion
9.  References

## Introduction

Java Collections Framework provides a comprehensive architecture for representing and manipulating collections of objects. It includes interfaces, implementations, and algorithms for working with collections. Collections simplify data manipulation and improve code readability and reusability.

## Java Collections Framework

The Java Collections Framework consists of:

-   **Interfaces**: Abstract data types that represent collections. Examples include `List`, `Set`, and `Queue`.
-   **Implementations**: Classes that provide concrete implementations of the collection interfaces. Examples include `ArrayList`, `HashSet`, and `LinkedList`.
-   **Algorithms**: Methods that perform useful computations on objects that implement collection interfaces.
-   **Comparator and Comparable**: Interfaces and classes to enable sorting of elements in collections.

![Collections in Java - javatpoint](https://static.javatpoint.com/images/java-collection-hierarchy.png)

## Collection Interfaces

### List

-   Represents an ordered collection of elements.
-   Allows duplicates.
-   Commonly used implementations: `ArrayList`, `LinkedList`.

### Set

-   Represents an unordered collection of unique elements.
-   Does not allow duplicates.
-   Commonly used implementations: `HashSet`, `TreeSet`.

### Queue

-   Represents a collection used for holding elements prior to processing.
-   Commonly used implementations: `LinkedList`.

## Collection Classes

### ArrayList

-   Implements the `List` interface.
-   Resizable array.
-   Provides fast random access.
-   Not synchronized (use `Collections.synchronizedList()` for synchronization).

### LinkedList

-   Implements the `List` and `Queue` interfaces.
-   Doubly-linked list.
-   Efficient for insertions and deletions.
-   Not synchronized.

### HashSet

-   Implements the `Set` interface.
-   Uses a hash table for storage.
-   No duplicate elements.
-   Not synchronized (use `Collections.synchronizedSet()` for synchronization).

### TreeSet

-   Implements the `NavigableSet` interface.
-   Sorted set using a Red-Black tree.
-   No duplicate elements.
-   Not synchronized.

### HashMap

-   Implements the `Map` interface.
-   Stores key-value pairs.
-   Allows one null key and multiple null values.
-   Not synchronized (use `Collections.synchronizedMap()` for synchronization).

### TreeMap

-   Implements the `NavigableMap` interface.
-   Sorted map using a Red-Black tree.
-   No duplicate keys.
-   Not synchronized.

## Collections Utility Class

The `java.util.Collections` class provides various utility methods for manipulating collections. Some commonly used methods include `sort()`, `shuffle()`, and `binarySearch()`.

## Java Tuple

A tuple is a simple data structure that can hold a collection of elements of different data types. In Java, tuples are not built-in as a distinct data structure, but you can create your own tuple-like structures using arrays, classes, or libraries like Apache Commons Lang's `Pair` class. Let's create a simple tuple example using arrays:

```
public class TupleExample {
    public static void main(String[] args) {
        // Create a tuple using an array
        Object[] tuple = { "Alice", 25, true };

        // Access tuple elements
        String name = (String) tuple[0];
        int age = (int) tuple[1];
        boolean isStudent = (boolean) tuple[2];

        // Print tuple elements
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Is Student: " + isStudent);
    }
}
```
In this example, we have created a simple tuple using an array. The tuple contains three elements: a name (string), an age (integer), and a flag indicating whether the person is a student (boolean).

Here's what the program does:

1.  We create an array called `tuple` that holds the three elements.
2.  We use array indexing and casting to extract the elements from the `tuple`.
3.  We store the extracted elements in variables (`name`, `age`, and `isStudent`).
4.  Finally, we print the values of these variables to the console.

When you run this program, it will output:

```
Name: Alice
Age: 25
Is Student: true
```

This example demonstrates how you can create a simple tuple-like structure in Java using an array. However, keep in mind that for more complex scenarios, you may want to consider using custom classes or external libraries that provide tuple-like functionality with type safety and additional features.


## Examples

### Example 1: Using ArrayList

```
import java.util.ArrayList;
import java.util.List;

public class ArrayListExample {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        for (String name : names) {
            System.out.println(name);
        }
    }
}
```

**Explanation:**

-   In this example, we are using the `ArrayList` class from the Java Collections Framework.
-   We start by importing the necessary classes (`ArrayList` and `List`) from the `java.util` package.
-   We create an instance of `ArrayList` called `names`, which holds a collection of strings.
-   We use the `add()` method to add three names ("Alice," "Bob," and "Charlie") to the `names` list.
-   Next, we iterate through the `names` list using a for-each loop. This loop iterates through each element (in this case, names) in the list.
-   Inside the loop, we print each name to the console.

**Output:**

```
Alice
Bob
Charlie
```

### Example 2: Using HashMap

```
import java.util.HashMap;
import java.util.Map;

public class HashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> ages = new HashMap<>();
        ages.put("Alice", 25);
        ages.put("Bob", 30);
        ages.put("Charlie", 28);

        int bobAge = ages.get("Bob");
        System.out.println("Bob's age: " + bobAge);
    }
}
```

**Explanation:**

-   In this example, we are using the `HashMap` class from the Java Collections Framework to create a mapping of names to ages.
-   We import the necessary classes (`HashMap` and `Map`) from the `java.util` package.
-   We create an instance of `HashMap` called `ages`, which stores mappings from names (strings) to ages (integers).
-   We use the `put()` method to add three key-value pairs to the `ages` map. These pairs represent names and their corresponding ages.
-   We retrieve Bob's age using the `get()` method and store it in the `bobAge` variable.
-   Finally, we print Bob's age to the console.

**Output:**

```
Bob's age: 30
```

### Example 3: Simulating a Tuple

```
public class TupleExample {
    public static void main(String[] args) {
        // Simulate a tuple using an array
        Object[] tuple = { "Alice", 25, true };
        
        String name = (String) tuple[0];
        int age = (int) tuple[1];
        boolean isStudent = (boolean) tuple[2];
        
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Is Student: " + isStudent);
    }
}
```

**Explanation:**

-   In this example, we simulate a tuple using a simple array.
-   We create an array called `tuple` that holds three elements: a string, an integer, and a boolean value.
-   We retrieve the elements from the `tuple` array using array indexing and casting to the appropriate data types.
-   We extract the name (a string), age (an integer), and a boolean flag indicating whether the person is a student.
-   Finally, we print the extracted values to the console.

**Output:**

```
Name: Alice
Age: 25
Is Student: true
```

In this example, we simulate a tuple because Java doesn't have a built-in tuple type, so we use an array or a custom class to represent a collection of values with different data types.

## 8. Conclusion

The Java Collections Framework provides a rich set of classes and interfaces for working with collections of data. Understanding these collections is essential for efficient data manipulation and algorithm implementation in Java.

## 9. References

-   [Oracle Java Collections Tutorial](https://docs.oracle.com/javase/tutorial/collections/intro/index.html)
-   [JavaTpoint Collections in Java Tutorial](https://www.javatpoint.com/collections-in-java)
