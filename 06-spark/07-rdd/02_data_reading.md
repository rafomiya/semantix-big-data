# Data reading and visualization

​	Pratical example:

`input_1.txt`

    Big Data
    2019
    Semantix
    Hadoop
    Semantix SP
    Hadoop 2019

`input_2.txt`

    Hadoop Course
    Data
    Hadoop
    Semantix
    SP
    Data

​	In Spark:

```scala
val rdd = sc.textFile("input*")
// rdd: org.apache.spark.rdd.RDD[String]

rdd.count()
// res2: Long = 12

rdd.first()
// res3: String = Big Data

rdd.take(5)
// res1: Array[String] = Array(Big Data, 2019, Semantix, Hadoop, Semantix SP)

rdd.foreach(println)
// displays all the values (in Scala)
```
