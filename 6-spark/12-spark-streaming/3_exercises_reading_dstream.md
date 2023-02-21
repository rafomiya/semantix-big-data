# Exercises - Reading data

1. Install o netcat on Spark's container.

```bash
docker exec -it jupyter-spark bash
apt update
apt install netcat
```

2. Create an application to read the data sent through the port 9999 and print on the console.

```python
from pyspark.streaming import StreamingContext


# creating Spark's variables
conf = SparkConf().setMaster("local[*]").setAppName("exercise_data_reading")
sc = SparkContext.getOrCreate(conf)
ssc = StreamingContext(sc, 5)  # 5 seconds interval

# creating the dstream
dstream = ssc.socketTextStream("localhost", 9999)

# defining what will be done from 5 to 5 seconds
dstream.pprint()

# starting the job
ssc.start()
# output:
# -------------------------------------------
# Time: 2022-04-22 02:34:25
# -------------------------------------------
# 
# -------------------------------------------
# Time: 2022-04-22 02:34:30
# -------------------------------------------
# test 1
# test 2
# 
# -------------------------------------------
# Time: 2022-04-22 02:34:35
# -------------------------------------------
# ------
# test 3
# 
# -------------------------------------------
# Time: 2022-04-22 02:34:40
# -------------------------------------------
# test 4
# ------
# test
# test

ssc.stop()
```
