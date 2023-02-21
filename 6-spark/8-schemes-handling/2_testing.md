# Testing Schemes

​	First of all, let's create a schema to be used:

```python
# importing data types
from pyspark.sql.types import *

# creating fieldlist
field_list = [
    StructField("id", IntegerType()),
    StructField("sector", StringType()),
]

# creating schema
sector_schema = StructType(field_list)

# creating sample data
test_data = [
    Row(1, "Sales"),
    Row(2, "HR"),
    Row(3, "IT")
]

# creating the dataframe from the test_data
sector = spark.createDataFrame(data=test_data, schema=sector_schema)
```

​	As you can see below, it is possible to create a dataframe from an object without a `.csv` file or any other data source. This is very useful when testing schemes or related stuff.
