### 1. While Loop

The `while` loop iterates through a code block as long as a specified condition remains `true`:

**Syntax for While Loop:**

```
while (condition) {
  // Code block to be executed
}
```

Example:

```
int i = 0;
while (i < 5) {
  System.out.println(i);
  i++;
}
```

**The Do/While Loop**

The `do/while` loop is a variation of the `while` loop. It executes the code block once before checking the condition. If the condition is true, it continues to execute the loop.

**Syntax for Do/While Loop:**

```
do {
  // Code block to be executed
} while (condition);
```

This loop always executes at least once, even if the condition is initially false.

Example:

```
int i = 0;
do {
  System.out.println(i);
  i++;
} while (i < 5);
```

### 2. For Loop

The `for` loop is used to iterate through a code block a specific number of times.

**Syntax for For Loop:**

```
for (initialization; condition; update) {
  // Code block to be executed
}
```

-   **Initialization**: Executed once before entering the loop.
-   **Condition**: Checked before each iteration; if `true`, the loop continues.
-   **Update**: Executed after each iteration.

Example:

```
for (int i = 0; i < 5; i++) {
  System.out.println(i);
}
```

**For-Each Loop**

The "for-each" loop is designed specifically for iterating through elements in an array or collection.

**Syntax for For-Each Loop:**

```
for (type variable : arrayname) {
  // Code block to be executed
}
```

Example:

```
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
for (String car : cars) {
  System.out.println(car);
}
```

These loop structures provide versatile ways to control the flow of your Java programs, allowing you to execute code repeatedly based on specific conditions or for a predetermined number of iterations.