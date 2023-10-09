# Basic dataframe with AWS S3 

## Objective

The objective of this lab is to demonstrate how to read data from an Amazon S3 bucket in CSV format using Apache Spark and then write the processed data back to the S3 bucket in CSV format.

```java
package com.sparkTutorial.awss3;  
  
import org.apache.spark.SparkConf;  
import org.apache.spark.api.java.JavaSparkContext;  
import org.apache.spark.sql.Dataset;  
import org.apache.spark.sql.Row;  
import org.apache.spark.sql.SparkSession;  
import org.apache.spark.sql.SaveMode;  
  
public class S3CSVReadWrite {  
  
    public static void main(String[] args) {  
        // Initialize Spark  
  SparkConf conf = new SparkConf()  
                .setAppName("S3CSVReadWrite")  
                .setMaster("local[*]"); // You can change this to a cluster URL if needed  
  
  
  JavaSparkContext sc = new JavaSparkContext(conf);  
  SparkSession spark = SparkSession.builder()  
                .appName("S3CSVReadWrite")  
                .getOrCreate();  
  
  // S3 Configuration  
  String awsAccessKeyId = "AKIA3OHF7P5GHWXPXB74";  
  String awsSecretAccessKey = "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";  
  String s3Bucket = "demo0123";  
  String s3Key = "costs.csv";  
  
  // Set AWS credentials  
  spark.sparkContext().hadoopConfiguration().set("fs.s3a.access.key", awsAccessKeyId);  
  spark.sparkContext().hadoopConfiguration().set("fs.s3a.secret.key", awsSecretAccessKey);  
  spark.sparkContext().hadoopConfiguration().set("spark.hadoop.fs.s3a.impl", "org.apache.hadoop.fs.s3a.S3AFileSystem"); // Add this line  
  spark.sparkContext().hadoopConfiguration().set("spark.hadoop.fs.s3a.aws.credentials.provider", "org.apache.hadoop.fs.s3a.SimpleAWSCredentialsProvider");  
  spark.sparkContext().hadoopConfiguration().set("fs.s3a.endpoint", "s3.amazonaws.com");  
  // Read CSV from S3 into DataFrame  
  String s3Path = "s3a://" + s3Bucket + "/" + s3Key;  
  Dataset<Row> df = spark.read()  
                .option("header", "true")  
                .option("inferSchema", "true")  
                .csv(s3Path);  
  
  // Show DataFrame contents  
  df.show();  
  
  // Perform operations on the DataFrame here...  
  
 // Write DataFrame back to S3 as CSV  String outputS3Key = "file.csv";  
  df.write()  
                .mode(SaveMode.Overwrite) // Change this mode as needed  
  .option("header", "true")  
                .csv("s3a://" + s3Bucket + "/" + outputS3Key);  
  
  // Stop SparkContext  
  spark.stop();  
  }  
}
```

## Prerequisites

Before you begin, make sure you have the following prerequisites in place:

1.  An Amazon Web Services (AWS) account with appropriate permissions.
2.  AWS Access Key ID and AWS Secret Access Key with access to the S3 bucket.
3.  Apache Maven installed for managing dependencies.
4.  Apache Spark and Hadoop installed and configured on your local machine.

## Setup

1.  Create a new Maven project or use an existing one.
2.  Add the following dependencies to your project's `pom.xml` file:

```
<dependencies>
    <dependency>
        <groupId>com.amazonaws</groupId>
        <artifactId>aws-java-sdk</artifactId>
        <version>1.12.563</version>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-aws</artifactId>
        <version>3.3.1</version>
    </dependency>
</dependencies>
```

3.  Create a Java class, e.g., `S3CSVReadWrite`, and copy the provided code into this class.

## Code Explanation

Let's break down the code into sections and explain each part.

### Spark Configuration

```
SparkConf conf = new SparkConf()
        .setAppName("S3CSVReadWrite")
        .setMaster("local[*]");
```
-   This code initializes the SparkConf object, setting the application name to "S3CSVReadWrite" and the master URL to "local[*]" for local execution. You can change the master URL to a cluster URL if needed.

```
JavaSparkContext sc = new JavaSparkContext(conf);
SparkSession spark = SparkSession.builder()
        .appName("S3CSVReadWrite")
        .getOrCreate();
```

-   Here, we create a JavaSparkContext and a SparkSession for working with Spark. The `getOrCreate()` method ensures that if a SparkSession already exists, it will be reused.

### AWS S3 Configuration

```
String awsAccessKeyId = "YOUR_AWS_ACCESS_KEY_ID";
String awsSecretAccessKey = "YOUR_AWS_SECRET_ACCESS_KEY";
String s3Bucket = "demo0123";
String s3Key = "costs.csv";
```
-   Set your AWS access key ID, secret access key, the S3 bucket name, and the S3 key (object) name for the CSV file you want to read.

```
spark.sparkContext().hadoopConfiguration().set("fs.s3a.access.key", awsAccessKeyId);
spark.sparkContext().hadoopConfiguration().set("fs.s3a.secret.key", awsSecretAccessKey);
spark.sparkContext().hadoopConfiguration().set("spark.hadoop.fs.s3a.impl", "org.apache.hadoop.fs.s3a.S3AFileSystem");
spark.sparkContext().hadoopConfiguration().set("spark.hadoop.fs.s3a.aws.credentials.provider", "org.apache.hadoop.fs.s3a.SimpleAWSCredentialsProvider");
spark.sparkContext().hadoopConfiguration().set("fs.s3a.endpoint", "s3.amazonaws.com");
```

-   These lines configure Spark to use the AWS S3A filesystem. Replace `YOUR_AWS_ACCESS_KEY_ID` and `YOUR_AWS_SECRET_ACCESS_KEY` with your AWS credentials.

### Reading CSV from S3

```
String s3Path = "s3a://" + s3Bucket + "/" + s3Key;
Dataset<Row> df = spark.read()
        .option("header", "true")
        .option("inferSchema", "true")
        .csv(s3Path);
```

-   This code reads the CSV file from the specified S3 path into a DataFrame using Spark. It assumes that the first row contains column headers and automatically infers the schema.

### Data Processing (Optional)

You can perform any necessary operations on the DataFrame at this point.

### Writing DataFrame Back to S3

```
String outputS3Key = "file.csv";
df.write()
        .mode(SaveMode.Overwrite)
        .option("header", "true")
        .csv("s3a://" + s3Bucket + "/" + outputS3Key);
```

-   This code writes the DataFrame back to the S3 bucket as a CSV file with the specified `outputS3Key`. You can customize the write mode and options as needed.

### Spark Context Shutdown

```
spark.stop();
```

-   Finally, the SparkContext is stopped to release resources.

## Running the Application

1.  Ensure that you have configured AWS credentials with sufficient permissions.
2.  Build and run the Java application.
3.  The code will read the CSV from S3, display its contents, perform any optional operations, and then write the DataFrame back to S3.

## Conclusion

This lab demonstrates how to read and write CSV data to and from an Amazon S3 bucket using Apache Spark. You can use this as a foundation for more complex data processing tasks involving S3 and Spark.

## Troubleshooting and Additional Notes

### AWS IAM Permissions

-   Ensure that the AWS IAM user or role associated with the provided AWS Access Key ID and Secret Access Key has the necessary permissions to access the specified S3 bucket and perform the required operations.

### Spark Version Compatibility

-   Make sure that the versions of the AWS SDK, Hadoop, and Spark dependencies are compatible with each other. In this example, the versions used are specified in the provided `pom.xml`, but you should verify that they work well together.

### S3 Bucket and Object Names

-   Verify that the S3 bucket name (`s3Bucket`) and object key (`s3Key`) are correct. Ensure that the specified CSV file exists in the bucket.

### Error Handling

-   Add error handling and logging to your code to handle exceptions that may occur during S3 operations, such as network issues or permission problems.

### Spark DataFrame Operations

-   If you need to perform additional operations on the DataFrame, such as filtering, aggregation, or transformation, you can do so between reading from S3 and writing back to S3. Spark provides powerful APIs for data manipulation.

### Data Partitioning

-   For large datasets, consider partitioning the data before writing it back to S3. Partitioning can improve query performance when reading the data later.

### Security Best Practices

-   Never hardcode sensitive AWS credentials directly in your code. Use AWS IAM roles, environment variables, or secure credential management solutions to store and retrieve credentials securely.

### AWS Region

-   Make sure the AWS region is correctly set for your S3 bucket. In this example, the `fs.s3a.endpoint` is set to "s3.amazonaws.com," which is the default for the US East (N. Virginia) region. If your bucket is in a different region, adjust the endpoint accordingly.

### Spark Cluster Deployment

-   If you want to run this code on a Spark cluster, modify the SparkConf to specify the cluster's master URL instead of "local[*]". Ensure that your cluster is properly configured to access AWS resources.

### Code Optimization

-   Depending on your specific use case, you may need to optimize your code for performance, including adjusting Spark configurations, partitioning data, and fine-tuning operations.

By following the steps outlined in this lab document and considering the additional notes and best practices, you can effectively read and write data to and from Amazon S3 using Apache Spark, making it easier to process and analyze large datasets stored in the cloud.