# Creating a Dataset

## Creating from sample data

​	To create a dataset, we must first create a case class defining the schema:

```scala
case class Name(id: Integer, name: String)
```

​	Then, we must create a sequence of objects of the created class. This sequence will become our dataset:

```scala
val objectSequence = Seq(Name(1, "Rafael"), Name(2, "Jéssica"))
val nameDS = spark.createDataset(objectSequence)
```

## Creating from a dataframe

​	To create a dataset from a dataframe, we have to follow the following steps:

- Read and create the dataframe as usual.
    - The dataframe need to have a schema, since the dataset is strongly typed.
    - This schema has to be compatible with the created case class.
- Add the `as` statement at the end of the declaration of the dataset.

```scala
case class Person(id: Integer, name: String, age: Integer)

val personsDS = spark.read.json("persons.json").as[Person]

// or

import org.apache.spark.sql.Encoders

// this creates a StructType, the same way we created schemas when hadling datasets.
val personSchema = Encoders.product[Person].schema

val personsDS = spark.read.schema(personSchema).json("persons.json").as[Person]
```

## Creating from a RDD

1. Create the case class:

```scala
case class DiscoveredCoord(
    id: Integer,
    coord: Tuple2[Double, Double]
)

val discoveredCoordRDD = sc.textFile("coords.tsv") \
    .map(_.split("\t")) \
    .map(fields => Discoveredcoord(
        fields(0),
        (fields(1),toFloat, fields(2).toFloat)
    ))

val discoveredCoordDS = spark.createDataset(discoveredCoordRDD)

discoveredCoordDS.printSchema

println(discoveredCoordDS.first)
```
