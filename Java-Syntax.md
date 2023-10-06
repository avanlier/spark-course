**1. The main method**

The `main()` method is an essential component present in every Java program:

```
public  static  void  main(String[] args)
```

Any code enclosed within the `main()` method's block will be executed. You don't need to fully comprehend the keywords preceding and following `main()` immediately; your understanding will develop gradually as you proceed through this tutorial.

For now, remember:

-   Every Java program must have a class name that matches the filename.
-   Each program must include the `main()` method.

**2. System.out.println()**

Within the `main()` method, we utilize the `println()` method to display a line of text on the screen:

`println` is an abbreviation for "print line." Whenever we wish our program to output a message to the screen, we employ `System.out.println()`.

```
public static void main(String[] args) {
  System.out.println("Hello World");
}
```

**3. String[] args**

`String[] args` acts as a receptacle for information we intend to provide to our program.