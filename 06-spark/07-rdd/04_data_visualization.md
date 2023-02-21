# Data Visualization

​	To visualize our data in a RDD, we can use the `collect()` method or simply print them with a `foreach()`:

```scala
words_with_count.foreach(y => println(y._1 + " - " + y._2))
// hadoop - 4
// semantix - 3
// data - 3
// 2019 - 2
// sp - 2
// big - 1
// curso - 1
```

```python
for word, count in words_sorted.collect():
    print(f"{word} - {count}")
```

​	However, keep in mind that the `collect()` is a very expensive operation, since it retrieves all our data to a single of the cluster.

​	To visualize the amount of partitions where the data of a RDD is distributed:

```python
words_sorted.getNumPartitions()
# 3
```
