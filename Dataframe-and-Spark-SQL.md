## Introduction

Apache Spark is a powerful open-source big data processing framework that provides various APIs for distributed data processing. Two important components of Spark for data manipulation and querying are DataFrames and Spark SQL. DataFrames are distributed collections of data organized into named columns, similar to tables in a relational database, while Spark SQL is a Spark module for structured data processing using SQL queries.

This documentation provides a comprehensive overview of DataFrames and Spark SQL in Apache Spark, along with Java code examples to illustrate their usage.

## Table of Contents

1.  [**Getting Started**](#getting-started)
    
    -   Setting up a Spark Session
    -   Creating DataFrames
2.  [**DataFrames in Spark**](#dataframes-in-spark)
    
    -   Operations on DataFrames
    -   Transformations and Actions
3.  [**Spark SQL**](#spark-sql)
    
    -   Executing SQL Queries
    -   Registering DataFrames as Temporary Tables
    -   Interoperability with DataFrames
4.  [**Examples**](#examples)
    
    -   Practical Java Examples for DataFrames and Spark SQL

## 1. Getting Started

### Setting up a Spark Session

To use DataFrames and Spark SQL in Java, you first need to set up a Spark session. A Spark session is the entry point to using Spark functionality. Here's how to create one:

```
import org.apache.spark.SparkConf;
import org.apache.spark.sql.SparkSession;

public class SparkSessionExample {
    public static void main(String[] args) {
        // Configure Spark
        SparkConf conf = new SparkConf()
                .setAppName("SparkDataFrameExample")
                .setMaster("local[*]");

        // Create a SparkSession
        SparkSession spark = SparkSession.builder()
                .config(conf)
                .getOrCreate();

        // Your Spark code here

        // Stop the SparkSession when done
        spark.stop();
    }
}
```

### Creating DataFrames

You can create DataFrames from various data sources, such as CSV files, Parquet files, JSON files, or by transforming existing data structures. Here's an example of creating a DataFrame from an existing Java list:

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class CreateDataFrameExample {
    public static void main(String[] args) {
        SparkSession spark = SparkSession.builder()
                .appName("CreateDataFrameExample")
                .getOrCreate();

        // Sample data
        List<Row> data = Arrays.asList(
                RowFactory.create(1, "Alice"),
                RowFactory.create(2, "Bob"),
                RowFactory.create(3, "Charlie")
        );

        // Define the schema
        StructType schema = new StructType(new StructField[]{
                new StructField("Id", DataTypes.IntegerType, false, Metadata.empty()),
                new StructField("Name", DataTypes.StringType, false, Metadata.empty())
        });

        // Create a DataFrame
        Dataset<Row> df = spark.createDataFrame(data, schema);

        df.show();
        spark.stop();
    }
}
```

## 2. DataFrames in Spark

### Operations on DataFrames

DataFrames support various operations, including filtering, selecting columns, aggregating data, and more. Here are some common DataFrame operations:

-   **Selecting Columns**:

```
df.select("Name").show();
```

-   **Filtering**:

```
df.filter(col("Age").gt(18)).show();
```

-   **Grouping and Aggregation**:

```
df.groupBy("Department").agg(avg("Salary")).show();
```

-   **Sorting**:

```
df.sort(col("Salary").desc()).show();
```

### Transformations and Actions

DataFrames have two types of operations: transformations and actions. Transformations create a new DataFrame, while actions return results or write data.

-   **Transformations** (e.g., `select`, `filter`, `groupBy`) are lazy and do not execute immediately.
    
-   **Actions** (e.g., `show`, `count`, `write`) trigger the execution of transformations.
    

## 3. Spark SQL

### Executing SQL Queries

Spark SQL allows you to execute SQL queries on DataFrames. To use Spark SQL, you need to register a DataFrame as a temporary table and then execute SQL queries against it:

```
// Register DataFrame as a temporary table
df.createOrReplaceTempView("people");

// Execute SQL query
Dataset<Row> result = spark.sql("SELECT Name, Age FROM people WHERE Age > 18");
result.show();
```

### Registering DataFrames as Temporary Tables

You can register multiple DataFrames as temporary tables and join or query them using SQL:

```
df1.createOrReplaceTempView("table1");
df2.createOrReplaceTempView("table2");

Dataset<Row> result = spark.sql("SELECT * FROM table1 JOIN table2 ON table1.Id = table2.Id");
result.show();
```

### Interoperability with DataFrames

You can seamlessly switch between DataFrames and SQL queries in your Spark code. For example, you can perform transformations on a DataFrame and then use Spark SQL for complex queries.

```
df.filter(col("Age").gt(18)).createOrReplaceTempView("filteredPeople");

Dataset<Row> result = spark.sql("SELECT Name, Age FROM filteredPeople");
result.show();
```

## 4. Java Examples

Here are some practical Java examples that demonstrate the usage of DataFrames and Spark SQL:

-   [**Example 1**: Reading and displaying data from a CSV file](#example-1)
-   [**Example 2**: Aggregating data with Spark SQL](#example-2)
-   [**Example 3**: Joining DataFrames with Spark SQL](#example-3)


### Example 1: Reading and Displaying Data from a CSV File

#### Code Overview

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class CsvDataFrameExample {
    public static void main(String[] args) {
        SparkSession spark = SparkSession.builder()
                .appName("CsvDataFrameExample")
                .getOrCreate();

        // Read data from a CSV file into a DataFrame
        Dataset<Row> df = spark.read()
                .option("header", "true")
                .csv("path/to/your/file.csv");

        // Show the DataFrame
        df.show();

        spark.stop();
    }
}
```

#### Explanation

1.  We start by creating a SparkSession, which is the entry point for Spark functionality. The `.appName("CsvDataFrameExample")` sets the application name, and `.getOrCreate()` ensures that an existing SparkSession is reused or a new one is created.
    
2.  We use `.read()` to read data from a CSV file into a DataFrame. The `.option("header", "true")` specifies that the first row of the CSV file contains the column headers. You should replace `"path/to/your/file.csv"` with the actual path to your CSV file.
    
3.  We call `.show()` to display the contents of the DataFrame.
    
4.  Finally, we stop the SparkSession to release resources.
    

### Java Example 2: Aggregating Data with Spark SQL

#### Code Overview

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class SparkSqlAggregationExample {
    public static void main(String[] args) {
        SparkSession spark = SparkSession.builder()
                .appName("SparkSqlAggregationExample")
                .getOrCreate();

        // Read data from a CSV file into a DataFrame
        Dataset<Row> df = spark.read()
                .option("header", "true")
                .csv("path/to/your/file.csv");

        // Register DataFrame as a temporary table
        df.createOrReplaceTempView("sales");

        // Execute SQL query to calculate total sales by department
        Dataset<Row> result = spark.sql("SELECT Department, SUM(Sales) AS TotalSales FROM sales GROUP BY Department");
        result.show();

        spark.stop();
    }
}
```

#### Explanation

1.  Similar to the previous example, we create a SparkSession and read data from a CSV file into a DataFrame.
    
2.  We register the DataFrame as a temporary table using `.createOrReplaceTempView("sales")`. This step allows us to use Spark SQL to query the DataFrame.
    
3.  We execute an SQL query using `.sql()`. In this example, we calculate the total sales by department using aggregation functions like `SUM`. The result is stored in a new DataFrame called `result`.
    
4.  We call `.show()` to display the result DataFrame, which shows the total sales for each department.
    
5.  Finally, we stop the SparkSession.
    

### Java Example 3: Joining DataFrames with Spark SQL

#### Code Overview

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class SparkSqlJoinExample {
    public static void main(String[] args) {
        SparkSession spark = SparkSession.builder()
                .appName("SparkSqlJoinExample")
                .getOrCreate();

        // Read data from CSV files into DataFrames
        Dataset<Row> ordersDF = spark.read()
                .option("header", "true")
                .csv("path/to/orders.csv");

        Dataset<Row> customersDF = spark.read()
                .option("header", "true")
                .csv("path/to/customers.csv");

        // Register DataFrames as temporary tables
        ordersDF.createOrReplaceTempView("orders");
        customersDF.createOrReplaceTempView("customers");

        // Execute SQL query to join DataFrames
        Dataset<Row> result = spark.sql("SELECT c.CustomerName, o.OrderDate " +
                "FROM customers c JOIN orders o ON c.CustomerID = o.CustomerID " +
                "WHERE o.OrderAmount > 1000");

        result.show();

        spark.stop();
    }
}
```

#### Explanation

1.  Again, we start by creating a SparkSession.
    
2.  We read data from two CSV files, `orders.csv` and `customers.csv`, into separate DataFrames: `ordersDF` and `customersDF`.
    
3.  Both DataFrames are registered as temporary tables, `orders` and `customers`, using `.createOrReplaceTempView()`. This enables us to perform SQL operations on them.
    
4.  We execute an SQL query using `.sql()`. In this example, we join the `customers` and `orders` tables on the `CustomerID` field and select `CustomerName` and `OrderDate`. We also add a filter to select orders with an `OrderAmount` greater than 1000.
    
5.  Finally, we call `.show()` to display the result, which shows customer names and order dates for high-value orders.
    
6.  We stop the SparkSession to release resources.
    

These Java examples demonstrate how to use DataFrames and Spark SQL in Apache Spark for various data processing tasks, including reading, filtering, aggregating, and joining data. The ability to seamlessly switch between DataFrames and Spark SQL queries makes it a powerful tool for data analysis and manipulation in a distributed computing environment.

**There are two methods for creating Spark DataFrames:**

1.  Creating DataFrames from Existing RDDs:
    -   Constructing a Schema Programmatically.
2.  Two Approaches for Defining a Schema:
    -   Defining the Schema Programmatically.

### Defining the Schema Programmatically.

```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;
import org.apache.spark.sql.functions.*;
import org.apache.spark.sql.types.*;

public class BlogData {

    public static void main(String[] args) {
        SparkSession spark = SparkSession.builder()
                .appName("BlogData")
                .getOrCreate();

        // Define schema for our data
        StructType schema = new StructType(new StructField[]{
                new StructField("Id", DataTypes.IntegerType, false, Metadata.empty()),
                new StructField("First", DataTypes.StringType, false, Metadata.empty()),
                new StructField("Last", DataTypes.StringType, false, Metadata.empty()),
                new StructField("Url", DataTypes.StringType, false, Metadata.empty()),
                new StructField("Published", DataTypes.StringType, false, Metadata.empty()),
                new StructField("Hits", DataTypes.IntegerType, false, Metadata.empty()),
                new StructField("Campaigns", new ArrayType(DataTypes.StringType, false), false, Metadata.empty())
        });

        // Create our data
        Row[] data = new Row[]{
                RowFactory.create(1, "Jules", "Damji", "https://tinyurl.1", "1/4/2016", 4535, new String[]{"twitter", "LinkedIn"}),
                RowFactory.create(2, "Brooke", "Wenig", "https://tinyurl.2", "5/5/2018", 8908, new String[]{"twitter", "LinkedIn"}),
                RowFactory.create(3, "Denny", "Lee", "https://tinyurl.3", "6/7/2019", 7659, new String[]{"web", "twitter", "FB", "LinkedIn"}),
                RowFactory.create(4, "Tathagata", "Das", "https://tinyurl.4", "5/12/2018", 10568, new String[]{"twitter", "FB"}),
                RowFactory.create(5, "Matei", "Zaharia", "https://tinyurl.5", "5/14/2014", 40578, new String[]{"web", "twitter", "FB", "LinkedIn"}),
                RowFactory.create(6, "Reynold", "Xin", "https://tinyurl.6", "3/2/2015", 25568, new String[]{"twitter", "LinkedIn"})
        };

        // Create a DataFrame using the defined schema
        Dataset<Row> blogsDF = spark.createDataFrame(Arrays.asList(data), schema);

        // Show the DataFrame
        blogsDF.show();
        System.out.println();

        // Print the DataFrame schema
        blogsDF.printSchema();

        // Show columns and expressions
        blogsDF.select(expr("Hits * 2")).show(2);
        blogsDF.select(col("Hits").multiply(2)).show(2);
        blogsDF.select(expr("Hits * 2")).show(2);

        // Show heavy hitters
        blogsDF.withColumn("Big Hitters", expr("Hits > 10000")).show();

        // Concatenate three columns, create a new column, and show it
        blogsDF.withColumn("AuthorsId", concat(expr("First"), expr("Last"), expr("Id")))
                .select(col("AuthorsId"))
                .show(4);

        // Sort by column "Id" in descending order
        blogsDF.sort(col("Id").desc()).show();

        // Write to Parquet format
        String parquetPath = "<path>";
        blogsDF.write().format("parquet").save(parquetPath);

        // Stop SparkSession
        spark.stop();
    }
}
```


**Note:** the expressions `blogs_df.sort(col("Id").desc)` and `blogsDF.sort($"Id".desc)` are identical. They both sort the DataFrame column named Id in descending order: one uses an explicit function, `col("Id")`, to return a Column object, while the other uses $ before the name of the column, which is a function in Spark that converts column named Id to a Column.

**Assignment 1:** let’s read a large CSV file containing data on San Francisco Fire Department calls. we will define a schema for this file and use the DataFrameReader class and its methods to tell Spark what to do. Because this file contains 28 columns and over 4,380,660 records,2 it’s more efficient to define a schema than have Spark infer it.

**Hint**
```
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;
import org.apache.spark.sql.types.*;

public class SparkDataFrameExample {
    public static void main(String[] args) {
        SparkSession spark = SparkSession.builder()
                .appName("SparkDataFrameExample")
                .getOrCreate();

        // Define the schema programmatically
        StructType fireSchema = DataTypes.createStructType(new StructField[]{
                DataTypes.createStructField("CallNumber", DataTypes.IntegerType, true),
                DataTypes.createStructField("UnitID", DataTypes.StringType, true),
                DataTypes.createStructField("IncidentNumber", DataTypes.IntegerType, true),
                DataTypes.createStructField("CallType", DataTypes.StringType, true),
                DataTypes.createStructField("CallDate", DataTypes.StringType, true),
                DataTypes.createStructField("WatchDate", DataTypes.StringType, true),
                DataTypes.createStructField("CallFinalDisposition", DataTypes.StringType, true),
                DataTypes.createStructField("AvailableDtTm", DataTypes.StringType, true),
                DataTypes.createStructField("Address", DataTypes.StringType, true),
                DataTypes.createStructField("City", DataTypes.StringType, true),
                DataTypes.createStructField("Zipcode", DataTypes.IntegerType, true),
                DataTypes.createStructField("Battalion", DataTypes.StringType, true),
                DataTypes.createStructField("StationArea", DataTypes.StringType, true),
                DataTypes.createStructField("Box", DataTypes.StringType, true),
                DataTypes.createStructField("OriginalPriority", DataTypes.StringType, true),
                DataTypes.createStructField("Priority", DataTypes.StringType, true),
                DataTypes.createStructField("FinalPriority", DataTypes.IntegerType, true),
                DataTypes.createStructField("ALSUnit", DataTypes.BooleanType, true),
                DataTypes.createStructField("CallTypeGroup", DataTypes.StringType, true),
                DataTypes.createStructField("NumAlarms", DataTypes.IntegerType, true),
                DataTypes.createStructField("UnitType", DataTypes.StringType, true),
                DataTypes.createStructField("UnitSequenceInCallDispatch", DataTypes.IntegerType, true),
                DataTypes.createStructField("FirePreventionDistrict", DataTypes.StringType, true),
                DataTypes.createStructField("SupervisorDistrict", DataTypes.StringType, true),
                DataTypes.createStructField("Neighborhood", DataTypes.StringType, true),
                DataTypes.createStructField("Location", DataTypes.StringType, true),
                DataTypes.createStructField("RowID", DataTypes.StringType, true),
                DataTypes.createStructField("Delay", DataTypes.FloatType, true)
        });

        // Read the CSV file into a DataFrame
        String sfFireFile = "/path/sf-fire-calls.csv";
        Dataset<Row> fireDF = spark.read()
                .option("header", "true")
                .schema(fireSchema)
                .csv(sfFireFile);

        // Show the DataFrame
        fireDF.show();

        spark.stop();
    }
}
```


 - What were all the different types of fire calls in 2018?
 - What months within the year 2018 saw the highest number of fire
   calls?
 - Which neighborhood in San Francisco generated the most fire calls
   in 2018?
 - Which neighborhoods had the worst response times to fire calls in
   2018?
 - Which week in the year in 2018 had the most fire calls?   
 - Is there a correlation between neighborhood, zip code, and number
   of fire calls?
 - How can we use Parquet files or SQL tables to store this data and
   read it back?

**Use Case**

let’s look at a collection of readings from Internet of Things (IoT) devices in a JSON file (we use this file in the end-to-end example later in this section).

 - Detect failing devices with battery levels below a threshold.
 - Identify offending countries with high levels of CO2 emissions.
 - Compute the min and max values for temperature, battery level, CO2, and humidity.
 - Sort and group by average temperature, CO2, humidity, and country.