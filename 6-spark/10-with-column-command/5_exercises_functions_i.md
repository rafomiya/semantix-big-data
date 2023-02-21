# Exercises - Functions

1. Create a dataframe to read the HDFS file at `/user/rafeal/data/juros_selic/juros_selic`.

```bash
hdfs dfs -cat /user/rafael/data/juros_selic/juros_selic | head -n 5
# output:
# "data";"valor"
# "01/06/1986";"1,27"
# "01/07/1986";"1,95"
# "01/08/1986";"2,57"
# "01/09/1986";"2,94"
```

```python
fees = spark.read.csv("/user/rafael/data/juros_selic/juros_selic", sep=";", header=True)

fees.printSchema()
fees.show(5)
# output:
# root
#  |-- data: string (nullable = true)
#  |-- valor: string (nullable = true)

# +----------+-----+
# |      data|valor|
# +----------+-----+
# |01/06/1986| 1,27|
# |01/07/1986| 1,95|
# |01/08/1986| 2,57|
# |01/09/1986| 2,94|
# |01/10/1986| 1,96|
# +----------+-----+
# only showing top 5 rows
```

2. Alter the format of the field `data` to `"MM/dd/yyyy"`.

```python
from pyspark.sql.functions import unix_timestamp, from_unixtime, col


fees = fees.withColumn("data", from_unixtime(unix_timestamp(col("data"), "dd/MM/yyyy"), "MM/dd/yyyy"))
fees.show(5)
# output:
# +----------+-----+
# |      data|valor|
# +----------+-----+
# |06/01/1986| 1,27|
# |07/01/1986| 1,95|
# |08/01/1986| 2,57|
# |09/01/1986| 2,94|
# |10/01/1986| 1,96|
# +----------+-----+
# only showing top 5 rows
```

3. Using the function `from_unixtime`, create the field `year_unix`, with the information of the year of the field `data`.

```python
fees = fees.withColumn("year_unix", from_unixtime(unix_timestamp("data", "dd/MM/yyyy"), "yyyy"))
fees.show(5)
# output:
# +----------+-----+---------+
# |      data|valor|year_unix|
# +----------+-----+---------+
# |06/01/1986| 1,27|     1986|
# |07/01/1986| 1,95|     1986|
# |08/01/1986| 2,57|     1986|
# |09/01/1986| 2,94|     1986|
# |10/01/1986| 1,96|     1986|
# +----------+-----+---------+
# only showing top 5 rows
```

4. Using the function `substring`, create the field `year_str`, with the information of the year of the field `data`.

```python
from pyspark.sql.functions import substring


fees = fees.withColumn("year_str", substring(col("data"), 7, 4))
fees.show(5)
# output:
# +----------+-----+---------+--------+
# |      data|valor|year_unix|year_str|
# +----------+-----+---------+--------+
# |06/01/1986| 1,27|     1986|    1986|
# |07/01/1986| 1,95|     1986|    1986|
# |08/01/1986| 2,57|     1986|    1986|
# |09/01/1986| 2,94|     1986|    1986|
# |10/01/1986| 1,96|     1986|    1986|
# +----------+-----+---------+--------+
# only showing top 5 rows
```

5. Using the function `split`, create the field `year_split`, with the information of the year of the field `data`.

```python
from pyspark.sql.functions import split


fees = fees.withColumn("year_split", split(col("data"), "/").getItem(2))
fees.show(5)
# output
# +----------+-----+---------+--------+----------+
# |      data|valor|year_unix|year_str|year_split|
# +----------+-----+---------+--------+----------+
# |06/01/1986| 1,27|     1986|    1986|      1986|
# |07/01/1986| 1,95|     1986|    1986|      1986|
# |08/01/1986| 2,57|     1986|    1986|      1986|
# |09/01/1986| 2,94|     1986|    1986|      1986|
# |10/01/1986| 1,96|     1986|    1986|      1986|
# +----------+-----+---------+--------+----------+
# only showing top 5 rows
```

6. Save on the HFDS at `/user/rodrigo/juros_selic_americano` on the format CSV, including the header.

```python
fees.write.csv("/user/rodrigo/juros_selic_americano", header=True, sep=";")
```

```bash
!hdfs dfs -ls /user/rodrigo/juros_selic_americano
# output:
# Found 2 items
# -rw-r--r--   2 root supergroup          0 2022-04-19 17:19 /user/rodrigo/juros_selic_americano/_SUCCESS
# -rw-r--r--   2 root supergroup      12303 2022-04-19 17:19 /user/rodrigo/juros_selic_americano/part-00000-11cc58f5-9fd1-446d-ae00-c5af4364caed-c000.csv
```
