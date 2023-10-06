In Java, variables come in different types, each serving a specific purpose:

-   **String** - Stores text, like "Hello." Strings are enclosed in double quotes.
-   **int** - Holds integers (whole numbers) without decimal points, such as 123 or -123.
-   **float** - Represents floating-point numbers with decimals, like 19.99 or -19.99.
-   **char** - Contains single characters, such as 'a' or 'B'. Characters are enclosed in single quotes.
-   **boolean** - Stores values with two states: true or false.

### 1. Declaring (Creating) Variables

To create a variable, you need to specify its type and assign a value to it:

> _type variable_name = value_;

For instance:

```
String name = "Jesse Shao";
System.out.println(name);
```

You can also declare a variable first and then assign it a value:

```
int myNum;
myNum = 15;
System.out.println(myNum);
```

Here are other types of variables:

```
int myNum = 11;
float myFloatNum = 6.66f;
char myLetter = 'C';
boolean myBool = true;
String myText = "Yooooooooo~";
```
### 2. Displaying Variables

The `println()` method is commonly used to display variables.

To combine text and a variable, use the `+` character:

```
String name = "Jesse";
System.out.println("What's up " + name + "!");
```

You can also add variables to one another:

```
String firstName = "Jesse";
String lastName = "Shao";
String fullName = firstName + lastName;
System.out.println(fullName);
```
For numeric values, the `+` character serves as a mathematical operator (note that we use int variables here):

```
int x = 5;
int y = 6;
System.out.println(x + y); // Prints the result of x + y
```

### 3. Declaring Multiple Variables

When declaring multiple variables of the same type, you can use a comma-separated list:

```
int x = 5, y = 6, z = 55;
System.out.println(x + y + z);
```

### 4. Java Identifiers

In Java, all variables must have unique names known as **identifiers**.

Identifiers can be concise (e.g., x and y) or more descriptive (e.g., age, sum, totalVolume).

Here are the general rules for naming variables (identifiers):

-   Identifiers can include letters, digits, underscores, and dollar signs.
-   They should commence with a letter.
-   Although you can start with $ and _ (not recommended), we avoid this in this tutorial.
-   Identifiers are case-sensitive (e.g., "myVar" and "myvar" are distinct variables).
-   They must start with a lowercase letter and have no spaces.
-   Reserved words like Java keywords (`int`, `String`, etc.) cannot be used as identifiers.