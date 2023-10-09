ETL pipelines need robust solutions to handle corrupt data. This is because data corruption scales as the size of data and the complexity of the data application grow. Corrupt data includes:

-   Missing information
    
-   Incomplete information
    
-   Schema mismatch
    
-   Differing formats or data types
    
-   User errors when writing data producers
    

Since ETL pipelines are built to be automated, production-oriented solutions must ensure pipelines behave as expected. This means that data engineers must both expect and systematically handle corrupt records.

In the roadmap for ETL, this is the Handle Corrupt Records step: 

![](https://lh5.googleusercontent.com/HS1mS61hoeRvRAo7WtYLzUUfYQwptJLdQZICUm_Sn0JC7v7AmugfIrT7h5iojirMy9bba5GtMrX0h5QXf58RdaSfuOEv66Zt7-Hu82OWUtZfSIqPkCnc67tba8R0oZfMGokvJfLHy32mGyziBl2esw)

# ![Spark Logo Tiny](https://lh6.googleusercontent.com/id0_H3kTgy0eP-_JJV0oUtRY0vebI6Usb3tLix3-mBuvJu_ayRfE4H3_Dhpl1eg8EmeyC1XNATXg__W-JcONUz06C6qGI1P16Zz_ihBHLBc9Lm8fd3Ua3dIt6TFQ7SpgX6PBZjvhT0R_bRJ5yETNvQ) In this Exercise you:

-   Examine the 3 ways Spark allows you to handle corrupt data
    

Implementation Steps are as below -

Initialize SparkSession and JavaSparkContext:
```
public static void main(String[] args) throws AnalysisException {
    // Initialize SparkSession
    SparkSession spark = SparkSession.builder()
            .appName("CorruptRecordHandling")
            .master("local[*]")
            .getOrCreate();

    // Initialize JavaSparkContext (if needed)
    JavaSparkContext sc = new JavaSparkContext(spark.sparkContext());
```
  
Run the following cell, which contains a corrupt record, {"a": 1, "b, "c":10}:

**Note:** This is not the preferred way to make a DataFrame. This code allows us to mimic a corrupt record you might see in production.

```
String str = "{\"a\": 1, \"b\":2, \"c\":3}@{\"a\": 1, \"b\":2, \"c\":3}@{\"a\": 1, \"b, \"c\":10}";  
  
// String str = "{\"a\":\"1\",\"b\":\"2\",\"c\":\"3\"}";  
String[] arrOfStr = str.split("@");  
  
// convert the Array to List  
  
Dataset<Row> corruptDF = spark.read().option("mode", "PERMISSIVE")  
.option("columnNameOfCorruptRecord", "_corrupt_record").json(sc.parallelize(Arrays.asList(arrOfStr)));  
  
corruptDF.show();
```

![](https://lh5.googleusercontent.com/B5Si2X4IkztizRutc1qdS47rLhZMKjFCDmY3NP4-BJNASXa19fow0fpjjkaWUfR_Oj-B29s0RSM_msJMIq-A8vjJl3nLw-L4vb3p4hJuNcnInAbF6qTXGtHGNSVpQqQivbmFhrkVJuNw1p89Rownug)

In the previous results, Spark parsed the corrupt record into its own column and processed the other records as expected. This is the default behavior for corrupt records, so you didn't technically need to use the two options mode and columnNameOfCorruptRecord.

There are three different options for handling corrupt records [set through the ParseMode option](https://github.com/apache/spark/blob/master/sql/catalyst/src/main/scala/org/apache/spark/sql/catalyst/util/ParseMode.scala#L34):

| **ParseMode** | **Behavior** |
|--|--|
|ParseMode  | Includes corrupt records in a "_corrupt_record" column (by default) |
|DROPMALFORMED  | Ignores all corrupted records |
|FAILFAST  | Throws an exception when it meets corrupted records |

  

The following cell acts on the same data but drops corrupt records:

```
String str1 = "{'a': 1, 'b':2, 'c':3}@{'a': 1, 'b':2, 'c':3}@{'a': 1, 'b, 'c':10}";  
String[] arrOfStr1 = str1.split("@");  
  
Dataset<Row> corruptDF1 = spark.read().option("mode", "DROPMALFORMED")  
.json(sc.parallelize(Arrays.asList(arrOfStr1)));  
  
corruptDF1.show();
```

![](https://lh5.googleusercontent.com/5N6fDmd7MyH08Rzmr0OynCmpu7XzldipGXQNIv6yAoekK551JDqOuyi6Nd4uuE8gLeRAsi8qjrW-IjvdlOygeMhCrUh7yK9f8P3ktmaXzoUvpKrTXY9LRT9UUl_ZB1M6tlfFa30O47bDMezBdO5nXg)

The following cell throws an error once a corrupt record is found, rather than ignoring or saving the corrupt records:
```
String str2 = "{'a': 1, 'b':2, 'c':3}@{'a': 1, 'b':2, 'c':3}@{'a': 1, 'b, 'c':10}";  
String[] arrOfStr2 = str2.split("@");  
  
Dataset<Row> corruptDF3 = spark.read()  
.option("mode", "FAILFAST")  
.json(sc.parallelize(Arrays.asList(arrOfStr2)));  
  
corruptDF3.show();
```

Full code

```
package com.sparkTutorial;  
  
import java.util.ArrayList;  
import java.util.Arrays;  
import java.util.List;  
  
import org.apache.log4j.Logger;  
import org.apache.spark.SparkConf;  
import org.apache.spark.api.java.JavaSparkContext;  
import org.apache.spark.sql.AnalysisException;  
import org.apache.spark.sql.Dataset;  
import org.apache.spark.sql.Row;  
import org.apache.spark.sql.SparkSession;  
  
public class CorruptRecordHandling {  
  
    static Logger log = Logger.getLogger(CorruptRecordHandling.class);  
  
  @SuppressWarnings("deprecation")  
    public static void main(String[] args) throws AnalysisException {  
  
        // Initialize SparkSession  
  SparkSession spark = SparkSession.builder()  
                .appName("CorruptRecordHandling")  
                .master("local[*]")  
                .getOrCreate();  
  
  // Initialize JavaSparkContext (if needed)  
  JavaSparkContext sc = new JavaSparkContext(spark.sparkContext());  
  
  String str = "{\"a\": 1, \"b\":2, \"c\":3}@{\"a\": 1, \"b\":2, \"c\":3}@{\"a\": 1, \"b, \"c\":10}";  
  
  // String str = "{\"a\":\"1\",\"b\":\"2\",\"c\":\"3\"}";  
  String[] arrOfStr = str.split("@");  
  
  System.out.println(arrOfStr.length);  
  
  // convert the Array to List  
  
  Dataset<Row> corruptDF = spark.read().option("mode", "PERMISSIVE")  
                .option("columnNameOfCorruptRecord", "_corrupt_record").json(sc.parallelize(Arrays.asList(arrOfStr)));  
  
  corruptDF.show();  
  
  String str1 = "{'a': 1, 'b':2, 'c':3}@{'a': 1, 'b':2, 'c':3}@{'a': 1, 'b, 'c':10}";  
  String[] arrOfStr1 = str1.split("@");  
  
  Dataset<Row> corruptDF1 = spark.read().option("mode", "DROPMALFORMED")  
                .json(sc.parallelize(Arrays.asList(arrOfStr1)));  
  
  corruptDF1.show();  
  
  }  
  
    public static <T> List<T> convertArrayToList(T array[]) {  
        // Create an empty List  
  List<T> list = new ArrayList<>();  
  // Iterate through the array  
  for (T t : array) {  
            // Add each element into the list  
  list.add(t);  
  }  
        // Return the converted List  
  return list;  
  }  
}
```

End of Exercise