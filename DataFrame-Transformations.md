## Overview

In this lab, we will explore the world of DataFrame transformations in Apache Spark. DataFrame transformations are a fundamental part of data processing in Spark, allowing you to manipulate, filter, and transform data to derive insights or prepare it for further analysis. This lab aims to provide you with exposure to the DataFrame API and hands-on experience in using it.

We will cover several common DataFrame transformation techniques to help you understand the core concepts. However, please note that the DataFrame API is extensive, and this lab will not attempt to cover every aspect or illustrate every possible technique. The focus is on building a foundational understanding of DataFrame transformations.

## Lab Duration

The estimated runtime for this lab may vary depending on your familiarity with Spark and the complexity of the transformations you attempt. Plan for at least 30 minutes to an hour to complete the lab.

## Prerequisites

Before starting this lab, ensure that you have the following prerequisites in place:

1.  Apache Spark environment set up and configured.
2.  Basic knowledge of Apache Spark and its concepts.

## Lab Tasks

In this lab, we will perform a series of DataFrame transformations using the Spark shell. The tasks will cover various aspects of DataFrame manipulation. Let's get started with the tasks.

### Assignment:

 - Display the data.Filter on age and display the data.
 - Filter on gender and display the data.
 - Count how many "F" and "M" items there are.
 - [Optional] Find the oldest person with gender "F".
	 - Use SQL to write this query - e.g. spark.sql(" ... ")
	 - Remember to register a temporary table.
	 - Use a subquery to find the maximum age.

### Solution

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class SimpleTransformationsExample {
    public static void main(String[] args) {
        // Create a SparkSession
        SparkSession spark = SparkSession.builder()
                .appName("SimpleTransformationsExample")
                .getOrCreate();

        // Read "people.json" into a DataFrame
        Dataset<Row> folksDF = spark.read().json("data/people.json");

        // Display the data
        folksDF.show();

        // Filter on age and display the data (age > 25)
        folksDF.filter(folksDF.col("age").gt(25)).show();

        // Filter on age and display the data (age > 25 and age < 50)
        folksDF.filter(folksDF.col("age").gt(25).and(folksDF.col("age").lt(50))).show();

        // Filter on gender and display the data (gender = "F")
        folksDF.filter(folksDF.col("gender").equalTo("F")).show();

        // Count how many "F" and "M" items there are
        folksDF.groupBy("gender").count().show();

        // [Optional] Find the oldest person with gender "F"
        folksDF.createOrReplaceTempView("people");
        spark.sql("SELECT name, age FROM people WHERE gender = 'F' AND age = (SELECT MAX(age) FROM people WHERE gender='F')").show();

        // Stop the SparkSession
        spark.stop();
    }
}
```

In this Java code:

-   We create a SparkSession, similar to the Scala code.
-   We read "people.json" into a DataFrame using the `read().json()` method.
-   We perform filtering operations using the `filter()` method, and comparison operations using `.col()` and various conditions.
-   We group data by "gender" and count the occurrences using `groupBy()` and `count()`.
-   For the optional task, we create a temporary view "people" to run a SQL query to find the oldest person with gender "F."
-   Finally, we stop the SparkSession to release resources.

## Working with More Complex Data

**Tasks**

 - Read github.json if you haven't already

	```
	Dataset<Row> githubDF = spark.read().json("data/github.json");
	```

 - Look at the schema and 5 sample rows (limit(5).show) again.
 - Look at the githubDF schema and a few rows (limit().show) again.
 - Select the login value of the actor and display it.
 - Find out how many unique logins there are in the data.
 - Each row in this data, contains a type column. Display all the unique values for the 'type' column.
 - Determine how may rows have a type of CreateEvent


```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class GitHubDataFrameOperations {
    public static void main(String[] args) {
        SparkSession spark = SparkSession.builder()
                .appName("GitHubDataFrameOperations")
                .getOrCreate();

        // Assuming you have already loaded the GitHub DataFrame as 'githubDF'

        // Display the first 5 rows
        githubDF.limit(5).show();

        // Select the 'actor' column and display it with its schema
        githubDF.limit(5).select("actor").show(false);
        githubDF.select("actor").printSchema();

        // Select the 'actor.login' column and display it
        githubDF.select("actor.login").limit(5).show();

        // Find the number of unique logins in the data
        long uniqueLoginsCount = githubDF.select("actor.login").distinct().count();
        System.out.println("Number of unique logins: " + uniqueLoginsCount);

        // Retrieve all unique values for the 'type' column
        githubDF.select("type").distinct().show();

        // Stop the SparkSession
        spark.stop();
    }
}
```

In this Java code:

-   We create a SparkSession and assume that you have already loaded the GitHub DataFrame as `githubDF`.
    
-   We perform operations such as displaying the first 5 rows, selecting columns, printing the schema, finding the number of unique logins, and retrieving unique values for the 'type' column, which are equivalent to the provided Spark DataFrame operations in Scala.
    
-   The results are displayed using `show()` and printed using `System.out.println()` for clarity.
    
-   Finally, we stop the SparkSession to release resources.

## Working with Text Data

**Tasks**

 - Read wiki-pageviews.txt if you haven't already
 - Show 5 rows from this data so you can examine it.

	```
	String  path  =  "<path>/wiki-pageviews.txt"; 
	Dataset<Row> viewsDF = spark.read().text(path);
	viewsDF.limit(5).show();
	```

 - We can see that each row contains a single string.
	 - Unlike JSON data, there is no automatic application of a schema.
	 - This is a cumbersome format to work with, and we'll see ways to transform it into an easier to use format later.

### Summary

We've practiced using some of the common transformations that are available for dataframes. We'll continue using this data to delve into Spark's capabilities.