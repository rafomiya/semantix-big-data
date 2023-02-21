# Sort

​	We can create new dataframes simply altering the order of the rows of an existing dataframe.

```scala
val wordsSorted = words.sortBy(-_._2)
// wordsSorted: org.apache.spark.rdd.RDD[(String, Int)]

wordsSorted.take(4)
// res25: Array[(String, Int)] = Array((hadoop,4), (semantix,3), (data,3), (2019,2))
```

```python
words_sorted = words.sortBy(lambda word: word[1], False)
# or
words_sorted = words.sortBy(lambda word: -word[1])
```
