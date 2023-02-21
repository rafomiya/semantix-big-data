# Creating Schemes

## Data types

​	Spark has many types of data to store informations:

- Numeric types:
    - `ByteType`
    - `ShortType`
    - `IntegerType`
    - `LongType`
    - `FloatType`
    - `DoubleType`
    - `DecimalType`
    - `BigDecimal`
- Textual types:
    - `StringType`
- Binary types:
    - `BinaryType`
    - `BooleanType`
- Time types:
    - `TimestampType`
    - `DateType`
- Complex types:
    - `ArrayType`
    - `MapType`
    - `StructType`

## Schemes Concepts

### `inferSchema`

​	In Spark, it is possible to infer the schema of a dataframe. This process consists in three steps:

- Reads a few blocks of the data available;
- Infer the data type of each column based on this reading; and
- Since the data isn't fully analyzed, take the most generic type as possible. e.g.: `IntegerType` becomes `LongType`.

​	Example:

`sector.csv`

    id,sector
    1,Sales
    2,HR
    3,IT

```scala
spark.read.option("inferSchema", "true").option("header", "true").csv("sector.csv").printSchema()
```

### Using created schemes

​	We can also create a schema for our data:

​	Example:

`sector.csv`

    id,sector
    1,Sales
    2,HR
    3,IT

```scala
// importing data types
import org.apache.spark.sql.types._

// creating fieldlist
val fieldList = List(
    StructField("id", IntegerType),
    StructField("sector", StringType)
)

// creating schema
val sectorSchema = StructType(fieldList)

// reading a file applying the created schema
val sector = spark.read.option("header", "true").schema(sectorSchema).csv("sector.csv")
```

```python
# importing data types
from pyspark.sql.types import *

# creating fieldlist
field_list = [
    StructField("id", IntegerType()),
    StructField("sector", StringType())
]

# creating schema
sector_schema = StructType(field_list)

# reading a file applying the created schema
sector = spark.read.option("header", "true").schema(sector_schema).csv("sector.csv")
```
