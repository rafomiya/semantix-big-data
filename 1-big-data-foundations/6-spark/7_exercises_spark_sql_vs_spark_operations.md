# #xercises - Spark SQL vs. Spark Operations

Do the following queries using SparkSQL and dataframe transformations on the table `student`, of the database `rafael`.

0. Analyzing the schema and defining the current database.

```scala
spark.catalog.setCurrentDatabase("rafael")
spark.catalog.listColumns("student").show(false)
// output:
// +-----------------+-----------+--------+--------+-----------+--------+
// |name             |description|dataType|nullable|isPartition|isBucket|
// +-----------------+-----------+--------+--------+-----------+--------+
// |id_discente      |null       |int     |true    |false      |false   |
// |nome             |null       |string  |true    |false      |false   |
// |ano_ingresso     |null       |int     |true    |false      |false   |
// |periodo_ingresso |null       |int     |true    |false      |false   |
// |nivel            |null       |string  |true    |false      |false   |
// |id_forma_ingresso|null       |int     |true    |false      |false   |
// |id_curso         |null       |int     |true    |false      |false   |
// +-----------------+-----------+--------+--------+-----------+--------+
```

1. Visualize the `id_discente` and `nome` of the first 5 rows.

```scala
// SparkSQL
spark.sql("select id_discente, nome from student limit 5").show

// Spark transformations
spark.read.table("student").select("id_discente", "nome").limit(5).show

// output:
// +-----------+--------------------+
// |id_discente|                nome|
// +-----------+--------------------+
// |      18957|ABELARDO DA SILVA...|
// |        553| ABIEL GODOY MARIANO|
// |      17977|ABIGAIL ANTUNES S...|
// |      16613|ABIGAIL FERNANDA ...|
// |      17398|ABIGAIL JOSIANE R...|
// +-----------+--------------------+
```

2. Visualize the `id_discente`, `nome` and `ano_ingresso` when the `ano_ingresso` is greater or equal to 2018.

```scala
// SparkSQL
spark.sql("select id_discente, nome, ano_ingresso from student where ano_ingresso >= 2018").show(5)

// Spark transformations
spark.read.table("student").select("id_discente", "nome", "ano_ingresso").where("ano_ingresso >= 2018").show(5)

// output:
// +-----------+--------------------+------------+
// |id_discente|                nome|ano_ingresso|
// +-----------+--------------------+------------+
// |      26880|ABIMAEL CHRISTOPF...|        2019|
// |      28508|   ABNER NUNES PERES|        2019|
// |      28071|ACSA ROBALO DOS S...|        2019|
// |      21968|AÇUCENA CARVALHO ...|        2018|
// |      22374|ADALBERTO LUFT LU...|        2018|
// +-----------+--------------------+------------+
```

3. Visualize, ordered by `nome`, the `id_discente`, `nome` and `ano_ingresso` when the `ano_ingresso` is greater or equal to 2018.

```scala
// SparkSQL
spark.sql("select id_discente, nome, ano_ingresso from student where ano_ingresso >= 2018 order by nome").show(5)

// Spark transformations
spark.read.table("student").select("id_discente", "nome", "ano_ingresso").where("ano_ingresso >= 2018").orderBy("nome").show(5)

// output:
// +-----------+--------------------+------------+
// |id_discente|                nome|ano_ingresso|
// +-----------+--------------------+------------+
// |      26880|ABIMAEL CHRISTOPF...|        2019|
// |      28508|   ABNER NUNES PERES|        2019|
// |      28071|ACSA ROBALO DOS S...|        2019|
// |      22374|ADALBERTO LUFT LU...|        2018|
// |      26367|ADALBERTO SEIDEL ...|        2019|
// +-----------+--------------------+------------+
```

4. Count the amount of rows from the previous item.

```scala
// SparkSQL
spark.sql("select id_discente, nome, ano_ingresso from student where ano_ingresso >= 2018 order by nome desc").count

// Spark transformations
spark.read.table("student").select("id_discente", "nome", "ano_ingresso").where("ano_ingresso >= 2018").orderBy($"nome".desc).count

// output:
res13: Long = 4266
```
