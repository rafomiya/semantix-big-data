# Exercises - DataFrame

1. Send the local directory `/input/exercises-data/juros_selic` to the HDFS path `/user/aluno/rafael/data`

```bash
hdfs dfs -put /input/exercises-data/juros_selic /user/aluno/rafael/data
```

2. Create the dataframe `feesDf` to read the HDFS file `/user/aluno/rafael/data/juros_selic/juros_selic.json`.

```scala
val feesDf = spark.read.json("/user/aluno/rafael/data/juros_selic/juros_selic.json")
// output:
// feesDf: org.apache.spark.sql.DataFrame = [data: string, valor: string]          
```

3. Visualize the `feesDf` schema.

```scala
feesDf.printSchema
// output:
// root
//  |-- data: string (nullable = true)
//  |-- valor: string (nullable = true)
```

4. Show the first 5 rows of the dataframe `feesDf`.

```scala
feesDf.show(5)
// output:
// +----------+-----+
// |      data|valor|
// +----------+-----+
// |01/06/1986| 1.27|
// |01/07/1986| 1.95|
// |01/08/1986| 2.57|
// |01/09/1986| 2.94|
// |01/10/1986| 1.96|
// +----------+-----+
// only showing top 5 rows
```

5. Count the amount of rows of `feesDf`.

```scala
feesDf.count
// output:
// res7: Long = 393
```

6. Create the dataframe `feesDf10` to filter only the rows with the field `valor` greater than 10.

```scala
val feesDf10 = feesDf.where("valor > 10")
// output:
// feesDf10: org.apache.spark.sql.Dataset[org.apache.spark.sql.Row] = [data: string, valor: string]
```

7. Save the dataframe `feesDf10` as a Hive table `rafael.fees_selic`.

```scala
feesDf10.write.saveAsTable("rafael.fees_selic")
```

8. Create the dataframe `feesHiveDf` to read the table `rafael.fees_selic`

```scala
val feesHiveDf = spark.read.table("rafael.fees_selic")
// output:
// feesHiveDf: org.apache.spark.sql.DataFrame = [data: string, valor: string]
```

9. Visualize the `feesHiveDf` schema.

```scala
feesHiveDf.printSchema
// output:
// root
//  |-- data: string (nullable = true)
//  |-- valor: string (nullable = true)
```

10. Show the first 5 rows of the dataframe `feesHiveDf`.

```scala
feesHiveDf.show(5)
// output:
// +----------+-----+
// |      data|valor|
// +----------+-----+
// |01/01/1987|11.00|
// |01/02/1987|19.61|
// |01/03/1987|11.95|
// |01/04/1987|15.30|
// |01/05/1987|24.63|
// +----------+-----+
// only showing top 5 rows
```

11. Save the dataframe `feesHiveDf` on the HDFS at the directory `/user/aluno/rafael/data/save_fees` as parquet.

```scala
feesHiveDf.write.save("/user/aluno/rafael/data/save_fees") 
```

12. Visualize the `save_fees` on the HDFS.

```bash
hdfs dfs -ls /user/aluno/rafael/data/save_fees
# output:
# Found 2 items
# -rw-r--r--   2 root supergroup          0 2022-02-21 18:04 /user/aluno/rafael/data/save_fees/_SUCCESS
# -rw-r--r--   2 root supergroup       1419 2022-02-21 18:04 /user/aluno/rafael/data/save_fees/part-00000-503cdf16-9836-4ce2-a0c1-6a1e3a188422-c000.snappy.parquet
```

13. Create the dataframe `feesHdfs` to read the `save_fees` directory from question 8.

```scala
val feesHdfs = spark.read.load("/user/aluno/rafael/data/save_fees")
// output:
// feesHdfs: org.apache.spark.sql.DataFrame = [data: string, valor: string]
```

14. Visualize the `feesHdfs` schema.

```scala
feesHdfs.printSchema
// output:
// root
//  |-- data: string (nullable = true)
//  |-- valor: string (nullable = true)
```

15. Show the first 5 rows of the dataframe `feesHdfs`.

```scala
feesHdfs.show(5)
// output:
// +----------+-----+
// |      data|valor|
// +----------+-----+
// |01/01/1987|11.00|
// |01/02/1987|19.61|
// |01/03/1987|11.95|
// |01/04/1987|15.30|
// |01/05/1987|24.63|
// +----------+-----+
// only showing top 5 rows
```
