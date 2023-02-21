# Exercises - RDD Partitions

1. Read the local files of the directory `file:///opt/spark/logs/` as RDD, with 10 partitions.

```python
rdd = sc.textFile("file:///opt/spark/logs", 10)
rdd.getNumPartitions()
# output:
# 10
```

2. Count the amount of appearances of each words of the RDD in 5 partitions.

```python
word_count = rdd.flatMap(lambda x: x.split(" ")).map(lambda x: (x, 1)).reduceByKey(lambda x, y: x + y, 5)
word_count.getNumPartitions()
# output:
# 5
```

3. Save the RDD on the HDFS directory `/user/rafael/logs_count_word_5`

```python
word_count.saveAsTextFile("/user/rafael/logs_count_word_5")
```

4. Redo question 2, with all the transformations on the same line of code.

```python

```

