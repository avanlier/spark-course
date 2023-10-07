In Spark, a PairRDD is a specialized RDD where each element is a key-value pair. PairRDDs are commonly used for various operations like aggregations, filtering, and joining data. This documentation provides detailed information on how to create and manipulate PairRDDs in Spark.

**Creating PairRDD from Another RDD**

To create a PairRDD from another RDD, you can follow these steps:

1.  Import the necessary Spark libraries.
2.  Create a `SparkConf` object to configure your Spark application.
3.  Create a `JavaSparkContext` object, which is the entry point for Spark functionality.
4.  Create an RDD of your choice. In this example, we'll create an RDD of String values.
5.  Use the `mapToPair` transformation to convert your RDD into a PairRDD.

```
// Import statements
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaPairRDD;
import org.apache.spark.api.java.JavaSparkContext;
import scala.Tuple2;

public class PairRddFromRegularRdd {
    public static void main(String[] args) throws Exception {
        // Configure Spark
        SparkConf conf = new SparkConf().setAppName("create").setMaster("local[1]");
        JavaSparkContext sc = new JavaSparkContext(conf);

        // Create an RDD from a list of String values
        List<String> inputStrings = Arrays.asList("Lily 23", "Jack 29", "Mary 29", "James 8");
        JavaRDD<String> regularRDD = sc.parallelize(inputStrings);

        // Convert the regularRDD to a PairRDD using mapToPair
        JavaPairRDD<String, Integer> pairRDD = regularRDD.mapToPair(getPairFunction());

        // Save the PairRDD to a text file
        pairRDD.coalesce(1).saveAsTextFile("out/pair_rdd_from_regular_rdd");
    }

    private static PairFunction<String, String, Integer> getPairFunction() {
        return s -> new Tuple2<>(s.split(" ")[0], Integer.valueOf(s.split(" ")[1]));
    }
}
```

**Creating PairRDD from Tuple List**

To create a PairRDD from a list of tuples, you can follow these steps:

1.  Import the necessary Spark libraries.
2.  Create a `SparkConf` object to configure your Spark application.
3.  Create a `JavaSparkContext` object, which is the entry point for Spark functionality.
4.  Create a list of tuples with a key-value structure.
5.  Use the `parallelizePairs` method to convert the list of tuples into a PairRDD.

```
// Import statements
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaPairRDD;
import org.apache.spark.api.java.JavaSparkContext;
import scala.Tuple2;

public class PairRddFromTupleList {
    public static void main(String[] args) throws Exception {
        // Configure Spark
        SparkConf conf = new SparkConf().setAppName("create").setMaster("local[1]");
        JavaSparkContext sc = new JavaSparkContext(conf);

        // Create a list of tuples
        List<Tuple2<String, Integer>> tupleList = Arrays.asList(
            new Tuple2<>("Lily", 23),
            new Tuple2<>("Jack", 29),
            new Tuple2<>("Mary", 29),
            new Tuple2<>("James", 8)
        );

        // Convert the tupleList to a PairRDD using parallelizePairs
        JavaPairRDD<String, Integer> pairRDD = sc.parallelizePairs(tupleList);

        // Save the PairRDD to a text file
        pairRDD.coalesce(1).saveAsTextFile("out/pair_rdd_from_tuple_list");
    }
}
```

**Use Case 11: Airports Not in the USA**

For this use case, you will read airport data from the "in/airports.text" file and generate a PairRDD with airport names as keys and country names as values. Then, you will remove all airports located in the United States and output the resulting PairRDD to "out/airports_not_in_usa_pair_rdd.text". Each row in the input file contains airport information with various columns.

_Sample Output:_

```
("Kamloops", "Canada")
("Wewak Intl", "Papua New Guinea")
```

_Code: Create the Java class "AirportsNotInUsaProblem" in the "com.sparkTutorial.pairRdd.filter" package._

**Use Case 12: Uppercase Country Names**

In this use case, you will read airport data from the "in/airports.text" file, generate a PairRDD with airport names as keys and country names as values, and then convert the country names to uppercase. Finally, you will save the resulting PairRDD to "out/airports_uppercase.text". Each row in the input file contains airport information with various columns.

_Sample Output:_

```
("Kamloops", "CANADA")
("Wewak Intl", "PAPUA NEW GUINEA")
```

_Code: Create the Java class "AirportsUppercaseProblem" in the "com.sparkTutorial.pairRdd.mapValues" package._

**reduceByKey Operation**

When called on a dataset of (K, V) pairs, returns a dataset of (K, V) pairs where the values for each key are aggregated using the given reduce function func, which must be of type (V,V) => V

Reduce by key and reduce operations takes a function and use it to combine values reduce by key runs several parallels reduce operations one for each key in the data set where each operating combines values that have the same key considering input data sets could have a huge number of keys reduced by. We read a couple of lines as an RTD into memory then we use flat map transformation to convert them to separate words in **Use case 3**.

Then we call the by value method to produce a histogram map of number of occurrences for every word.

The problem with this approach is that the count by value is an action operation which will generate a histogram map in the memory of the driver program. However if the data scale is too large the histogram map won't be able to fit into memory.

The rescue is used to reduce by key operation.

**Use Case 14: Word Count with reduceByKey**

In this use case, you will count the number of words using the `reduceByKey` operation. You will read text data from the "in/word_count.text" file, split it into words, and then count the occurrences of each word using `reduceByKey`. The results will be printed to the console.

_Code: Create the Java class "WordCount" in the "com.sparkTutorial.pairRdd.aggregation.reducebykey" package._

```
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaPairRDD;
import org.apache.spark.api.java.JavaRDD;
import org.apache.spark.api.java.JavaSparkContext;
import scala.Tuple2;

public class WordCount {
    public static void main(String[] args) throws Exception {
        // Set logging level to ERROR to reduce verbosity
        Logger.getLogger("org").setLevel(Level.ERROR);

        // Create a SparkConf object to configure the Spark application
        SparkConf conf = new SparkConf()
            .setAppName("wordCounts")
            .setMaster("local[3]"); // Using 3 local CPU cores
        JavaSparkContext sc = new JavaSparkContext(conf);

        // Load input text data from the "in/word_count.text" file into an RDD
        JavaRDD<String> lines = sc.textFile("in/word_count.text");

        // Split each line into words and flatten them
        JavaRDD<String> words = lines.flatMap(line -> Arrays.asList(line.split(" ")).iterator());

        // Map each word to a (word, 1) key-value pair
        JavaPairRDD<String, Integer> wordPairRdd = words.mapToPair(word -> new Tuple2<>(word, 1));

        // Reduce by key to count the occurrences of each word
        JavaPairRDD<String, Integer> wordCounts = wordPairRdd.reduceByKey((x, y) -> x + y);

        // Collect the results into a map
        Map<String, Integer> wordCountsMap = wordCounts.collectAsMap();

        // Print word counts
        for (Map.Entry<String, Integer> wordCountPair : wordCountsMap.entrySet()) {
            System.out.println(wordCountPair.getKey() + " : " + wordCountPair.getValue());
        }

        // Stop the Spark context to release resources
        sc.stop();
    }
}
```

**Use Case 15: Average House Price by Bedroom Count**

Create a Spark program as “AverageHousePriceProblem” in the package “com.sparkTutorial.pairRdd.aggregation.reducebykey.housePrice” to read the house data from in/RealEstate.csv, output the average price for houses with different number of bedrooms. The houses dataset contains a collection of recent real estate listings in San Luis Obispo county and around it.

The dataset contains the following fields:

1. MLS: Multiple listing service number for the house (unique ID).

2. Location: city/town where the house is located. Most locations are in San Luis Obispo county and northern Santa Barbara county (Santa MariaOrcutt, Lompoc, Guadelupe, Los Alamos), but there some out of area locations as well.

3. Price: the most recent listing price of the house (in dollars).

4. Bedrooms: number of bedrooms.

5. Bathrooms: number of bathrooms.

6. Size: size of the house in square feet.

7. Price/SQ.ft: price of the house per square foot.

8. Status: type of sale. The types are represented in the dataset: Short Sale, Foreclosure and Regular.

Each field is comma separated.
_Sample Output:_

```
(3, 325000)
(1, 266356)
(2, 325000)
...
```

> Note: 3, 1 and 2 mean the number of bedrooms. 325000 means the average
> price of houses with 3 bedrooms is 325000.

_Code: Create the Java class "AverageHousePriceProblem" in the "com.sparkTutorial.pairRdd.aggregation.reducebykey.housePrice" package._

**countByKey**

Only available on RDDs of type (K, V). Returns a hashmap of (K, Int) pairs with the count of each key.

**groupByKey Operation**

When called on a dataset of (K, V) pairs, returns a dataset of (K, Iterable<V>) pairs.

Let us create a Java class as GroupByKeyVsReduceByKey to count the number of words using groupByKey in the package “com.sparkTutorial.pairRdd.groupbykey”

```
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaPairRDD;
import org.apache.spark.api.java.JavaSparkContext;
import org.apache.log4j.Level;
import org.apache.log4j.Logger;
import scala.Tuple2;
import com.google.common.collect.Iterables;

import java.util.Arrays;
import java.util.List;

public class GroupByKeyVsReduceByKey {
    public static void main(String[] args) throws Exception {
        // Set the log level to ERROR to reduce console output
        Logger.getLogger("org").setLevel(Level.ERROR);

        // Configure Spark
        SparkConf conf = new SparkConf()
                .setAppName("GroupByKeyVsReduceByKey")
                .setMaster("local[*]");
        
        // Create a SparkContext
        JavaSparkContext sc = new JavaSparkContext(conf);

        // Input data: a list of words
        List<String> words = Arrays.asList("one", "two", "two", "three", "three", "three");

        // Create a PairRDD where each word is paired with the value 1
        JavaPairRDD<String, Integer> wordsPairRdd = sc.parallelize(words)
                .mapToPair(word -> new Tuple2<>(word, 1));

        // Using reduceByKey to count word occurrences
        List<Tuple2<String, Integer>> wordCountsWithReduceByKey = wordsPairRdd
                .reduceByKey((x, y) -> x + y)
                .collect();

        // Using groupByKey to count word occurrences
        List<Tuple2<String, Integer>> wordCountsWithGroupByKey = wordsPairRdd
                .groupByKey()
                .mapValues(intIterable -> Iterables.size(intIterable))
                .collect();

        // Print the results
        System.out.println("Word Counts with reduceByKey: " + wordCountsWithReduceByKey);
        System.out.println("Word Counts with groupByKey: " + wordCountsWithGroupByKey);

        // Stop the SparkContext
        sc.stop();
    }
}
```

**Use Case 16: Airports Grouped by Country**

Create a Spark program as AirportsByCountryProblem in the package “com.sparkTutorial.pairRdd.groupbykey” to read the airport data from in/airports.text, output the list of the names of the airports located in each country. Each row of the input file contains the following columns:

Airport ID, Name of airport, Main city served by airport, Country where airport is located, IATA/FAA code, ICAO Code, Latitude, Longitude, Altitude, Timezone, DST, Timezone in Olson format

_Sample Output:_

```
"Canada", ["Bagotville", "Montreal", "Coronation", ...]
"Norway" : ["Vigra", "Andenes", "Alta", "Bomoen", "Bronnoy",..]
"Papua New Guinea", ["Goroka", "Madang", ...]
```

_Code: Create the Java class "AirportsByCountryProblem" in the "com.sparkTutorial.pairRdd.groupbykey" package._

**SortByKey Operation**

The `sortByKey` operation in Spark is used to sort PairRDDs by their keys.

**Use Case 17: Sort House Prices by Bedroom Count**

In an extension of Use Case 15, you can sort the resulting PairRDD by the number of bedrooms to observe how the price changes with an increase in the number of bedrooms.

**Join Operations**

Spark supports various join operations, such as inner join, left outer join, right outer join, and full outer join. These operations combine two PairRDDs based on a common key.

One is the age pair already with the name being the key and the age being the value.

The other one is the address pair with the name being the key and the address being the value as you see. Both are RDDs have John as a common key Tom is present in the one RDD but not in the address RDD James is present in the address RDD but not in the age. Let us try several joins on it and observe the output.

First we create a Java class as JoinOperations in the package “com.sparkTutorial.pairRdd.join”.

**Use Case 18: Joining PairRDDs**

In this use case, you will perform different join operations on two PairRDDs—one with age data and the other with address data. You will use inner join, left outer join, right outer join, and full outer join operations to combine the data and save the results to text files.

```
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaPairRDD;
import org.apache.spark.api.java.JavaSparkContext;
import scala.Tuple2;

public class JoinOperations {
    public static void main(String[] args) throws Exception {
        // Configure Spark
        SparkConf conf = new SparkConf()
            .setAppName("JoinOperations")
            .setMaster("local[1]");
        
        // Create a SparkContext
        JavaSparkContext sc = new JavaSparkContext(conf);

        // Create PairRDD for ages
        JavaPairRDD<String, Integer> ages = sc.parallelizePairs(Arrays.asList(
            new Tuple2<>("Tom", 29),
            new Tuple2<>("John", 22)
        ));

        // Create PairRDD for addresses
        JavaPairRDD<String, String> addresses = sc.parallelizePairs(Arrays.asList(
            new Tuple2<>("James", "USA"),
            new Tuple2<>("John", "UK")
        ));

        // Inner Join: Combine ages and addresses based on common keys
        JavaPairRDD<String, Tuple2<Integer, String>> join = ages.join(addresses);
        join.saveAsTextFile("out/age_address_join.text");

        // Left Outer Join: Include all records from 'ages' and matching records from 'addresses'
        JavaPairRDD<String, Tuple2<Integer, Optional<String>>> leftOuterJoin = ages.leftOuterJoin(addresses);
        leftOuterJoin.saveAsTextFile("out/age_address_left_out_join.text");

        // Right Outer Join: Include all records from 'addresses' and matching records from 'ages'
        JavaPairRDD<String, Tuple2<Optional<Integer>, String>> rightOuterJoin = ages.rightOuterJoin(addresses);
        rightOuterJoin.saveAsTextFile("out/age_address_right_out_join.text");

        // Full Outer Join: Include all records from both 'ages' and 'addresses'
        JavaPairRDD<String, Tuple2<Optional<Integer>, Optional<String>>> fullOuterJoin = ages.fullOuterJoin(addresses);
        fullOuterJoin.saveAsTextFile("out/age_address_full_out_join.text");

        // Stop SparkContext
        sc.stop();
    }
}
```

_Code: Create the Java class "JoinOperations" in the "com.sparkTutorial.pairRdd.join" package._
