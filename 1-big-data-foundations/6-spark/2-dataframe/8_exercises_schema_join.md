# Exercises - Schemas and Joins

1. Create the dataframe `studentDf` to read the HDFS file `/user/aluno/rafael/data/escola/alunos.csv`, without the `option` method.

```scala
val studentDf = spark.read.csv("/user/aluno/rafael/data/escola/alunos.csv")
// output:
// studentDf: org.apache.spark.sql.DataFrame = [_c0: string, _c1: string ... 5 more fields]
```

2. Visualize the `studentDf` schema.

```scala
studentDf.printSchema
// output:
// root
//  |-- _c0: string (nullable = true)
//  |-- _c1: string (nullable = true)
//  |-- _c2: string (nullable = true)
//  |-- _c3: string (nullable = true)
//  |-- _c4: string (nullable = true)
//  |-- _c5: string (nullable = true)
//  |-- _c6: string (nullable = true)
```

3. Create the dataframe `studentDf` to read the file `/user/aluno/rafael/data/escola/alunos.csv`, with the option of including the header.

```scala
val studentDf = spark.read.option("header", "true").csv("/user/aluno/rafael/data/escola/alunos.csv")
// output:
// studentDf: org.apache.spark.sql.DataFrame = [id_discente: string, nome: string ... 5 more fields]
```

4. Visualize the `studentDf` schema.

```scala
studentDf.printSchema
// output:
// root
//  |-- id_discente: string (nullable = true)
//  |-- nome: string (nullable = true)
//  |-- ano_ingresso: string (nullable = true)
//  |-- periodo_ingresso: string (nullable = true)
//  |-- nivel: string (nullable = true)
//  |-- id_forma_ingresso: string (nullable = true)
//  |-- id_curso: string (nullable = true)
```

5. Create the dataframe `studentDf` to read the file `/user/aluno/rafael/data/escola/alunos.csv` with the option of including the header and infer the schema.

```scala
val studentDf = spark.read.option("header", "true").option("inferSchema", "true").csv("/user/aluno/rafael/data/escola/alunos.csv")
// output:
// studentDf: org.apache.spark.sql.DataFrame = [id_discente: int, nome: string ... 5 more fields]
```

6. Visualize the `studentDf` schema.

```scala
studentDf.printSchema
// output:
// root
//  |-- id_discente: integer (nullable = true)
//  |-- nome: string (nullable = true)
//  |-- ano_ingresso: integer (nullable = true)
//  |-- periodo_ingresso: integer (nullable = true)
//  |-- nivel: string (nullable = true)
//  |-- id_forma_ingresso: integer (nullable = true)
//  |-- id_curso: integer (nullable = true)
```

7. Save the dataframe `studentDf` as a Hive table called `student` on the database `rafael`.

```scala
studentDf.write.saveAsTable("rafael.student")
```

8. Create the dataframe `coursesDf` to read the file `/user/aluno/rafael/data/escola/cursos.csv` with the option of including the header and infer the schema.

```scala
val coursesDf = spark.read.option("inferSchema", "true").option("header", "true").csv("/user/aluno/rafael/data/escola/cursos.csv")
// output:
// coursesDf: org.apache.spark.sql.DataFrame = [id_curso: int, id_unidade: int ... 10 more fields]
```

9. Create the dataframe `studentCoursesDf` with a inner join of `studentDf` and `coursesDf` when the `id_curso` is equal in both tables.

```scala
val studentCoursesDf = studentDf.join(coursesDf, "id_curso")
// output:
// studentCoursesDf: org.apache.spark.sql.DataFrame = [id_curso: int, id_discente: int ... 16 more fields]
```

10. Visualize the data, the schema and the amount of rows from `studentCoursesDf`

```scala
studentCoursesDf.show(5)
// output:
// +--------+-----------+--------------------+------------+----------------+-----+-----------------+----------+--------+--------------------+-----+----------------------+------------+--------------------+-------------+-----------------+--------------------+-----+
// |id_curso|id_discente|                nome|ano_ingresso|periodo_ingresso|nivel|id_forma_ingresso|id_unidade|  codigo|                nome|nivel|id_modalidade_educacao|id_municipio|id_tipo_oferta_curso|id_area_curso|id_grau_academico|id_eixo_conhecimento|ativo|
// +--------+-----------+--------------------+------------+----------------+-----+-----------------+----------+--------+--------------------+-----+----------------------+------------+--------------------+-------------+-----------------+--------------------+-----+
// |   76995|      18957|ABELARDO DA SILVA...|        2017|               1|    G|            62151|       194|    null|LICENCIATURA EM C...|    G|                     1|        8550|                   4|     20000006|          8067070|                null|    1|
// |    3402|        553| ABIEL GODOY MARIANO|        2015|            null|    M|          2081113|       150|SVTIAGRO|TÉCNICO EM AGROPE...|    M|                     1|        9332|                null|         null|             null|             6264215|    1|
// |  759711|      17977|ABIGAIL ANTUNES S...|        2017|               1|    T|          2081111|       696| UGTCADM|TÉCNICO EM ADMINI...|    T|                     1|        9431|                null|         null|             null|              171158|    1|
// |    1222|      16613|ABIGAIL FERNANDA ...|        2017|            null|    M|            37350|       349|PBTIQUIM|TÉCNICO EM QUÍMIC...|    M|                     1|        9091|                null|         null|             null|             6264214|    1|
// |    5041|      17398|ABIGAIL JOSIANE R...|        2017|            null|    M|            37350|       189|ALTIAGRP|TÉCNICO EM AGROPE...|    M|                     1|        8550|                null|         null|             null|                null|    1|
// +--------+-----------+--------------------+------------+----------------+-----+-----------------+----------+--------+--------------------+-----+----------------------+------------+--------------------+-------------+-----------------+--------------------+-----+

studentCoursesDf.printSchema
// output:
// root
//  |-- id_curso: integer (nullable = true)
//  |-- id_discente: integer (nullable = true)
//  |-- nome: string (nullable = true)
//  |-- ano_ingresso: integer (nullable = true)
//  |-- periodo_ingresso: integer (nullable = true)
//  |-- nivel: string (nullable = true)
//  |-- id_forma_ingresso: integer (nullable = true)
//  |-- id_unidade: integer (nullable = true)
//  |-- codigo: string (nullable = true)
//  |-- nome: string (nullable = true)
//  |-- nivel: string (nullable = true)
//  |-- id_modalidade_educacao: integer (nullable = true)
//  |-- id_municipio: integer (nullable = true)
//  |-- id_tipo_oferta_curso: integer (nullable = true)
//  |-- id_area_curso: integer (nullable = true)
//  |-- id_grau_academico: integer (nullable = true)
//  |-- id_eixo_conhecimento: integer (nullable = true)
//  |-- ativo: integer (nullable = true)

studentCoursesDf.count
// output:
// res4: Long = 9954
```
