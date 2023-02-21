# Schemes

​	When dealing with structured data, such as parquet and Hive tables, Spark can infer the data schema.

​	With semi-structured data, such as CSV or JSON files, Spark can **try** to infer the schema.

## Defining schemes

​	Let's imagine we have a CSV file as follows:

```csv
id,name
1,Sales
2,TI
3,RH
```

​	The following code reads that `.csv` file and prints its schema:

```scala
spark.read.csv("sector.csv").printSchema()
// output:
// root
//  |--_c0: string (nullable = True)
//  |--_c1: string (nullable = True)
```

​	Note that the columns have no names, and all the columns are represented as `string`, even the `id`, that can be replaced by `int`.

### `inferSchema`

​	If we want Spark to "discover" the data type for us, we can add the option `"inferSchema"`:

```scala
spark.read.option("inferSchema", "true").csv("sector.csv").printSchema()
// output:
// root
//  |--_c0: int (nullable = True)
//  |--_c1: string (nullable = True)
```

​	Spark reads a few blocks of the dataframe to determine the data type of each column. Since the dataframe isn't fully analyzed to infer the types, Spark will always guess for a more generic data type. e.g.: a `float` field would be read as `double`, since Spark doesn't know how much precision will be needed to read the entire dataframe.

​	That is one of the main differences between a dataframe and a dataset: dataset always have a predefined schema.

### `header`

​	If our CSV file have a header, we can tell that to Spark using the `"header"` option:

```scala
spark.read.option("inferSchema", "true").option("header", "true").csv("sector.csv").printSchema()
// output:
// root
//  |--id: int (nullable = True)
//  |--name: string (nullable = True)
```