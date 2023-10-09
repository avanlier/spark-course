# Advanced Transformations in Apache Spark

In Apache Spark, advanced transformations allow you to perform powerful operations on Resilient Distributed Datasets (RDDs). These transformations are essential for various data manipulation tasks. In this document, we'll explore some of these advanced transformations and provide code examples to demonstrate their functionality.

## mapPartitions Transformation

The `mapPartitions` transformation is similar to the standard `map` transformation, but it operates on RDD partitions rather than individual elements. This means that the provided function is executed once per RDD partition. Consequently, there is a one-to-one mapping between partitions of the source RDD and the resulting target RDD. Since each partition is stored as a whole on a node, this transformation does not require shuffling.

In the following code example, we create an RDD of integers and increment all elements of the RDD by 1 using `mapPartitions`.

```java
// JavaRDD<Integer> intRDD = ...;
JavaRDD<Integer> mapPartitions = intRDD.mapPartitions(iterator -> {
    List<Integer> intList = new ArrayList<>();
    while (iterator.hasNext()) {
        intList.add(iterator.next() + 1);
    }
    return intList.iterator();
});
```
## mapPartitionsWithIndex Transformation

The `mapPartitionsWithIndex` transformation is similar to `mapPartitions`, but it provides the partition index as well. This can be useful when you need to associate elements with their respective partitions.

In the following code example, we use `mapPartitionsWithIndex` to identify which elements belong to which partition.

```
// JavaRDD<Integer> intRDD = ...;
intRDD.mapPartitionsWithIndex((index, iterator) -> {
    List<String> list = new ArrayList<>();
    while (iterator.hasNext()) {
        list.add("Element " + iterator.next() + " belongs to partition " + index);
    }
    return list.iterator();
}, false);
```

## mapPartitionsToPair Transformation

The `mapPartitionsToPair` transformation combines the functionality of `mapPartitions` and `mapToPair`. It runs map transformations on every partition of the RDD and returns a `JavaPairRDD` instead of a regular `JavaRDD`.

In the following example, we convert a `JavaPairRDD` of <String, Integer> using `mapPartitionsToPair`.

```
// JavaRDD<Integer> intRDD = ...;
JavaPairRDD<String, Integer> pairRDD = intRDD.mapPartitionsToPair(t -> {
    List<Tuple2<String, Integer>> list = new ArrayList<>();
    while (t.hasNext()) {
        int element = t.next();
        list.add(element % 2 == 0 ? new Tuple2<>("even", element) : new Tuple2<>("odd", element));
    }
    return list.iterator();
});
```

## mapValues Transformation

The `mapValues` transformation is applicable only to pair RDDs. It operates exclusively on the values of the pair RDDs without affecting the keys. This transformation is particularly useful when you want to transform only the values in a pair RDD.

In the code below, we demonstrate how to use `mapValues` to multiply values by 3 in a pair RDD.

```
// JavaPairRDD<String, Integer> pairRDD = ...;
JavaPairRDD<String, Integer> mapValues = pairRDD.mapValues(v1 -> v1 * 3);
```

## flatMapValues Transformation

The `flatMapValues` transformation is similar to `mapValues`, but it applies a `flatMap` function to the values. This is useful when you need to generate multiple output values for each input key.

Consider a pair RDD containing the mapping of months to lists of expenses.

```
// JavaPairRDD<String, String> monExpRDD = ...;
JavaPairRDD<String, Integer> monExpflattened1 = monExpRDD.flatMapValues(v -> Arrays.asList(v.split(",")).stream().map(s -> Integer.parseInt(s)).collect(Collectors.toList()));
```

## repartitionAndSortWithinPartitions Transformation

The `repartitionAndSortWithinPartitions` transformation is an `OrderedRDDFunctions` operation, similar to `sortByKey`. It works on pair RDDs. This transformation first repartitions the pair RDD based on the given partitioner and then sorts each partition by the key of the pair RDD. It requires an instance of a partitioner as an argument.

In the following code, we demonstrate how to use `repartitionAndSortWithinPartitions` to repartition and sort a pair RDD.

```
// JavaPairRDD<String, Integer> monExpflattened1 = ...;
JavaPairRDD<String, Integer> repartitionAndSortWithinPartitions = monExpflattened1.repartitionAndSortWithinPartitions(new HashPartitioner(2));
```
## foldByKey Transformation

The `foldByKey` transformation can be considered similar to `reduceByKey` but with an initial zero value. It employs an associative function to merge values for each key, using the initial zero value.

Example usage of `foldByKey`:

```
// JavaPairRDD<K, V> pairRDD = ...;
pairRDD.foldByKey(0, (v1, v2) -> v1 + v2).collect();
```

## aggregateByKey Transformation

The `aggregateByKey` transformation is similar to `reduceByKey` and `foldByKey` but offers more generalized behavior. It allows you to return a pair RDD with a different value type than the input RDD. This transformation is useful when you need to transform an RDD of type (k1, v1) to (k1, v2), which is not possible with `reduceByKey` or `foldByKey`.

Example usage of `aggregateByKey`:

```
// JavaPairRDD<K, V> pairRDD = ...;
JavaPairRDD<K, V> aggregateByKey = pairRDD.aggregateByKey(
    zeroValue,
    (v1, v2) -> mergeFunction,
    (v1, v2) -> mergeCombinersFunction
);
```

## combineByKey Transformation

The `combineByKey` transformation is the most generalized form, allowing you to combine values of pair RDDs based on keys. It is one step ahead of `aggregateByKey` because it lets you create the initial combiner function as well. The `combineByKey` transformation accepts three parameters:

-   `createCombiner`: A function to create a combiner for a key, i.e., it creates an initial value for a key when it is first encountered in a partition.
-   `mergeValueWithinPartition`: A function that merges the value of a key with its existing combiner value within a partition. This function triggers only when an initial combiner value is created for a key.
-   `mergeCombiners`: A function that takes the combined values for keys created on each partition and merges them to create the final result.

Example usage of `combineByKey`:

```
// JavaPairRDD<K, V> pairRDD = ...;
JavaPairRDD<K, V> combineByKey = pairRDD.combineByKey(
    createCombinerFunction,
    mergeValueWithinPartitionFunction,
    mergeCombinersFunction
);
```

## flatMapToPair Transformation

The `flatMapToPair` transformation applies a `flatMap` function to an RDD of strings, generating key-value pairs.

Example usage of `flatMapToPair`:

```
// JavaRDD<String> stringRDD = ...;
JavaPairRDD<String, Integer> flatMapToPair = stringRDD.flatMapToPair(s -> Arrays.asList(s.split(" ")).stream()
    .map(token -> new Tuple2<>(token, 1))
    .collect(Collectors.toList()).iterator());
```

These advanced transformations are essential tools in Apache Spark for various data processing tasks. By executing the provided code examples, you can observe the effects of each transformation on RDDs and gain a better understanding of their functionality.


Let us create a Java class as “TransformationsDemo” in the package rdd.advancedTransformation”, with the below code.

```
public class TransformationsDemo {
    public static void main(String[] args) {
        SparkSession sparkSession = SparkSession.builder().master("local").appName("My App").getOrCreate();
        JavaSparkContext jsc = new JavaSparkContext(sparkSession.sparkContext());
        JavaRDD < Integer > intRDD = jsc.parallelize(Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10), 2);
        //mapPartitions 
        JavaRDD < Integer > mapPartitions = intRDD.mapPartitions(iterator - > {
            List < Integer > intList = new ArrayList < > ();
            while (iterator.hasNext()) {
                intList.add(iterator.next() + 1);
            }
            return intList.iterator();
        });
        //mapPartitionsWithIndex 
        intRDD.mapPartitionsWithIndex((index, iterator) - > {
            List < String > list = new ArrayList < String > ();
            while (iterator.hasNext()) {
                list.add("Element " + iterator.next() + " belongs to partition " + index);
            }
            return list.iterator();
        }, false);
        //mapPartitionsToPair 
        JavaPairRDD < String, Integer > pairRDD = intRDD.mapPartitionsToPair(t - > {
            List < Tuple2 < String,
            Integer >> list = new ArrayList < > ();
            while (t.hasNext()) {
                int element = t.next();
                list.add(element % 2 == 0 ? new Tuple2 < String, Integer > ("even", element) :
                    new Tuple2 < String, Integer > ("odd", element));
            }
            return list.iterator();
        });
        JavaPairRDD < String, Integer > mapValues = pairRDD.mapValues(v1 - > v1 * 3);
        // System.out.println(mapValues.collect()); 
        // intRDD.mapPartitionsToPair(f) 
        // System.out.println(mapPartitions.toDebugString()); 
        // sort bykey 
        JavaPairRDD < String, String > monExpRDD = jsc
            .parallelizePairs(Arrays.asList(new Tuple2 < String, String > ("Jan", "50,100,214,10"),
                new Tuple2 < String, String > ("Feb", "60,314,223,77")));
        //flatMapValues 
        JavaPairRDD < String, Integer > monExpflattened1 = monExpRDD.flatMapValues(
            v - > Arrays.asList(v.split(",")).stream().map(s - > Integer.parseInt(s)).collect(Collectors.toList()));
        //repartitionAndSortWithinPartitions 
        JavaPairRDD < String, Integer > repartitionAndSortWithinPartitions = monExpflattened1
            .repartitionAndSortWithinPartitions(new HashPartitioner(2));
        JavaPairRDD < Integer, String > unPartitionedRDD = jsc.parallelizePairs(Arrays.asList(new Tuple2 < Integer, String > (8, "h"),
            new Tuple2 < Integer, String > (5, "e"), new Tuple2 < Integer, String > (4, "d"),
            new Tuple2 < Integer, String > (2, "a"), new Tuple2 < Integer, String > (7, "g"),
            new Tuple2 < Integer, String > (6, "f"), new Tuple2 < Integer, String > (1, "a"),
            new Tuple2 < Integer, String > (3, "c"), new Tuple2 < Integer, String > (3, "z")));
        JavaPairRDD < Integer, String > repartitionAndSortWithinPartitions2 = unPartitionedRDD.repartitionAndSortWithinPartitions(new HashPartitioner(3));
        pairRDD.coalesce(2);
        //Our requirement is to find the count of values that start with A per key. 
        JavaPairRDD < String, String > pairRDD3 = jsc.parallelizePairs(Arrays.asList(
            new Tuple2 < String, String > ("key1", "Austria"), new Tuple2 < String, String > ("key2", "Australia"),
            new Tuple2 < String, String > ("key3", "Antartica"), new Tuple2 < String, String > ("key1", "Asia"),
            new Tuple2 < String, String > ("key2", "France"), new Tuple2 < String, String > ("key3", "Canada"),
            new Tuple2 < String, String > ("key1", "Argentina"), new Tuple2 < String, String > ("key2", "American Samoa"),
            new Tuple2 < String, String > ("key3", "Germany")), 1);
        // System.out.println(pairRDD3.getNumPartitions()); 
        //aggregateByKey 
        JavaPairRDD < String, Integer > aggregateByKey = pairRDD3.aggregateByKey(0, (v1, v2) - > {
            System.out.println(v2);
            if (v2.startsWith("A")) {
                v1 += 1;
            }
            return v1;
        }, (v1, v2) - > v1 + v2);
        //combineByKey 
        JavaPairRDD < String, Integer > combineByKey = pairRDD3.combineByKey(v1 - > {
            if (v1.startsWith("A")) {
                return 1;
            } else {
                return 0;
            }
        }, (v1, v2) - > {
            if (v2.startsWith("A")) {
                v1 += 1;
            }
            return v1;
        }, (v1, v2) - > v1 + v2);
        //flatMapToPair 
        JavaRDD < String > stringRDD = jsc.parallelize(Arrays.asList("Hello Spark", "Hello Java"));
        JavaPairRDD < String, Integer > flatMapToPair = stringRDD.flatMapToPair(s - > Arrays.asList(s.split(" ")).stream()
            .map(token - > new Tuple2 < String, Integer > (token, 1)).collect(Collectors.toList())
            .iterator());
        //foldByKey 
        flatMapToPair.foldByKey(0, (v1, v2) - > v1 + v2).collect();
    }
}
```