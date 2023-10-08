# Introduction to IntelliJ IDEA

IntelliJ IDEA is a popular Integrated Development Environment (IDE) for Java developers. It provides a feature-rich and user-friendly environment for writing, debugging, and managing Java applications. In this training, we'll explore the essential features of IntelliJ IDEA and learn how to use it effectively for Java development.

# Key Features of IntelliJ IDEA

-   Code assistance and intelligent code completion
    
-   Powerful code navigation and search tools
    
-   Built-in version control integration (Git, SVN, etc.)
    
-   Extensive support for testing frameworks (JUnit, TestNG, etc.)
    
-   Seamless integration with popular build tools (Maven, Gradle)
    
-   Comprehensive debugging capabilities
    
-   Refactoring tools for code optimization
    
-   Support for various Java frameworks and libraries
    

# Let’s get Started

## Installing and Launching IntelliJ IDEA

Before we dive into IntelliJ IDEA, make sure you have it installed on your system. You can download IntelliJ IDEA from the [official website](https://www.jetbrains.com/idea/download/).

After installation, launch IntelliJ IDEA, and you'll be greeted with the welcome screen. Here are a few essential elements to get started:

-   Create New Project: Start a new Java project or open an existing one
    
-   Open Project: Open an existing project from your file system
    
-   Configure: Customize your IDE settings and plugins
    
-   Get from Version Control: Clone a project from a version control system (e.g., Git)
    

## Creating First Project

Let's create a new Java project:

-   Click on "New Project" on the welcome screen
	    

	![](https://lh3.googleusercontent.com/BrOiv-ZM76_axWo8IkzJCETYyQJN0MyLouS7wKKPlmvLrBlM5cM8tz87Vgwa-unshDYcMabyHw1iPw6lDjn0FcwH9I7BBCvp40SyhEj9XrhZqKoIXHSbXXjfQz2-WORGuJoeOrZZbJCflstopdKTqu0)

-   Choose "Java" from the list of project templates
    
-   Configure the project settings:
    

-   Project Name: Give your project a meaningful name (for instance; CalculatorProject )
    
-   Project Location: Choose where to save your project files
    
-   Project SDK: Select your Java Development Kit (JDK) version
    

-   Click "Create" to create the project
	    

	![](https://lh6.googleusercontent.com/hWTCu3bSk2aP5y9E514GfA4En7C6zkksq-1w-WDCgCFHNbcGcsfLsNgntodb1Gsg7vl327YgQS5V8D25CqeXbodORoiWWk-jlso98S2Pr0U_IniyOQBLi3_a6EHbtWz-u53_gnf8GosPBlKMDtQs_Ds)

## Writing and Running Java Code

Now that we have our project set up, let's create a simple Java class and run it:

### Creating a Java Class

-   In the Project Explorer, right-click on the "src" folder
    
-   Select "New > Java Class”
    
	
	![](https://lh5.googleusercontent.com/KedK5EZ_0x2TS1VtVYCIkB9NXwCoxGHOi86QpiwrxiuqowxV8cV-IzczbNCLgX9mJ5pXfca-EYkg2mBrxFsdbEY4dSCi9gBsm7909UjCcx8MJ-kioRT4Gff-8CQtn88BPxT1tidcv7t8ONEhRdZT7cc)

-   Enter a class name (e.g., "Calculator")
    
-   Click "OK" to create the class
    

### Writing Java Code

In the Calculator class, write the following Java code:

```
public  class  Calculator {  
public  static  int  add(int a, int b) {  
return a + b;  
}  
public  static  int  subtract(int a, int b) {  
return a - b;  
}  
public  static  void  main(String[] args) {  
int num1 = 10;  
int num2 = 5;  
  
int sum = add(num1, num2);  
int difference = subtract(num1, num2);  
  
System.out.println("Sum: " + sum);  
System.out.println("Difference: " + difference);  
}}
```
### Running the Java Code

-   To run your code, right-click within the main method in the Calculator class and select "Run 'Calculator.main()'”
    
	
	![](https://lh3.googleusercontent.com/uquSULTli6sBj1w5lOKsAxLcmSgYoBqnEIGtCpyWlvBZf6pjtje4Q3SwyR9py-qVlEklQlhmtnmzeyFuS9ovC2OxsMAusL0fT4Smib2RKu7TUBLYespcO0txy1aCR_FpgbfMbdFCEhsR7r8eqrQ1XGE)

-   You should see the output in the "Run" tool window at the bottom of the IDE. The output will display the sum and difference of num1 and num2
	    

	![](https://lh5.googleusercontent.com/Z0E2aHWfZwiKI5-WAsa2S1E4dhTOQYXPiOWMZtaUcSATbrNqFWqbwzUmtaPDm2JSP5EMRNZo4hzlXx5ssiYjNyD8TdkxKoVsGcY-XjYLMwgAwgieaWmhsgyqNVbMSTZHOUQK-lBgLAS64O_z9LuWjWU)

## Debugging Your Code

IntelliJ IDEA provides robust debugging tools to help you identify and fix issues in your code. Now, let's debug the Calculator class:

-   Place breakpoints in your code by clicking in the gutter next to the line numbers. You can place breakpoints on lines like int sum = add(num1, num2); and int difference = subtract(num1, num2);
    
	
	![](https://lh6.googleusercontent.com/yQ8Elkx2OgSkI8KREfK56qdDOcX6ru15K-ctcIimgwdRhPqmUdYQTai58kbzidq9cuVGkQD24NT-NUns3fxD0UYYfME1NJZ2eNxGX7BxWDBXGZ-v0d7AJgScknk4Gh5FTNDebQ_JDLE5d0VEJ-HK8SY)

-   Click the "Debug" button or right-click within the main method and select "Debug 'Calculator.main()'"
    
	
	![](https://lh6.googleusercontent.com/q3xhmdgCnTklT0Tbwwgg8KNsMPnZvx2Z2G9sjYtqt0gvkdp9PepA7NzT3LOcA-I-xRRHQuKVl6Yg3vHT_3i4yWfuTR_-3yfJPBDZaomd_2ah-Qfz7n--fqIfgDHPLLB0GQJ2nDHnm4PEP3E9XHn220E)

-   The debugger will stop at the breakpoints you set. You can use the debugger controls to navigate through your code and inspect variable values
    
-   For example, you can hover over variables like num1, num2, sum, and difference to see their values
    
-   You can also add watches and evaluate expressions in the "Debug" tool window
    
	
	![](https://lh5.googleusercontent.com/nRRn0qpc3SolUs2KEYB0SveHjI9bC5Jl5TWdp1APtSGnA612P_fE9rejb0FeATIsYVj6LmAzK5xV1JC-yUfXiO3BPVESTFUvXFwL44-2Bzn5HOLjNIEBP7GHtFU24luUICOEG_Lpws7Aoh8AAj5_Z0s)

-   To continue debugging, use the controls like "Step Over", "Step Into", and "Resume Program"
    
	
	![](https://lh6.googleusercontent.com/qDAi7ekHsAO936ZmXeOsu3bu_2UIfVVPeu05pgg3kiezqqEnDnk1rsigOrCJWaRRNyKFEwJa1B15ZJ1H5g-8M-cUspIZhlGmMgB_sbD1uhANWTwS9vgxTRF4XZC-HCFQg-ANH9pXLN8x2ut_0z7cqbA)

-   Fix any issues in your code and continue debugging until your code behaves as expected.
    

This example demonstrates how to write, run, and debug Java code in IntelliJ IDEA using the Calculator class. You can apply these debugging techniques to your own projects to identify and resolve issues effectively.

## Working with Packages and Classes

In this step, we'll create a simple Java package, create classes within that package, and demonstrate how to work with packages and classes in IntelliJ IDEA.

### Creating a Java Package

-   In the Project Explorer (left sidebar), right-click on the "src" folder
    
-   Select "New > Package"
    
	
	![](https://lh5.googleusercontent.com/LfBCXYEBiV4hc6L4vpOI8hQT02ESJQ8bYK1oG9ymggs0EG0bbQAuI68Hz75w0YWLBg9d8PrexcKeDK2qC7pYWgq9jfVyQrki5H7u7JPoDUWdYqvBtP6y-tNVv99SLwxom-12zLb3fCSdyRe2IroKwOk)

-   Enter a package name, for example, "com.myapp.util" (You can use any name you prefer)
    
-   Click "OK" to create the package
    

### Creating Java Classes

Now, let's create two Java classes within the package:

  

Class: MathUtil.java

-   Right-click on the newly created package (e.g., "com.myapp.util")
    
-   Select "New > Java Class"
    
	
	![](https://lh4.googleusercontent.com/qp-wpNymmmGXHn83iiApbsHZatlRBJSHMOp8vH-cC_kqKsSz5KZgvB9g2qaI27WRHg7-yxlifDBmmxBLrlES8i1sIvPcocCAX4coui0yINEKkD_FPiNTfOC794AqfXqmNGVXozbvjTXqOE9XBoe2YH0)

-   Enter the class name as "MathUtil" and click "OK"
    
-   In the MathUtil class, write the following code:
	    
	```	
	package com.myapp.util;  
	public  class  MathUtil {  
	public  static  int  add(int a, int b) {  
	return a + b;  
	}  
	public  static  int  subtract(int a, int b) {  
	return a - b;  
	}  
	}
	```
  

Class: ``MainApp.java``

-   Right-click on the same package (e.g., "com.myapp.util").
    
-   Select "New > Java Class"
    
	
	![](https://lh5.googleusercontent.com/u7PklV__J8aebKl-H0-65JZ5ypJikAPq26A6vsv3GJCtklZmfD2mUZgx85oE0d-9rjhGMtX9MxC5j_0-lDN9Ji9c0YFkh0TzX2ffJ_qOLitQ_j6BPGArnCSNG6HyJw43ZyKzgHRnzvODS3gagLcdS64)

-   Enter the class name as "MainApp" and click "OK"
    
-   In the MainApp class, write the following code:
	    
	```
	package com.myapp.util;  
	public  class  MainApp {  
	public  static  void  main(String[] args) {  
	int num1 = 20;  
	int num2 = 10;  
	int sum = MathUtil.add(num1, num2);  
	int difference = MathUtil.subtract(num1, num2);  
	System.out.println("Sum: " + sum);  
	System.out.println("Difference: " + difference);  
	}  
	}
	```
	  

### Using Classes in Different Packages

Notice that we have created classes in the "com.myapp.util" package. To use these classes from another package, you need to import them. IntelliJ IDEA makes this process seamless:

-   In the MainApp class, IntelliJ IDEA will automatically suggest adding the required import statements. If not, you can manually add them at the top of the MainApp.java file:
	    
	```
	import  com.myapp.util.MathUtil;
	```
-   Now, you can use the MathUtil class in your MainApp class.
    
	
	![](https://lh5.googleusercontent.com/dnaKm1ImKLk6cxWOScEzLhnpEWhoIdBgREIWM-ry7drtjx6V4-4KKbPdrdAtjXyg0j-WUrriMtY15KcTtfzvk_LgCGquvMRV24c6YwenpBXSXLTxBr1GdxhPD9xlMyPeBWJbTojUMVvOHcK8pDajjJE)

### Running the Application

To run the application:

-   Right-click within the main method in the MainApp class.
    
-   Select "Run 'MainApp.main()'"
    
	
	![](https://lh5.googleusercontent.com/d_bwYeZZDSw4_KI7K1oXPFojzL3HVyQLICr3q9OLSlEbsXcKp_WdmLfpevKkGYJ9k2fvbp8QOk2-1kNIIcRCL7bh9Jk6wvUPug1C3XNB-PiDzXD3BpM7g4CP6tLUlpaH0q77WIT1ZirK36Jgq3ZfGmY)

-   You should see the output in the "Run" tool window at the bottom of the IDE. It will display the sum and difference of num1 and num2.
    
	
	![](https://lh6.googleusercontent.com/IQ7ao1JyFJHGE7lgG9tfiUiI51Lh9RRIeux-a2Kf7Deoe-QckNcV8PGn2cOt5MG1jO_pZk7vNdltuD9wM8RxNpmgbXkQpWYXwPjCvFXVkIzn6hgu-sTakIDjaY5VGo5Cnizdg9aV7Pu8nk832wFPl14)

This example demonstrates how to work with packages and classes in IntelliJ IDEA, including creating packages, classes, and importing classes from different packages.

# Conclusion

IntelliJ IDEA is a powerful and versatile IDE that provides excellent support for Java development. In this training, we covered the basics of creating projects, writing and debugging code, organizing classes, building and running projects, and using Git for version control. As you explore more features, you'll find that IntelliJ IDEA enhances your productivity and helps you write high-quality Java applications. Happy coding!