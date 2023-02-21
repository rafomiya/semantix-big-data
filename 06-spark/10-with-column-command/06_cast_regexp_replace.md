# Functions Cast, Regex Replace & When

## `cast`

​	Changes the data type of a field.

​	Syntax:

```python
from pyspark.sql.functions import col
from pyspark.sql.types import *


dataframe.withColumn(column_name, column.cast(new_type))
```

​	Example I: the dataframe `product` has the column `price`. This column's data type is `String`, on the format `1000.00`. We can cast it to `FloatType`:

```python
from pyspark.sql.types import FloatType
from pyspark.sql.functions import col


converted_float = product.withColumn("float_price", col("price").cast(FloatType()))
converted_float.show()
# output:
# +-------+-----------+
# |  price|float_total|
# +-------+-----------+
# |1000.00|     1000.0|
# +-------+-----------+
converted_float.printSchema()
# output:
# root
#  |-- price: string (nullable = true)
#  |-- real total: float (nullable = true)
```

​	Example II: same situation, but this time, we want to create a field with the formatted price.

```python
from pyspark.sql.functions import format_number


formatted_price = product.withColumn("formatted_price", format_number(col("price").cast(FloatType()), 2))
formatted_price.show()
# output:
# +-------+---------------+
# |  price|formatted_price|
# +-------+---------------+
# |1000.00|       1,000.00|
# +-------+---------------+
formatted_price.printSchema()
# output:
# root
#  |-- price: string (nullable = true)
#  |-- real total: string (nullable = true)
```

## `regexp_replace`

​	Replaces a given pattern by another value.

​	Syntax:

```python
from pyspark.sql.functions import col
from pyspark.sql.types import *


dataframe.withColumn(column_name, regexp_replace(column, pattern, new_value))
```

​	Example: replacing the `","` of the field `price` (`StringType`) to `"."`, and then cast it to `FloatType`:

```python
product = product.withColumn("price", regexp_replace(col("price"), ",", ".").cast(FloatType()))
```

## `when`

​	The `when` command is responsible for representing a boolean condition on the dataframe transformation.

​	Syntax:

```python
from pyspark.sql.functions import when


dataframe.withColumn(column_name, when(condition, true_value).otherwise(false_value))
```

​	Example:

```python
from pyspark.sql.functions import when, substring, length


codes = product.select("code").take(5)
# codes = { AABC, ACBB, 00ABCC, AACC, 00BBCC }

# removing the digit 0 before the code itself
codes = codes.withColumn("code_without_zero", when(length(col("cod")) > 4, substring(col("cod"), 3, 4)).otherwise(col("cod")))
codes.show()
# codes = { AABC, ACBB, ABCC, AACC, BBCC }
```


