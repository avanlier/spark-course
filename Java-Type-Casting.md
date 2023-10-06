Type casting in Java involves the assignment of a value from one data type to another.

In Java, two main types of casting are prevalent:

-   **Widening Casting** (automatic) - converting a smaller data type into a larger one. `byte` -> `short` -> `char` -> `int` -> `long` -> `float` -> `double`
    
-   **Narrowing Casting** (manual) - converting a larger data type into a smaller one. `double` -> `float` -> `long` -> `int` -> `char` -> `short` -> `byte`
    

### Widening Casting

Widening casting happens automatically when assigning a smaller data type to a larger one:

```
public class MyClass {
  public static void main(String[] args) {
    int myInt = 9;
    double myDouble = myInt; // Automatic casting: int to double

    System.out.println(myInt);      // Outputs 9
    System.out.println(myDouble);   // Outputs 9.0
  }
}
```

### Narrowing Casting

Narrowing casting requires manual intervention by specifying the target data type in parentheses before the value:

```
public class MyClass {
  public static void main(String[] args) {
    double myDouble = 9.78;
    int myInt = (int) myDouble; // Manual casting: double to int

    System.out.println(myDouble);   // Outputs 9.78
    System.out.println(myInt);      // Outputs 9
  }
}
```

This approach enables you to control the conversion from a larger data type to a smaller one when necessary.