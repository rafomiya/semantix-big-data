# Reading Data

​	To read data through Spark Streaming, we need to create a `StreamingContext` variable (`ssc`). Here's how to do so in Pyspark and Scala:

```python
from pyspark import SparkContext
from pyspark.streaming import StreamingContext


conf = SparkConf().setMaster("local")
sc = SparkContext.getOrCreate(conf)
ssc = StreamingContext(sc, 2)  # 2 seconds interval
```

```scala
import org.apache.spark._
import org.apache.spark.streaming._


val conf = new SparkConf().setMaster("local")
val sc = new SparkContext(conf)
val ssc = new StreamingContext(sc, Seconds(2))  // 2 seconds interval
```

​	Creating a DStream to capture data from the session active on the port 9999:

```python
dstr = ssc.socketTextStream("localhost", 9999)

dstr.pprint()  # outputs the data

ssc.start()
```

```scala
val dstr = ssc.socketTextStream("localhost", 9999)

dstr.print()  // outputs the data

ssc.start()
```

​	Using netcat to send data to the port 9999:

```bash
netcat -lp 9999
```
