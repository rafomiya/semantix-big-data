# Shared Variables

- When a function is passed to Spark, the operation is executed on a remote cluster node.
    - it works in separate copies of all the variables used on the function.
    - the variables are copied to each machine, and no updates to the variables are propagated back to the driver.
    - the read/write between tasks is inneficient.
- Spark provides two types of shared variables:
    - Broadcast
    - Accumulators

## Broadcast

- Each machine on the cluster will have a variable only for readings in cache.
    - It isn't necessary to create a copy for the tasks.

- Use it when:
    - tasks in different stages use the same data.
    - it is important to store the data in cache in a desserialized way.

```python
sc.broadcast(m)
```

### Methods

- `id`: unique identifier of the broadcast.
- `value`: self explanatory.
- `unpersist`: deletes asynchronously the copies in cache of the broadcast variable on the executors.
- `destroy`: deletes all the data and metadata related to the broadcast variable.
- `toString`: string representation of the variable.

```python
broadcast_var = sc.broadcast([1, 2, 3])

type(broadcast_var)
# output:
# pyspark.broadcast.Broadcast

broadcast_var.value
# output:
# [1, 2, 3]

broadcast_var.destroy()
```

## Accumulators

- Accumulators are variables that are only "added" to a associative and comutative operation.
    - efficient parallelism.
    - can be used to implement counters.
    - supports accumulators of numeric types.
- Spark shows the value of each accumulator modified by a task on the tab "Tasks".
- In Java and Scala, it is possible to see the tracking of accumulators through the GUI.

### Methods

​	Scala:

```scala
// syntax:
sc.longAccumulator(value, accum_name)
sc.doubleAccumulator(value, accum_name)

// example:
val accum = sc.longAccumulator(0, "myAccum")
sc.parallelize(Array(1, 2, 3, 4)).foreach(x => accum.add(x))

accum.value
// output:
// 10
```

​	Python: note that it isn't possible to give a name to the accumulator:

```python
# syntax:
sc.Accumulator(value)

# example:
accum = sc.Accumulator(0)
sc.parallelize([1, 2, 3, 4]).foreach(lambda x: accum.add(x))

accum.value
# output:
# 10
```

## Cache

​	Another important thing is to know how to cache and uncache tables:

​	Cache:

```python
spark.catalog.cacheTable(table_name)
# or with rdd, dataframe or dataset:
df.cache()
```

​	Uncache:

```python
spark.catalog.uncacheTable(table_name)
```
