### Understanding Java Conditional Statements

Java includes the standard logical conditions inspired by mathematics:

-   Less than: `a < b`
-   Less than or equal to: `a <= b`
-   Greater than: `a > b`
-   Greater than or equal to: `a >= b`
-   Equal to: `a == b`
-   Not Equal to: `a != b`

These conditions allow you to execute different actions based on specific decisions.

In Java, you can work with the following **conditional statements**:

1.  **`if` Statement**: Use `if` to specify a block of code to execute if a given condition is true.
2.  **`else` Statement**: Use `else` to specify a block of code to execute if the same condition is false.
3.  **`else if` Statement**: Use `else if` to define a new condition to test if the initial condition is false.
4.  **`switch` Statement**: Employ `switch` to define multiple alternative blocks of code to execute.

Note: In Java, `if` is case-sensitive, so it must be written in lowercase. Uppercase letters (e.g., If or IF) will result in an error.

**Syntax for `if`, `else if`, and `else` Statements:**

```
if (condition1) {
  // Code block to execute if condition1 is true
} else if (condition2) {
  // Code block to execute if condition1 is false and condition2 is true
} else {
  // Code block to execute if both condition1 and condition2 are false
}
```

Here's an example:

```
int time = 22;

if (time < 10) {
  System.out.println("Good morning.");
} else if (time < 20) {
  System.out.println("Good day.");
} else {
  System.out.println("Good evening.");
}
// Outputs "Good evening."
```

**Shortened Syntax for Ternary Conditionals:**

When you have only one statement to execute for `if` and `else`, you can use a shortened form called the ternary conditional:

```
variable = (condition) ? expressionTrue : expressionFalse;
```

Example:

```
int time = 20;
String result = (time < 18) ? "Good day." : "Good evening.";
System.out.println(result);
```

### Java Switch Statements

The `switch` statement allows you to choose one of several code blocks to execute based on the value of an expression.

**Syntax for `switch` Statement:**

```
```

Here's how it works:

-   The `switch` expression is evaluated once.
-   The expression's value is compared with the values of each `case`.
-   If a match is found, the corresponding code block is executed.
-   The optional `break` keyword is used to exit the `switch` block, preventing further code execution and case testing.

Here's an example that uses the day of the week number to determine the weekday name:

javaCopy code

`int  day  =  4;  switch  (day) {  case  1: System.out.println("Monday");  break;  case  2: System.out.println("Tuesday");  break;  case  3: System.out.println("Wednesday");  break;case  4: System.out.println("Thursday");  break;  case  5: System.out.println("Friday");break;  case  6: System.out.println("Saturday");  break;  case  7: System.out.println("Sunday");  break; }  // Outputs "Thursday" (day 4)`

These conditional statements in Java allow you to control the flow of your programs based on various conditions and inputs.