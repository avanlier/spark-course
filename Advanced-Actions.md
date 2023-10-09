
# Advanced Actions in Apache Spark

Advanced Actions in Apache Spark are powerful operations that provide insights and approximations about the data in an RDD. These actions are particularly useful when dealing with large datasets. In this document, we will explore various advanced actions and provide examples.

## countApprox Action

The `countApprox` action returns the approximate value of an RDD within a specified time frame, regardless of whether the job has completed or not. The error factor is typically higher when the timeout is shorter.

```java
JavaRDD<Integer> intRDD = sparkContext.parallelize(Arrays.asList(1, 4, 3, 5, 7, 6, 9, 10, 11, 13, 16, 20));
PartialResult<BoundedDouble> countApprox = intRDD.countApprox(2);
System.out.println("Confidence: " + countApprox.getFinalValue().confidence());
System.out.println("High: " + countApprox.getFinalValue().high());
System.out.println("Low: " + countApprox.getFinalValue().low());
System.out.println("Mean: " + countApprox.getFinalValue().mean());
System.out.println("Final: " + countApprox.getFinalValue().toString());
```
## countByKeyApprox Action

The `countByKeyApprox` action is applied to a pair RDD and returns an approximate result within a timeout period. The result is of type `PartialResult` and provides variations such as `high()`, `low()`, `mean()`, and more.

```
JavaPairRDD<String, Integer> pairRDD = ...; // Create a pair RDD
PartialResult<Map<String, BoundedDouble>> countByKeyApprox = pairRDD.countByKeyApprox(1);

for (Entry<String, BoundedDouble> entry : countByKeyApprox.getFinalValue().entrySet()) {
    System.out.println("Confidence for " + entry.getKey() + ": " + entry.getValue().confidence());
    System.out.println("High for " + entry.getKey() + ": " + entry.getValue().high());
    System.out.println("Low for " + entry.getKey() + ": " + entry.getValue().low());
    System.out.println("Mean for " + entry.getKey() + ": " + entry.getValue().mean());
    System.out.println("Final value for " + entry.getKey() + ": " + entry.getValue().toString());
}
```

## countByValueApprox Action

The `countByValueApprox` action is used on a pair RDD to approximate the count of values within a stipulated timeout with considerable accuracy. You can check the accuracy using the helper method `confidence()`.

```
JavaPairRDD<String, Integer> pairRDD = ...; // Create a pair RDD
PartialResult<Map<Tuple2<String, Integer>, BoundedDouble>> countByValueApprox = pairRDD.countByValueApprox(1);

for (Entry<Tuple2<String, Integer>, BoundedDouble> entry : countByValueApprox.getFinalValue().entrySet()) {
    System.out.println("Confidence for key " + entry.getKey()._1() + " and value " + entry.getKey()._2() + ": " + entry.getValue().confidence());
    System.out.println("High for key " + entry.getKey()._1() + " and value " + entry.getKey()._2() + ": " + entry.getValue().high());
    System.out.println("Low for key " + entry.getKey()._1() + " and value " + entry.getKey()._2() + ": " + entry.getValue().low());
    System.out.println("Mean for key " + entry.getKey()._1() + " and value " + entry.getKey()._2() + ": " + entry.getValue().mean());
    System.out.println("Final value for key " + entry.getKey()._1() + " and value " + entry.getKey()._2() + ": " + entry.getValue().toString());
}
```

## countAsync Action

The `countAsync` action returns a `FutureAction` representing the total number of elements in the RDD. The `FutureAction` class provides helper methods such as `isDone()`, `cancel()`, and `get()` for asynchronous processing.

```
JavaRDD<Integer> intRDD = ...; // Create an RDD
JavaFutureAction<Long> intCount = intRDD.countAsync();

System.out.println("The async count for the RDD is: " + intCount);
```

## collectAsync Action

The `collectAsync` action is another asynchronous operation that returns a future for retrieving all elements of an RDD.

```
JavaRDD<Integer> intRDD = ...; // Create an RDD
JavaFutureAction<List<Integer>> intCol = intRDD.collectAsync();

for (Integer val : intCol.get()) {
    System.out.println("Collected value: " + val);
}
```

## takeAsync Action

The `takeAsync` action retrieves the first `n` elements of the RDD in a `FutureAction`.

```
JavaRDD<Integer> intRDD = ...; // Create an RDD
JavaFutureAction<List<Integer>> takeAsync = intRDD.takeAsync(3);

for (Integer val : takeAsync.get()) {
    System.out.println("Async value of take: " + val);
}
```
## foreachAsync Action

The `foreachAsync` action applies a function to each element of the RDD asynchronously.

```
JavaRDD<Integer> intRDD = ...; // Create an RDD
intRDD.foreachAsync(new VoidFunction<Integer>() {
    @Override
    public void call(Integer t) throws Exception {
        System.out.println("The value is: " + t);
    }
});
```

## collectPartitions Action

The `collectPartitions` action returns an array containing all the elements in specific partitions of the RDD.

```
JavaRDD<Integer> intRDD = ...; // Create an RDD
List<Integer>[] collectPart = intRDD.collectPartitions(new int[]{1, 2});

for (List<Integer> i : collectPart) {
    for (Integer it : i) {
        System.out.println("Collected value: " + it);
    }
}
```

To practice all the above actions, let us create a Java class “AdvanceActionExamples”, with the below code:

```
public class AdvanceActionExamples {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        System.setProperty("hadoop.home.dir", "E:\\hadoop");
        SparkConf conf = new SparkConf().setMaster("local").setAppName("ActionExamples").set("spark.hadoop.validateOutputSpecs", "false").set("spark.scheduler.mode", "FAIR");
        JavaSparkContext sparkContext = new JavaSparkContext(conf);
        Logger rootLogger = LogManager.getRootLogger();
        rootLogger.setLevel(Level.WARN);
        // countApprox(long timeout) 
        JavaRDD < Integer > intRDD = sparkContext.parallelize(Arrays.asList(1, 4, 3, 5, 7, 6, 9, 10, 11, 13, 16, 20));
        PartialResult < BoundedDouble > countAprx = intRDD.countApprox(2);
        System.out.println("Confidence::" + countAprx.getFinalValue().confidence());
        System.out.println("high::" + countAprx.getFinalValue().high());
        System.out.println("Low::" + countAprx.getFinalValue().low());
        System.out.println("Mean::" + countAprx.getFinalValue().mean());
        System.out.println("Final::" + countAprx.getFinalValue().toString());
        //countApprox(long timeout, double confidence) 
        PartialResult < BoundedDouble > countAprox = intRDD.countApprox(1, 0.95);
        System.out.println("Confidence::" + countAprox.getFinalValue().confidence());
        System.out.println("high::" + countAprox.getFinalValue().high());
        System.out.println("Low::" + countAprox.getFinalValue().low());
        System.out.println("Mean::" + countAprox.getFinalValue().mean());
        System.out.println("Final::" + countAprox.getFinalValue().toString());
        List < Tuple2 < String, Integer >> list = new ArrayList < Tuple2 < String, Integer >> ();
        list.add(new Tuple2 < String, Integer > ("a", 1));
        list.add(new Tuple2 < String, Integer > ("b", 2));
        list.add(new Tuple2 < String, Integer > ("c", 3));
        list.add(new Tuple2 < String, Integer > ("a", 4));
        JavaPairRDD < String, Integer > pairRDD = sparkContext.parallelizePairs(list);
        // countByKeyApprox(long timeout); 
        PartialResult < Map < String, BoundedDouble >> countByKeyApprx = pairRDD.countByKeyApprox(1);
        for (Entry < String, BoundedDouble > entrySet: countByKeyApprx.getFinalValue().entrySet()) {
            System.out.println("Confidence for " + entrySet.getKey() + " ::" + entrySet.getValue().confidence());
            System.out.println("high for " + entrySet.getKey() + " ::" + entrySet.getValue().high());
            System.out.println("Low for " + entrySet.getKey() + " ::" + entrySet.getValue().low());
            System.out.println("Mean for " + entrySet.getKey() + " ::" + entrySet.getValue().mean());
            System.out.println("Final val for " + entrySet.getKey() + " ::" + entrySet.getValue().toString());
        }
        //countByKeyApprox(long timeout, double confidence) 
        PartialResult < Map < String, BoundedDouble >> countByKeyApprox = pairRDD.countByKeyApprox(1, 0.75);
        for (Entry < String, BoundedDouble > entrySet: countByKeyApprox.getFinalValue().entrySet()) {
            System.out.println("Confidence for " + entrySet.getKey() + " ::" + entrySet.getValue().confidence());
            System.out.println("high for " + entrySet.getKey() + " ::" + entrySet.getValue().high());
            System.out.println("Low for " + entrySet.getKey() + " ::" + entrySet.getValue().low());
            System.out.println("Mean for " + entrySet.getKey() + " ::" + entrySet.getValue().mean());
            System.out.println("Final val for " + entrySet.getKey() + " ::" + entrySet.getValue().toString());
        }
        // countByKeyApprox(long timeout); 
        PartialResult < Map < Tuple2 < String, Integer > , BoundedDouble >> countByValueApprx = pairRDD.countByValueApprox(1);
        for (Entry < Tuple2 < String, Integer > , BoundedDouble > entrySet: countByValueApprx.getFinalValue().entrySet()) {
            System.out.println("Confidence for key " + entrySet.getKey()._1() + " and value " + entrySet.getKey()._2() + " ::" + entrySet.getValue().confidence());
            System.out.println("high for key " + entrySet.getKey()._1() + " and value " + entrySet.getKey()._2() + " ::" + entrySet.getValue().high());
            System.out.println("Low for key " + entrySet.getKey()._1() + " and value " + entrySet.getKey()._2() + " ::" + entrySet.getValue().low());
            System.out.println("Mean for key " + entrySet.getKey()._1() + " and value " + entrySet.getKey()._2() + " ::" + entrySet.getValue().mean());
            System.out.println("Final val for key " + entrySet.getKey()._1() + " and value " + entrySet.getKey()._2() + " ::" + entrySet.getValue().toString());
        }
        // countByKeyApprox(long timeout, double confidence) 
        PartialResult < Map < Tuple2 < String, Integer > , BoundedDouble >> countByValueApprox = pairRDD.countByValueApprox(1, 0.85);
        for (Entry < Tuple2 < String, Integer > , BoundedDouble > entrySet: countByValueApprox.getFinalValue().entrySet()) {
            System.out.println("Confidence for key " + entrySet.getKey()._1() + " and value " + entrySet.getKey()._2() + " ::" + entrySet.getValue().confidence());
            System.out.println("high for key " + entrySet.getKey()._1() + " and value " + entrySet.getKey()._2() + " ::" + entrySet.getValue().high());
            System.out.println("Low for key " + entrySet.getKey()._1() + " and value " + entrySet.getKey()._2() + " ::" + entrySet.getValue().low());
            System.out.println("Mean for key " + entrySet.getKey()._1() + " and value " + entrySet.getKey()._2() + " ::" + entrySet.getValue().mean());
            System.out.println("Final val for key " + entrySet.getKey()._1() + " and value " + entrySet.getKey()._2() + " ::" + entrySet.getValue().toString());
        }
        long countApprxDistinct = intRDD.countApproxDistinct(0.95);
        System.out.println("The approximate distinct element count is ::" + countApprxDistinct);
        JavaPairRDD < String, Long > approxCountOfKey = pairRDD.countApproxDistinctByKey(0.80);
        approxCountOfKey.foreach(new VoidFunction < Tuple2 < String, Long >> () {
            @Override
            public void call(Tuple2 < String, Long > tuple) throws Exception {
                System.out.println("The approximate distinct vlaues for Key :" + tuple._1() + " is ::" + tuple._2());
            }
        });
        JavaRDD < Integer > intRDD1 = sparkContext.parallelize(Arrays.asList(1, 4, 3, 5, 7, 6, 9, 10, 11, 13, 16, 20), 4);
        JavaRDD < Integer > intRDD2 = sparkContext.parallelize(Arrays.asList(31, 34, 33, 35, 37, 36, 39, 310, 311, 313, 316, 320), 4);
        JavaFutureAction < Long > intCount = intRDD1.countAsync();
        System.out.println(" The async count for " + intCount);
        JavaFutureAction < List < Integer >> intCol = intRDD2.collectAsync();
        for (Integer val: intCol.get()) {
            System.out.println("The collect val is " + val);
        }
        JavaFutureAction < List < Integer >> takeAsync = intRDD.takeAsync(3);
        for (Integer val: takeAsync.get()) {
            System.out.println(" The async value of take is :: " + val);
        }
        intRDD.foreachAsync(new VoidFunction < Integer > () {
            @Override
            public void call(Integer t) throws Exception {
                System.out.println("The val is :" + t);
            }
        });
        intRDD2.foreachAsync(new VoidFunction < Integer > () {
            @Override
            public void call(Integer t) throws Exception {
                System.out.println("the val2 is :" + t);
            }
        });
        List < Integer > lookupVal = pairRDD.lookup("a");
        for (Integer val: lookupVal) {
            System.out.println("The lookup val is ::" + val);
        }
        int numberOfPartitions = intRDD2.getNumPartitions();
        System.out.println("The no of partitions in the RDD are ::" + numberOfPartitions);
        List < Partition > partitions = intRDD1.partitions();
        for (Partition part: partitions) {
            System.out.println(part.toString());
            System.out.println(part.index());
        }
        List < Integer > [] collectPart = intRDD1.collectPartitions(new int[] {
            1,
            2
        });
        System.out.println("The length of collectPart is " + collectPart.length);
        for (List < Integer > i: collectPart) {
            for (Integer it: i) {
                System.out.println(" The val of collect is " + it);
            }
        }
        System.out.println(" The no of partitions are ::" + intRDD1.getNumPartitions());
    }
}
```
## Conclusion

Advanced actions in Apache Spark allow you to gain insights into your data with the flexibility of handling large datasets efficiently.