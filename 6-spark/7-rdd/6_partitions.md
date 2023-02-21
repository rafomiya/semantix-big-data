# RDD & Partitions

​	Spark stores the data from RDDs in different partitions. The minimum amount of partitions is 2, and we can define them manually on the reading and reduction of our data.

```python
# defining the RDD
rdd = sc.textFile("entrada*")

# 3 is the number of partitions. in this case, it is ignored.
words = rdd.flatMap(lambda row: row.split(" "), 3)

# 20 is the number of partitions. in this case, it is ignored.
words_1 = rdd.map(lambda word: (word, 1), 20)

# 10 is the number of partitions. in reduces, it is not ignored
words_reduce = words_1.reduceByKey(lambda x, y: x + y, 10)

# creating a new RDD with a new number of partitions
words_repartitioned = words_words_reduce.repartition(5)

# visualizing the amount of partitions of each RDD
print(worsd_reduce.getNumPartitions())  # 10
print(worsd_repartitioned.getNumPartitions())  # 5
```
