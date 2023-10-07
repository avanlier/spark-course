### Introduction

In Java, every application starts with a class, and this class must match the filename. In this quickstart guide, we will create our first Java file, MyClass.java, which will contain a "Hello World" message. This is a simple yet essential step to get started with Java programming.

### Creating Your First Java File

1.  **Choose a Text Editor**: You can use any text editor to create your Java file. Popular options include Notepad (on Windows), Visual Studio Code, or any code editor of your choice.
    
2.  **Write the Java Code**: Open your text editor and create a new file named `MyClass.java`. In this file, you'll write the following Java code:
    
    ```
    public class MyClass {
        public static void main(String[] args) {
            System.out.println("Hello World!");
        }
    }
    ```    
    Here's what this code does:
    
    -   `public class MyClass`: This line defines a class named `MyClass`. In Java, classes should always start with an uppercase letter.
        
    -   `public static void main(String[] args)`: This line defines the `main` method, which is the entry point of your Java program. It takes an array of strings (`String[] args`) as its parameter. We'll explain this in more detail shortly.
        
    -   `System.out.println("Hello World!");`: This line uses the `println` method from the `System` class to print the "Hello World!" message to the console.
        
3.  **Save the File**: Save the file using the class name, `MyClass`, and add ".java" to the end of the filename. So, save it as `MyClass.java`.
    

### Running Your Java Program

To run your Java program, follow these steps:

1.  **Open a Terminal/Command Prompt**: You need to open a terminal or command prompt on your computer.
    
2.  **Navigate to the Directory**: Use the `cd` command to navigate to the directory where your `MyClass.java` file is located. For example:
    
```
cd path/to/your/java/file
```
    
Replace `path/to/your/java/file` with the actual path to your file.
    
3.  **Compile the Java File**: To compile your Java file, run the following command:
    
```
javac MyClass.java
```
    
This command tells the Java compiler (`javac`) to compile your `MyClass.java` file. If there are no errors in your code, this command will generate a bytecode file named `MyClass.class`.
    
4.  **Run the Java Program**: After compiling successfully, run your Java program using the following command:
    
```
java MyClass
```
    
You should see the "Hello World!" message printed to the console:
    
```
Hello World!
```
    

### Important Notes:

-   **Java is Case-Sensitive**: Keep in mind that Java is case-sensitive. For example, "MyClass" and "myclass" have different meanings.
    
-   **Matching File Name and Class Name**: The name of the Java file must exactly match the class name defined inside it. In our example, the filename is `MyClass.java`, and the class is `MyClass`.
    
-   **Semicolons**: Each code statement in Java must end with a semicolon (`;`).
    

Congratulations! You've just created and executed your first Java program. You're now ready to explore more complex Java concepts and build powerful applications.