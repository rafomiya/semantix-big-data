# Exercises - Schemes

1. Create the dataframe `names_us_without_schema` to read the files on the HDFS at `/user/rafael/data/names`.

```python
names_us_without_schema = spark.read.csv("/user/rafael/data/names")
```

2. Visualize the schema and the first 5 rows of `names_us_without_schema`.

```python
names_us_without_schema.printSchema()
names_us_without_schema.take(5)
# output:
# root
#  |-- _c0: string (nullable = true)
#  |-- _c1: string (nullable = true)
#  |-- _c2: string (nullable = true)
# 
# [Row(_c0='Emma', _c1='F', _c2='18809'),
#  Row(_c0='Isabella', _c1='F', _c2='18612'),
#  Row(_c0='Emily', _c1='F', _c2='17429'),
#  Row(_c0='Olivia', _c1='F', _c2='17078'),
#  Row(_c0='Ava', _c1='F', _c2='17035')]
```

3. Create the dataframe `names_us` to read the files on the HDFS at `/user/rafael/data/names` with the following schema:

- `name`: `String`
- `sex`: `String`
- `quantity`: `Integer`

```python
from pyspark.sql.types import *

names_schema = StructType([
    StructField("name", StringType()),
    StructField("sex", StringType()),
    StructField("quantity", IntegerType())
])

names_us = spark.read.csv(path="/user/rafael/data/names", schema=names_schema)
```

4. Visualize the schema and the first 5 rows of `names_us`.

```python
names_us.printSchema()
names_us.take(5)
# output:
# root
#  |-- name: string (nullable = true)
#  |-- sex: string (nullable = true)
#  |-- quantity: integer (nullable = true)
# 
# [Row(name='Emma', sex='F', quantity=18809),
#  Row(name='Isabella', sex='F', quantity=18612),
#  Row(name='Emily', sex='F', quantity=17429),
#  Row(name='Olivia', sex='F', quantity=17078),
#  Row(name='Ava', sex='F', quantity=17035)]
```

5. Save the dataframe `names_us` on the format `orc` on the HDFS at `/user/rafael/names_us_orc`.

```python
names_us.write.orc(path="/user/rafael/names_us_orc")
# verifying if the data has been written correctly:
!hdfs dfs -ls /user/rafael/names_us_orc
# output:
# Found 9 items
# -rw-r--r--   2 root supergroup          0 2022-04-15 22:24 /user/rafael/names_us_orc/_SUCCESS
# -rw-r--r--   2 root supergroup    3315116 2022-04-15 22:24 /user/rafael/names_us_orc/part-00000-c5c519ff-52f2-46ea-8cc8-fcfccac6df93-c000.snappy.orc
# -rw-r--r--   2 root supergroup    2556757 2022-04-15 22:24 /user/rafael/names_us_orc/part-00001-c5c519ff-52f2-46ea-8cc8-fcfccac6df93-c000.snappy.orc
# -rw-r--r--   2 root supergroup    1770422 2022-04-15 22:24 /user/rafael/names_us_orc/part-00002-c5c519ff-52f2-46ea-8cc8-fcfccac6df93-c000.snappy.orc
# -rw-r--r--   2 root supergroup    1195508 2022-04-15 22:24 /user/rafael/names_us_orc/part-00003-c5c519ff-52f2-46ea-8cc8-fcfccac6df93-c000.snappy.orc
# -rw-r--r--   2 root supergroup    1062692 2022-04-15 22:24 /user/rafael/names_us_orc/part-00004-c5c519ff-52f2-46ea-8cc8-fcfccac6df93-c000.snappy.orc
# -rw-r--r--   2 root supergroup     920100 2022-04-15 22:24 /user/rafael/names_us_orc/part-00005-c5c519ff-52f2-46ea-8cc8-fcfccac6df93-c000.snappy.orc
# -rw-r--r--   2 root supergroup     193555 2022-04-15 22:24 /user/rafael/names_us_orc/part-00006-c5c519ff-52f2-46ea-8cc8-fcfccac6df93-c000.snappy.orc
# -rw-r--r--   2 root supergroup     108717 2022-04-15 22:24 /user/rafael/names_us_orc/part-00007-c5c519ff-52f2-46ea-8cc8-fcfccac6df93-c000.snappy.orc
```
