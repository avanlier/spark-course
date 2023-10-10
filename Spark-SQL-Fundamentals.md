## Introduction

In this lab, we will delve into the fundamental aspects of Spark SQL, a powerful component of Apache Spark that allows you to work with structured data. We will explore how to perform common operations using Spark SQL, such as reading and writing data files in various formats and creating DataFrames. This lab is designed to provide you with a foundational understanding of Spark SQL's capabilities.

## Lab Duration

This lab is expected to take approximately 15-20 minutes to complete.

## Lab Preparation

Before we begin, ensure that you have already loaded the necessary data files. If you haven't done so, please load the required data files for this lab.

## Lab Tasks

In this lab, we will accomplish the following tasks:

1.  **Read Data Files**: We will learn how to use Spark SQL to read data from files in various formats.
    
2.  **Write Data Files**: We will explore how to write data to files in different formats.
    
3.  **Create DataFrames**: We will create DataFrames, a core data structure in Spark SQL, to work with structured data efficiently.
    
**Let's proceed to each task step by step.**

Load data from the following files, if you haven't already

 - `people.json` as JSON
 - `wiki-pageviews.txt` as text
 - `github.json` as JSON

## Loading Data

### Loading Text and JSON Data

#### Reading JSON Data

In this section, we will read JSON data from the `"people.json"` file and display the first 5 rows of the DataFrame.

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class DataLoadingExample {
    public static void main(String[] args) {
        // Create a SparkSession
        SparkSession spark = SparkSession.builder()
                .appName("DataLoadingExample")
                .getOrCreate();

        // Read "people.json" into a DataFrame
        Dataset<Row> folksDF = spark.read().json("data/people.json");

        // Display the first 5 rows of folksDF
        folksDF.limit(5).show();

        // Stop the SparkSession
        spark.stop();
    }
}
```

#### Reading Text Data

Now, we will read text data from the `"wiki-pageviews.txt"` file and display the first 5 rows of the DataFrame.

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class DataLoadingExample {
    public static void main(String[] args) {
        // Create a SparkSession
        SparkSession spark = SparkSession.builder()
                .appName("DataLoadingExample")
                .getOrCreate();

        // Read "wiki-pageviews.txt" into a DataFrame
        Dataset<Row> viewsDF = spark.read().text("data/wiki-pageviews.txt");

        // Display the first 5 rows of viewsDF
        viewsDF.limit(5).show();

        // Stop the SparkSession
        spark.stop();
    }
}
```

### Reading More Complex Data

#### Reading JSON Data

In this section, we will read more complex JSON data from the `"github.json"` file and display the first 5 rows of the DataFrame.

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class DataLoadingExample {
    public static void main(String[] args) {
        // Create a SparkSession
        SparkSession spark = SparkSession.builder()
                .appName("DataLoadingExample")
                .getOrCreate();

        // Read "github.json" into a DataFrame
        Dataset<Row> githubDF = spark.read().json("data/github.json");

        // Display the first 5 rows of githubDF
        githubDF.limit(5).show();

        // Stop the SparkSession
        spark.stop();
    }
}
```

## Writing Data

### Writing Data as Parquet

In this section, we will write the "folksDF" DataFrame as a Parquet file.

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class DataLoadingExample {
    public static void main(String[] args) {
        // Create a SparkSession
        SparkSession spark = SparkSession.builder()
                .appName("DataLoadingExample")
                .getOrCreate();

        // Assuming folksDF is already defined and contains data

        // Write out folksDF as a Parquet file
        folksDF.write().parquet("data/people.parquet");

        // Stop the SparkSession
        spark.stop();
    }
}
```

### Writing Data as CSV

In this section, we will write the "folksDF" DataFrame as a CSV file.

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class DataLoadingExample {
    public static void main(String[] args) {
        // Create a SparkSession
        SparkSession spark = SparkSession.builder()
                .appName("DataLoadingExample")
                .getOrCreate();

        // Assuming folksDF is already defined and contains data

        // Write out folksDF as a CSV file with headers
        folksDF.coalesce(1).write().option("header", true).csv("data/people.csv");

        // Stop the SparkSession
        spark.stop();
    }
}
```

## Conclusion

This Java code demonstrates how to load and manipulate data using Apache Spark. You can adapt these examples to read and write data in various formats and perform more complex data processing tasks in your Spark applications.