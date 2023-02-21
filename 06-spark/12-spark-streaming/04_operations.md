# Spark Streaming Operations

​	The operations available in Spark Streaming are very similar to the ones we already know: transformations and actions. DStreams accepts the same transformations and actions available in RDDs.

​	Examples of transformations:

- `Map`
- `Filter`
- `FlatMap`
- `ReduceByKey`

​	Examples of actions:

- `Count`
- `CountByValue`
- `Reduce`
- `Print`
- `ForeachRDD`

​	Example: saving the words from the stream into the HDFS:

```python
from pyspark.streaming import StreamingContext


ssc = StreamingContext(sc, 2)

readStr = ssc.socketTextStream("localhost", 9999)

words = readStr.flatMap(lambda line: line.split(" "))
words.saveAsTextFiles("hdfs://localhost/line")

ssc.start()
```

## Word count example

​	Code:

```python
from pyspark.streaming import StreamingContext


ssc = StreamingContext(sc, 10)

readStr = ssc.socketTextStream("localhost", 9999)

words_splitted = readStr.flatMap(lambda x: x.split(" "))
words_with_1 = words_splitted.map(lambda x: (x.lower(), 1))
word_count = words_with_1.reduceByKey(lambda x, y: x + y)

word_count.pprint()

ssc.start()
```

​	Input through netcat:

```bash
netcat -lp 9999
# palavra a a a
# yayyy a aa a
# palavra palavra
# abobora abacate
# maça melancia
# abobora abacate
# abobora
# abacate
# melancia
# palavra
# palavra
```

​	Output:

```
-------------------------------------------
Time: 2022-04-22 02:48:40
-------------------------------------------
('a', 5)
('palavra', 3)
('yayyy', 1)
('aa', 1)

-------------------------------------------
Time: 2022-04-22 02:48:50
-------------------------------------------
('maça', 1)
('abacate', 2)
('abobora', 2)
('melancia', 1)

-------------------------------------------
Time: 2022-04-22 02:49:00
-------------------------------------------
('palavra', 2)
('abacate', 1)
('abobora', 1)
('melancia', 1)
```
