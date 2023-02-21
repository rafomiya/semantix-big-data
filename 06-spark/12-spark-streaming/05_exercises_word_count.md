# Exercises - Word Count

1. Create the directory `/user/rafael/stream` on the HDFS.

```bash
hdfs dfs -mkdir /user/rafael/stream
```

2. Create an Spark application to count words each 10 seconds on the port 9998 and print on the console during 50 segundos.

```python
# code:

# setting up Spark's variables
from pyspark.streaming import StreamingContext
from time import sleep


conf = SparkConf().setMaster("local[*]").setAppName("word_count")
sc = SparkContext.getOrCreate(conf)
ssc = StreamingContext(sc, 10)

dstream = ssc.socketTextStream("localhost", 9998)

dstream \
    .flatMap(lambda x: x.split(" ")) \
    .map(lambda x: (x.lower(), 1)) \
    .reduceByKey(lambda x, y: x + y) \
    .pprint()

ssc.start()
sleep(50)
ssc.stop()
```

```bash
# input:
netcat -lp 9998
# test_1
# test_2
# TEST_3  
# TEST_2
# teST_1
# avocado apple aVOCaDo
# apPLe aVOcADo
# APPle     
# test
# tEsT
# TEst
# tEST
# 1 2 3
# 3 21
# 3 2 1
# 12
# 21 12
# 12 21
# 21
```

```
# output:
-------------------------------------------
Time: 2022-04-22 03:40:00
-------------------------------------------

-------------------------------------------
Time: 2022-04-22 03:40:10
-------------------------------------------
('test_3', 1)
('test_2', 2)
('test_1', 1)

-------------------------------------------
Time: 2022-04-22 03:40:20
-------------------------------------------
('avocado', 2)
('apple', 1)
('test_1', 1)

-------------------------------------------
Time: 2022-04-22 03:40:30
-------------------------------------------
('avocado', 1)
('apple', 2)

-------------------------------------------
Time: 2022-04-22 03:40:40
-------------------------------------------
('1', 1)
('3', 2)
('test', 4)
('21', 1)
('2', 1)
```

3. Create an Spark application to count words each 10 seconds on the port 9998 and save the data on the HFDS on the directory `hdfs://namenode/user/rafael/stream/word_count` during 50 seconds.

```python
# code:
dstream = ssc.socketTextStream("localhost", 9998)

dstream \
    .flatMap(lambda x: x.split(" ")) \
    .map(lambda x: (x.lower(), 1)) \
    .reduceByKey(lambda x, y: x + y) \
    .saveAsTextFiles("hdfs://namenode/user/rafael/stream/word_count")

ssc.start()
sleep(50)
ssc.stop()
```

```bash
# input:
netcat -lp 9998
# aaaaaa
# test
# test
# aaaaaa
# 1 2 3
# 1 2 3
# 1 2 3 4 5
# 3 2
# 2 1
# 3 3
# 33 
# test
# aaaaa
#      
# avocado
# avoCADo
# TEST
# iiiii
# iiiii iiiii iiiii
# aaaaaa
# avocaDO
# 33 2 1 3
# test
```

```bash
# output:
hdfs dfs -ls /user/rafael/stream/
# Found 5 items
# drwxr-xr-x   - root supergroup          0 2022-04-22 03:16 /user/rafael/stream/word_count-1650597380000
# drwxr-xr-x   - root supergroup          0 2022-04-22 03:16 /user/rafael/stream/word_count-1650597390000
# drwxr-xr-x   - root supergroup          0 2022-04-22 03:16 /user/rafael/stream/word_count-1650597400000
# drwxr-xr-x   - root supergroup          0 2022-04-22 03:16 /user/rafael/stream/word_count-1650597410000
# drwxr-xr-x   - root supergroup          0 2022-04-22 03:17 /user/rafael/stream/word_count-1650597420000
```

