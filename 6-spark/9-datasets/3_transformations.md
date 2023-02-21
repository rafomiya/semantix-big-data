# Transformations in Datasets

​	There are two types of transformations in datasets: typed and untyped. Typed transformations will always return a new dataset, while untyped transformations will always return dataframes or untyped columns.

​	Typed transformations:

- `filter`
- `limit`
- `sort`
- `flatMap`
- `map`
- `orderBy`

​	Untyped transformations:

- `join`
- `groupBy`
- `col`
- `drop`
- `select`
- `withColumn`

​	Example: applying transformations to the existing dataset `person`:

    +---+-------+
    | id|   name|
    +---+-------+
    |  1| Rafael|
    |  2|Jéssica|
    +---+-------+

```scala
val sortedPerson = person.sort("name")
// sortedPerson: org.apache.spark.sql.Dataset[Person] = [id: int, name: string]

val nameOnly = person.select("name")
// nameOnly: org.apache.spark.sql.DataFrame = [name: string]

val combined = person.sort("name").where("id > 10").select("name")
// combined: org.apache.spark.sql.DataFrame = [name: string]
```

## Saving datasets

​	When saving a dataset, it will always be saved as a dataframe. That means the only advantage of using datasets is on the performance of the transformations.

```scala
// saves as a dataframe, even if `person` is a dataset
person.write.json("hdfs:///user/rafael/data/")
```
