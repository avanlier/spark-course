In Java, arrays provide a convenient way to store multiple values within a single variable, eliminating the need to declare separate variables for each value. Here, we'll explore the fundamentals of working with arrays.

### Declaring an Array

To declare an array, specify the variable type followed by square brackets:

```
String[] cars;
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
```

### Accessing Array Elements

You access elements within an array by referring to their index number. Remember that Java uses zero-based indexing, where [0] is the first element, [1] is the second, and so on:

```
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
System.out.println(cars[0]); // Outputs Volvo
```

### Modifying Array Elements

To change the value of a specific element, simply reference its index number:

```
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
cars[0] = "Opel";
System.out.println(cars[0]); // Now outputs Opel instead of Volvo
```

### Finding Array Length

To determine the number of elements in an array, use the `length` property:

```
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
System.out.println(cars.length); // Outputs 4
```

### Looping Through an Array

You can iterate through the array elements using a `for` loop, specifying the `length` property to control the loop's execution:

```
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
for (int i = 0; i < cars.length; i++) {
  System.out.println(cars[i]);
}
```
### Enhanced For-Each Loop

Java provides a for-each loop, designed exclusively for iterating through array elements:

```
for (type variable : arrayname) {
  ...
}
```

For instance, you can use it like this:

```
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
for (String car : cars) {
  System.out.println(car);
}
```

The above code reads as follows: for each `String` element (referred to as `car`) in the `cars` array, print out the value of `car`.

### Multidimensional Arrays

A multidimensional array is an array containing one or more arrays. To create a two-dimensional array, enclose each array within its own set of curly braces:

```
int[][] myNumbers = { {1, 2, 3, 4}, {5, 6, 7} };
```

In this example, `myNumbers` is an array containing two arrays as its elements.

To access elements in the `myNumbers` array, specify two indexes: one for the outer array and one for the inner array:

```
int[][] myNumbers = { {1, 2, 3, 4}, {5, 6, 7} };
int x = myNumbers[1][2];
System.out.println(x); // Outputs 7
```

You can also use nested loops to access elements in a two-dimensional array:

```
public class MyClass {
  public static void main(String[] args) {
    int[][] myNumbers = {{1, 2, 3, 4}, {5, 6, 7}};
    for (int i = 0; i < myNumbers.length; ++i) {
      for (int j = 0; j < myNumbers[i].length; ++j) {
        System.out.println(myNumbers[i][j]);
      }
    }
  }
}
```

This code demonstrates a nested loop structure to retrieve elements from a two-dimensional array.