# Map & FlatMap

​	Continuing the previous example, we will see now two transformations: FlatMap and Map.

## FlatMap

​	FlatMap is a transformation that applies an operation on all the rows of a dataframe, returning the new dataframe. It also flattens the result, meaning the new dataframe will have more rows than the original one.

```python
rdd.take(2)
# ['Big Data', 'Semantix SP']

words = rdd.flatMap(lambda x: x.split())

words.collect()
# ['Big', 'Data', 'Semantix', 'SP']
```

```scala
rdd.take(2)
// res1: Array[String] = Array(Big Data, Semantix SP)

val words = rdd.flatMap(x => x.split(" "))
// or
val words = rdd.flatMap(_.split(" "))

words.foreach(println)
// Big
// Data
// Semantix
// SP
```

## Map

​	Map is a much more simple operation, once it only applies the operation to all the rows of the dataframe, returning a new dataframe with the same amount of rows.

```python
rdd.take(2)
# ['Big Data', 'Semantix SP']

words = rdd.map(lambda x: x.split())

words.collect()
# [['Big', 'Data'], ['Semantix', 'SP']]
```

​	Another example:

```python
wordsLowerWithLength = words \
    .flatMap(lambda x: x.split()) \
    .map(lambda x: x.lower()) \
    .map(lambda x: (x, len(x)))
```
