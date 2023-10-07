### Transformations

#### **filter:** 
To analyze the "airport.text" file, let's create a Java class named "AirportsInUsaProblem" in the "com.sparkTutorial.rdd.airportspackage" package. Our goal is to create a Spark program that reads data from the "airport.text" file, identifies airports located in the United States, and outputs their names and respective cities to a new file named "airports_in_usa.text". The problem statement is as follows:

**Use Case 1:** Create a Spark program to read data from "in/airports.text," identify airports in the United States, and output their names and cities to "out/airports_in_usa.text". Each row in the input file contains the following columns:

-   Airport ID
-   Name of airport
-   Main city served by airport
-   Country where airport is located
-   IATA/FAA code
-   ICAO Code
-   Latitude
-   Longitude
-   Altitude
-   Timezone
-   DST
-   Timezone in Olson format

Sample output: "Putnam County Airport", "Greencastle" "Dowagiac Municipal Airport", "Dowagiac"

Submit the program and observe the output.

#### **map:** 
Let's create a Java class called "AirportsByLatitudeProblem" in the "com.sparkTutorial.rdd.airports" package. We aim to identify airports with latitudes greater than 40 and output the airport names and latitudes to a file.

**Use Case 2:** Create a Spark program to read data from "in/airports.text," identify airports with latitudes greater than 40, and output their names and latitudes to "out/airports_by_latitude.text". Each row in the input file contains the following columns:

-   Airport ID
-   Name of airport
-   Main city served by airport
-   Country where airport is located
-   IATA/FAA code
-   ICAO Code
-   Latitude
-   Longitude
-   Altitude
-   Timezone
-   DST
-   Timezone in Olson format

Sample output: "St Anthony", 51.391944 "Tofino", 49.082222

Submit the program and observe the output.

#### flatMap:
In the package "com.sparkTutorial.rdd," create a Java application named "WordCount." The program should follow these steps:

-   Treat each line as an argument.
-   Split each line by spaces to create an array of words.
-   Convert the array into a list and then into a string iterator.
-   Create a new RDD with each item representing a word from the original input file.
-   Apply a "key by value" operation on the word RDD to count the unique occurrences of words in the input RDD.

**Use Case 3:** Create a Spark program to read data from "in/word_count.text" using the WordCount class. The program should count the unique occurrences of words in the input file and print the word-count pairs to the console.

```
package com.sparkTutorial.rdd;

import org.apache.log4j.Level;
import org.apache.log4j.Logger;
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaRDD;
import org.apache.spark.api.java.JavaSparkContext;
import java.util.Arrays;
import java.util.Map;

public class WordCount {
    public static void main(String[] args) throws Exception {
        Logger.getLogger("org").setLevel(Level.ERROR);
        SparkConf conf = new SparkConf().setAppName("wordCounts").setMaster("local[3]");
        JavaSparkContext sc = new JavaSparkContext(conf);

        JavaRDD<String> lines = sc.textFile("in/word_count.text");
        JavaRDD<String> words = lines.flatMap(line -> Arrays.asList(line.split(" ")).iterator());
        Map<String, Long> wordCounts = words.countByValue();

        for (Map.Entry<String, Long> entry : wordCounts.entrySet()) {
            System.out.println(entry.getKey() + " : " + entry.getValue());
        }
    }
}

```

#### **Union:** 
Let's start by introducing the union operation union operation gives us back an rdd consisting of the data from both input Data sets. This is quite useful in a lot of use cases.

For instance we can use it to aggregate log files from multiple sources. It is worth mentioning that unlike the mathematical union operation if there are any duplicates in the input files the resulting RDD of Spark's union operation will contain duplicates as well.

Let us create Java class in the package “com.sparkTutorial.rdd.nasaApacheWebLogs” as UnionLogProblem

**Use Case 4:**"in/nasa_19950701.tsv" file contains 10000 log lines from one of NASA's apache server for July 1st, 1995. "in/nasa_19950801.tsv" file contains 10000 log lines for August 1st, 1995

Create a Spark program to generate a new RDD which contains the log lines from both July 1st and August 1st, take a 0.1 sample of those log lines and save it to "out/sample_nasa_logs.tsv" file.

Keep in mind, that the original log files contains the following header lines.

 - host 
 - logname 
 - time 
 - method 
 - url 
 - response 
 - bytes

Make sure the head lines are removed in the resulting RDD.

#### intersection

Let us create a Java class in the package “com.sparkTutorial.rdd.nasaApacheWebLogs” as “SameHostsProblem”. Create a Spark program to generate a new RDD which contains the hosts which are accessed on BOTH days. Save the resulting RDD to "out/nasa_logs_same_hosts.csv" file.

**Use Case 5:** Each step of the solution:

Initialize our spark conf and spark context object.

load the two log files as 2 String RDDs.

Since we are only interested in the host name, so we do a map transformation on both input RDDs, split the original log lines using tab as the delimiter, then we return the first column which is the host name.

Do an intersection operation on the two host names RDDs which should return us the common host names between the two RDDs.

Remove the header line.

Save the resulting RDD to a file.

#### collect

**Use case 6:** Let us create a Java class as CollectExample in the package “com.sparkTutorial.rdd.collect”, as below

```
import org.apache.log4j.Level;
import org.apache.log4j.Logger;
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaRDD;
import org.apache.spark.api.java.JavaSparkContext;
import java.util.Arrays;
import java.util.List;

public class CollectExample {
    public static void main(String[] args) {
        // Set the log level to ERROR to reduce verbosity
        Logger.getLogger("org").setLevel(Level.ERROR);
        
        // Configure Spark
        SparkConf conf = new SparkConf()
            .setAppName("CollectExample")
            .setMaster("local[*]");  // Using all available CPU cores
        
        // Initialize SparkContext
        JavaSparkContext sc = new JavaSparkContext(conf);
        
        // Input data: a list of words
        List<String> inputWords = Arrays.asList(
            "spark", "hadoop", "spark", "hive", "pig", "cassandra", "hadoop"
        );
        
        // Create an RDD (Resilient Distributed Dataset) from the list of words
        JavaRDD<String> wordRdd = sc.parallelize(inputWords);
        
        // Collect RDD elements into a list
        List<String> words = wordRdd.collect();
        
        // Iterate over the collected words and print them
        for (String word : words) {
            System.out.println(word);
        }
        
        // Stop the SparkContext when done
        sc.stop();
    }
}
```

#### countByValue

Refer to Use case 3.

#### take

Return an array with the first n elements of the dataset.

This operation can be very useful if it would like to take a piece of the data for unit tests and quick debugging.

You can just take let's say the first three rows of the RDD and print them out to the console take return and elements from the RDD and it'll try to reduce the number of partitions it accesses. So it is possible that the take operation could end up giving us back a biased collection and it doesn't necessary return the elements in the order we might expect.

**Use Case 7:** Let us create a Java class as TakeExample in “com.sparkTutorial.rdd.take” package.

```
import org.apache.log4j.Level;
import org.apache.log4j.Logger;
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaRDD;
import org.apache.spark.api.java.JavaSparkContext;
import java.util.Arrays;
import java.util.List;

public class TakeExample {
    public static void main(String[] args) throws Exception {
        // Set the log level to OFF
        Logger.getLogger("org").setLevel(Level.OFF);

        // Configure Spark
        SparkConf conf = new SparkConf().setAppName("take").setMaster("local[*]");
        JavaSparkContext sc = new JavaSparkContext(conf);

        // Input data
        List<String> inputWords = Arrays.asList("spark", "hadoop", "spark", "hive", "pig", "cassandra", "hadoop");

        // Create an RDD from the input data
        JavaRDD<String> wordRdd = sc.parallelize(inputWords);

        // Take the first 3 elements from the RDD
        List<String> words = wordRdd.take(3);

        // Print the taken words
        for (String word : words) {
            System.out.println(word);
        }

        // Stop the SparkContext
        sc.stop();
    }
}
```

#### reduce

Let us create a Java class as ReduceExample in the package “com.sparkTutorial.rdd.reduce”, with the below mentioned code:

Use Case 8:

```
import org.apache.log4j.Level;
import org.apache.log4j.Logger;
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaRDD;
import org.apache.spark.api.java.JavaSparkContext;
import java.util.Arrays;
import java.util.List;

public class ReduceExample {

    public static void main(String[] args) throws Exception {
        // Disable logging for org.apache package
        Logger.getLogger("org").setLevel(Level.OFF);

        // Set up Spark configuration
        SparkConf conf = new SparkConf()
                .setAppName("reduce")
                .setMaster("local[*]");

        // Create a SparkContext
        JavaSparkContext sc = new JavaSparkContext(conf);

        // Input data: a list of integers
        List<Integer> inputIntegers = Arrays.asList(1, 2, 3, 4, 5);

        // Create an RDD from the list
        JavaRDD<Integer> integerRdd = sc.parallelize(inputIntegers);

        // Use the reduce operation to compute the product of all integers
        Integer product = integerRdd.reduce((x, y) -> x * y);

        // Print the result
        System.out.println("Product is: " + product);

        // Close the SparkContext
        sc.close();
    }
}
```

Execute the code and observe the output.

**Use Case 9:** Create a Spark program to read the first 100 prime numbers from in/prime_nums.text, print the sum of those numbers to console.

Each row of the input file contains 10 prime numbers separated by spaces.

#### cache and persistence

The cache( ) method is a shorthand for using the default storage level, which is StorageLevel.MEMORY_ONLY (store deserialized objects in memory)

Let us create Java class as PersistExample in the package “com.sparkTutorial.rdd.persist” which will persist the intermediate results in the memory space.

**Use Case 10:**

```
import org.apache.log4j.Level;
import org.apache.log4j.Logger;
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaRDD;
import org.apache.spark.api.java.JavaSparkContext;
import org.apache.spark.storage.StorageLevel;
import java.util.Arrays;
import java.util.List;

public class PersistExample {

    public static void main(String[] args) throws Exception {
        // Set log level to ERROR
        Logger.getLogger("org").setLevel(Level.ERROR);

        // Configure Spark
        SparkConf conf = new SparkConf()
                .setAppName("persistExample")
                .setMaster("local[*]");

        // Create a SparkContext
        JavaSparkContext sc = new JavaSparkContext(conf);

        // Define a list of input integers
        List<Integer> inputIntegers = Arrays.asList(1, 2, 3, 4, 5);

        // Create an RDD from the input list
        JavaRDD<Integer> integerRdd = sc.parallelize(inputIntegers);

        // Persist the RDD in memory
        integerRdd.persist(StorageLevel.MEMORY_ONLY());

        // Reduce operation to compute the product
        Integer product = integerRdd.reduce((x, y) -> x * y);

        // Count the number of elements in the RDD
        long count = integerRdd.count();

        // Print the product and count
        System.out.println("Product is: " + product);
        System.out.println("Count of elements is: " + count);

        // Stop the SparkContext
        sc.stop();
    }
}
```