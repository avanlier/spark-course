Welcome to the module on Functional Programming (FP) in Java! In this module, we will explore the fundamental concepts of functional programming in Java. In FP, functions or methods are the building blocks, and you use these functions to perform operations on data.

In the Functional Programming paradigm, computation and method invocation are treated as evaluation of mathematical expressions or functions. It does not change the program state and the data these functions operate on.

In this module, we'll delve into Java's Lambda Expressions, Functional Interfaces, and Streams that form the key components of functional programming in Java.

### **Agenda**
1. [Overview of Functional Programming Concepts](#overview)
2. [Lambda Expressions Overview](#lambda-expressions)
3. [Functional Interfaces and Lambda Expressions](#functional-interfaces)
4. [Creating Custom Functional Interfaces](#custom-interfaces)
5. [Introduction to Streams](#streams-intro)
6. [Stream Operations](#stream-operations)

### **1. Overview of Functional Programming Concepts** <a id="overview"></a>

In this section, we'll introduce the fundamental concepts of functional programming in Java.

##### **Introduction**

Functional programming is a programming paradigm that treats computation as the evaluation of mathematical expressions and avoids changing program state and mutable data. It is based on the following core principles:
- **Immutability:** In a real-world scenario, think of a banking application where financial transaction data should be immutable to ensure the consistency and auditability of transactions.
- **Pure Functions:** In a scientific calculation application, pure functions ensure that the same input always produces the same output, which is crucial for reproducibility.
- **First-class Functions:** In a data analysis application, first-class functions allow you to pass data transformation functions as arguments, enabling powerful data manipulation capabilities.

Functional programming benefits software development by promoting cleaner, more maintainable, and less error-prone code. It encourages code reuse and simplifies reasoning about complex systems.

### **2. Lambda Expressions Overview** <a id="lambda-expressions"></a>

in this section, we'll explore Lambda Expressions, their syntax, and provide examples to understand their usage.

##### **Introduction**
A Lambda expression in Java is a concise way to define and use anonymous functions, also known as lambda functions or closures. Lambda expressions allow you to express instances of single-method interfaces (functional interfaces) in a more compact and readable form. A programmer can now define and use a function without the need to create a separate class.

Lambda expressions promote functional programming in Java by making it easier to work with functions as first-class citizens. They were introduced in Java 8 and have since become a powerful tool in modern Java programming.

**Syntax of Lambda Expressions** <br>
`(parameters) -> expression`

- **Parameters:** These are the input arguments to the lambda function. You can have zero or more parameters.
- **Arrow (->):** Separates the parameter list from the body of the lambda expression.
- **Expression:** The body of the lambda expression, which can be an expression that computes and returns a value.

Lambda expressions are primarily used with functional interfaces (interfaces having only one abstract method). You can think of a lambda expression as a way to provide the inline implementation of that single abstract method in a concise manner.

**Issues Lambda Expressions Solve**

Lambda expressions in Java address several issues and provide benefits:
- **Conciseness:** Lambda expressions reduce boilerplate code when implementing functional interfaces. This makes code more concise and readable.
- **Readability:** By expressing the behavior of a function in a more compact form, lambda expressions often make code more readable, as the focus shifts from the mechanics of implementation to the intent of the code.
- **Functions as First-Class Citizens:** Lambda expressions treat functions as first-class citizens, which means you can pass functions as arguments to other functions, return them from other functions, and assign them to variables.
- **Built-in Functional Interfaces:** Java provides a rich set of built-in functional interfaces like, Consumer, Predicate, Functions that work seamlessly with lambda expressions.
- **Improved API Design:** Functional interfaces and lambda expressions encourage better API design by emphasizing the single abstract method that needs to be implemented. This helps in creating more intuitive and well-structured APIs.
- **Ease of Parallelism:** Lambda expressions simplify the use of Java's parallel processing capabilities, making it easier to write code that can take advantage of multi-core processors.
- **Reduced Bugs:** With less code to write and maintain, there are fewer opportunities for bugs to creep into the implementation, resulting in more reliable code.

In short, lambda expressions in Java are a powerful feature that enables more expressive and concise code, especially when working with functional interfaces, collections, and parallel programming. They help address issues related to code verbosity, readability, and ease of expressing behavior, ultimately leading to more efficient and maintainable code

**Example:** A Simple Lambda Expression, Lambda Expressions with Collections,  Sorting with Lambda Expression, and Lambda Expressions with Streams

***Note: Create a new file in IntelliJ with name as <u>LambdaExample.java</u> with following code and execute it***


```scijava
import java.util.*;
import java.util.function.Function;

public class LambdaExample {
    public static void main(String[] args) {
        // Define a lambda expression for squaring numbers
        Function<Integer, Integer> square = (x) -> x * x;

        // Create a list of integers
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Iterate through the list and print each number
        numbers.forEach((number) -> System.out.println(number));

        // Create a list of strings
        List<String> names = Arrays.asList("Bob", "Alice", "Dave", "Charlie");

        // Sort the list of names in alphabetical order
        names.sort((name1, name2) -> name1.compareTo(name2));

        // Print the sorted names
        names.forEach((name) -> System.out.println(name));

        // Apply the square function to each number and print the result
        numbers.forEach((number) ->
                          System.out.println(
                            "Square of " + number + " is " + square.apply(number)
                          )
                      );

        // A list of fruits
        List<String> fruits = Arrays.asList("apple", "banana", "cherry", "date");

        // Convert the list to a stream and then apply stream functions on it
        long count = fruits.stream()                          // Convert to stream
                    .filter(fruit -> fruit.startsWith("c"))   // Apply predicate
                    .count();                                 // Count stream elements

    }
}
```

##### **Exercise 1**
Write Lambda Expressions for basic operations like addition, subtraction, multiplication, and division.

### **3. Functional Interfaces and Lambda Expressions** <a id="functional-interfaces"></a>

Learn about functional interfaces and how they work with Lambda Expressions. We'll also cover predefined functional interfaces.

**Introduction**

Functional Interfaces are interfaces that contain a single abstract method and can be used as types for lambda expressions. It serves as a blueprint for lambda expressions and method references. In other words, functional interfaces define the contract for functions that can be passed around as values. Java provides several built-in functional interfaces in the `java.util.function` package.

<u>**Predefined Functional Interfaces**</u>
- **`Predicate<T>`:** In a filtering application, predicates allow you to specify conditions for selecting items from a collection. It takes one argument of type `T` and returns a `boolean` result.
- **`Function<T, R>`:** Widely used in data transformation applicationa, functions are essential for mapping one data type to another. Represents a function that takes one argument of type `T` and returns a result of type `R`.
- **`Consumer<T>`:** In a logging or notification system, consumers can process messages without returning a result. Represents a function that takes one argument of type `T` and returns no result.
- **`Supplier<T>`:** In a configuration management system, suppliers can provide configuration values. Represents a function that takes no arguments but returns a result of type `T`.

**Example:** Lets see how we can use the `Predicate<T>` and `Function<T, R>` functional interfaces using Lambda Expression.

***Note: Create a new file in IntelliJ with name as <u>FunctionalInterfaceEx.java</u> with following code and execute it***


```scijava
import java.util.function.Predicate;
import java.util.function.Function;

public class FunctionalInterfaceEx {
    public static void main(String[] args) {
        Predicate<Integer> isEven = (x) -> x % 2 == 0;
        System.out.println(isEven.test(4)); // true

        Function<Integer, String> intToString = (x) -> Integer.toString(x);
        System.out.println(intToString.apply(42)); // "42"
    }
}
```

**Exercise**

Use predefined Functional Interfaces to filter and map data in a list of integers.

*Hint: You can filter numbers that are ever or odd, or that are divisble by some specific number.*

### **4. Creating Custom Functional Interfaces** <a id="custom-interfaces"></a>

Discover how to create custom functional interfaces tailored to your specific use cases.


**Introduction**

Creating custom functional interfaces is athe core of functional programming in Java. Functional interfaces are interfaces that contain exactly one abstract method and can be used as the target types for lambda expressions or method references. While Java provides a set of predefined functional interfaces, discussed earlier, there are situations where you need to define custom functional interfaces to mimic specific behaviors or execute operations for your application. Let's explore them in more detail:

**Why Create Custom Functional Interfaces?**
- **Domain-specific Behavior:** Custom functional interfaces allow you to define behavior that is specific to your application's domain. For example, you might create a functional interface for a mathematical operation, a data transformation, or a validation rule that is unique to your project.
- **Enhanced Readability:** By creating custom functional interfaces, you can improve the readability of your code. It becomes clearer what the purpose of a lambda expression or method reference is when the functional interface's name reflects the intent.
- **Encapsulation:** Custom functional interfaces help encapsulate behavior. This means you can define the behavior in one place and reuse it across your application without exposing implementation details.

**Creating a Custom Functional Interface**

Here's how you can create a custom functional interface:
```
@FunctionalInterface
interface MyFunction {
    return-type performOperation(param-list);
}
```

<u>**Let's break down the components of this custom functional interface:**</u>
- **@FunctionalInterface:** This annotation is optional but recommended. It indicates that the interface is intended to be a functional interface. It helps in preventing accidental addition of more abstract methods to the interface.
- **interface MyFunction:** This is the declaration of the custom functional interface. In this example, we've named it `MyFunction`, but you should choose a meaningful name that reflects the purpose of the interface.
- **return-type performOperation(param-list);:** This is the single abstract method declared within the interface. It defines the method signature, parameters, and return type that any implementation of `MyFunction` must adhere to.

**Using Custom Functional Interfaces**

Once you've defined a custom functional interface, you can use it to create lambda expressions or method references.



Now imagine you're developing a physics simulation application where you need to calculate forces between particles. You could create a custom functional interface ***`ForceCalculator`*** to represent this calculation, and then provide different implementations for different force calculation algorithms, such as gravitational forces or electrostatic forces.

***Note: Create a new file in IntelliJ with name as <u>`GravitationalForceCalculator.java`</u> with following code and execute it***


```scijava
public class GravitationalForceCalculator {

    @FunctionalInterface
    interface ForceCalculator {
        double calculateForce(double mass1, double mass2, double distance);
    }

    public static void main(String[] args) {
        ForceCalculator gForce = (mass1, mass2, distance) -> {
            double gConstant = 6.67430e-11;
            return (gConstant * mass1 * mass2) / (distance * distance);
        };

        double force = gForce.calculateForce(5.98e24, 7.35e22, 3.84e8);
        System.out.println("Gravitational Force: " + force);
    }
}
```

In this example, the custom functional interface ***`ForceCalculator`*** allows you to encapsulate the behavior of calculating forces and provide different implementations as needed.

Custom functional interfaces are a powerful tool for defining and encapsulating behavior in a clean and reusable way, promoting good code organization and maintainability in your Java projects.

**Exercise**

Create and use a custom Functional Interface for a specific use case, such as calculating the area of a shape. Or assume you have a sales dataset and want to calculate custom sales statistics. You could define a `SalesAggregator` functional interface with a method `aggregate()` in it.

### **5. Introduction to Streams** <a id="streams-intro"></a>

Explore Java Streams, their characteristics, and how to create them.

##### **What are Java Streams?**
Java Streams are a sequence of elements that can be processed as they arrive using functional interfaces. They provide a high-level abstraction for working with data, allowing you to express complex data manipulation operations concisely and elegantly. Streams offer a way to process data lazily, which means that elements are processed on-demand as needed, rather than eagerly processing the entire data set upfront.

**Key characteristics of Java Streams include:**
- **Desing Operational Pipelines:** Streams allow you to create a series of data manipulation operations (e.g., validating, filtering, mapping, and reduction) that are executed sequentially in a pipeline. Each operation processes and transforms the data, and the result of one operation flows into the next.
- **Lazy Evaluation:** Stream operations are performed lazily, meaning that they only process elements when required. This lazy evaluation improves efficiency and allows for optimized processing of large data sets.
- **Functional Operations:** Streams support a wide range of functional-style operations, including ***`map`***, ***`filter`***, ***`reduce`***, ***`collect`***, and more. These operations are inspired by functional programming concepts and encourage a declarative style of coding.

##### **Creating Streams:**
You can create streams from various data sources, including:
- **Collections:** You can convert collections such as List, Set, or Map into streams using the ***stream()*** method. For example: <br>
`List<String> names = Arrays.asList("Alice", "Bob", "Charlie");` <br>
`Stream<String> nameStream = names.stream();`

- **Arrays:** You can create streams directly from arrays using the ***Arrays.stream()*** method. For example: <br>
`int[] numbers = {1, 2, 3, 4, 5};` <br>
`IntStream numberStream = Arrays.stream(numbers);`

- **Stream Factories:** Java provides stream factories like ***`Stream.of()`*** and ***`Stream.generate()`*** to create streams from specific elements or by generating elements on-the-fly. For example: <br>
`Stream<String> elements = Stream.of("one", "two", "three");` <br>
`Stream<Integer> generatedStream = Stream.generate(() -> new Random().nextInt(100));`

Now imagine you are developing an e-commerce application, and you have a list of products. You want to find all products in a specific category and generate a report of their names and prices. Here's how you can create Java Streams for this task.

***Note: Create a new file in IntelliJ with name as <u>`ProductReport.java`</u> with following code and execute it***


```scijava
import java.util.*;
import java.util.stream.Collectors;
import java.util.stream.Stream;

// define the Product class
class Product {
    private String name;
    private String category;
    private double price;

    public Product(String name, String category, double price) {
        this.name = name;
        this.category = category;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public String getCategory() {
        return category;
    }

    public double getPrice() {
        return price;
    }
}


// The Product Report class
public class ProductReport {

    public static void main(String[] args) {

        // Sample list of products
        List<Product> products = Arrays.asList(
            new Product("Laptop", "Electronics", 899.99),
            new Product("T-shirt", "Apparel", 19.99),
            new Product("Smartphone", "Electronics", 599.99),
            new Product("Jeans", "Apparel", 49.99),
            new Product("Coffee Maker", "Appliances", 129.99),
            new Product("Headphones", "Electronics", 149.99),
            new Product("Sneakers", "Apparel", 79.99),
            new Product("Toaster", "Appliances", 39.99)
        );

        // Specify the category for the report
        String targetCategory = "Electronics";

        // Create a Stream of products filtered by the target category
        Stream<Product> filteredProducts = products.stream()
            .filter(product -> product.getCategory().equals(targetCategory));

        // Generate a report of product names and prices for the specified category
        List<String> report = filteredProducts
            .map(product -> product.getName() + " - $" + product.getPrice())
            .collect(Collectors.toList());

        // Display the report
        System.out.println("Products in the " + targetCategory + " category:");
        report.forEach(System.out::println);  // Pass the reference for the System.out.println() method
    }
}
```

In this code:
- We define a `Product` class to represent individual products, each with a name, category, and price.
- We create a `list` of sample products (products) that belong to different categories, including "Electronics," "Apparel," and "Appliances."
- We specify the target category for which we want to generate a report (in this case, "Electronics").
- We use Java Streams to filter the products based on the target category and then map the filtered products to their names and prices.
- Finally, we collect the mapped data into a list (report) and display the report, listing the names and prices of products in the "Electronics" category.

This example demonstrates how to create Java Streams to filter and process data based on a real-world use case scenario in an e-commerce application.

**Exercise**

Create a Java Stream from a list of integers and perform the following tasks:
- Filter the even numbers
- Map the remaining numbers to their squares
- Collect the squared numbers into a List
- Print the List fof squared numbers

***Note: Create a new file in IntelliJ with name as <u>`StreamCreationExercise.java`</u> with following code and create your exercise***


```scijava
import java.util.*;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class StreamCreationExercise {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Create a Stream from the list of integers
        Stream<Integer> numberStream = numbers.stream();

        // TO-DO
        // Your code here: Filter even numbers, map to squares, and collect into a List

        // Print the result
        System.out.println(squaredEvenNumbers);
    }
}
```

### **6. Stream Operations** <a id="stream-operations"></a>

Learn about common Stream operations like map, filter, and reduce, along with examples.

##### **Introduction**
Once you have a stream, you can perform various operations on it, categorized as intermediate and terminal operations:
- **Intermediate Operations:** These operations transform a stream into another stream and are often combined to form a processing pipeline. Common intermediate operations include `map`, `filter`, `distinct`, `sorted`, and `limit`. For example: <br>
```
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<String> filteredNames = names.stream()
    .filter(name -> name.length() > 3)
    .map(String::toUpperCase)
    .collect(Collectors.toList());
```

- **Terminal Operations:** These operations produce a result or a side-effect and close the stream. Common terminal operations include `collect`, `forEach`, `reduce`, and `count`. For example: <br>
```
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
long count = names.stream()
    .filter(name -> name.length() > 3)
    .count();
```

##### **Streams are widely used in real-world scenarios**
- **Data Processing:** Streams are invaluable for processing large data sets efficiently. For example, in a financial application, you can use streams to calculate statistics on a large set of financial transactions.
- **Data Transformation:** In a data transformation application, you can use streams to map, filter, and aggregate data into the desired format.
- **Parallel Processing:** Java Streams can be parallelized using the parallelStream() method, allowing you to take advantage of multi-core processors for enhanced performance.
- **Database Queries:** Streams are commonly used in database queries when working with Java Persistence API (JPA) to process query results.
- **File and I/O Handling:** Streams can also be used for reading and writing files, making I/O operations more efficient and concise.

Now imagine you're working on a financial application, and you have a list of financial transactions that you need to process to calculate various statistics. In this example, we'll use Java Streams to filter, map, and aggregate financial transaction data to calculate the total amount of transactions for a specific account.

***Note: Create a new file in IntelliJ with name as <u>`FinancialAnalysis.java`</u> with following code and execute it***


```scijava
import java.util.*;
import java.util.stream.Collectors;

class FinancialTransaction {
    private String accountNumber;
    private double amount;

    public FinancialTransaction(String accountNumber, double amount) {
        this.accountNumber = accountNumber;
        this.amount = amount;
    }

    public String getAccountNumber() {
        return accountNumber;
    }

    public double getAmount() {
        return amount;
    }
}

public class FinancialAnalysis {
    public static void main(String[] args) {
        // Sample financial transactions
        List<FinancialTransaction> transactions = Arrays.asList(
            new FinancialTransaction("A123", 1000.0),
            new FinancialTransaction("B456", 750.0),
            new FinancialTransaction("A123", 500.0),
            new FinancialTransaction("C789", 1200.0),
            new FinancialTransaction("B456", 800.0)
        );

        // Calculate the total amount of transactions for account "A123"
        String targetAccount = "A123";
        double totalAmount = transactions.stream()
            .filter(transaction -> transaction.getAccountNumber().equals(targetAccount))
            .mapToDouble(FinancialTransaction::getAmount)
            .sum();

        System.out.println("Total amount for account " + targetAccount + ": $" + totalAmount);
    }
}
```

**In this example:** <br>
- We define a `FinancialTransaction` class to represent individual financial transactions, each with an account number and an amount.
- We create a list of sample financial transactions (transactions) that include transactions for different accounts.
- Using Java Streams, we filter the transactions for a specific account (in this case, "A123") and then use the `mapToDouble` operation to extract the transaction amounts as primitive double values.
- Finally, we use the `sum` operation to calculate the total amount for the specified account.

When you run this code, it will process the list of transactions and calculate the total amount for the "A123" account, demonstrating how streams can be used to efficiently process financial data and perform calculations in a real-world scenario.

**Exercise**

Given a list of names, perform the following operations using Java Streams:
- Filter out names that contain fewer than 5 characters.
- Convert the remaining names to uppercase.
- Collect the filtered and uppercase names into a new List.
- Find and print the average number of characters per name in the filtered list of remaining names.


```scijava
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

class NameOperations {
    public static void main(String[] args) {
        // Sample list of names
        List<String> names = Arrays.asList("Allison", "Bobby", "Charles", "Davidson", "Eva-Mendez", "Freddy", "Graham");

        // TO-DO (enter your code in place of ....)
        // Create a stream, filter names on length, map them to uppercase, and collect them as a new list
        List<String> filteredAndUppercaseNames = names.stream()
                .... // Filter names with at least 5 characters
                .... // Convert names to uppercase
                .... // Collect into a new List

        System.out.println("Filtered and Uppercase Names: " + filteredAndUppercaseNames);

        // TO-DO
        // Calculate the average number of characters in the filtered list
        double averageLength = filteredAndUppercaseNames.stream()
                .... // Convert names to their lengths
                .... // Calculate the average
                .... // Default to 0.0 if no names match the filter

        System.out.println("Average Number of Characters: " + averageLength);
    }
}

```

### **Conclusion**
In this notebook, we've covered the foundational concepts of functional programming in Java, including Lambda Expressions, Functional Interfaces, and Java Streams. These powerful tools allow developers to write concise and expressive code, making it easier to work with collections and process data in a functional style. By mastering these concepts, Java developers can write more efficient and maintainable code.

Functional programming is an essential skill for modern Java development, and we hope this notebook has provided you with a solid foundation to explore and utilize these concepts in your projects.

Feel free to experiment with the provided exercises and explore more advanced topics in functional programming in Java to further enhance your skills.

**Happy coding!**

---
---


```scijava

```
