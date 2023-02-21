# Actions

​	There are many possible actions to be done in a dataframe. Here are some examples:

- `count`: returns the amount of lines.
- `first`: returns the first line.
- `take(n)`: returns `n` lines as an array.
- `show(n)`: displays the first `n` lines.
- `collect`: brings all the information of the drive nodes.
  - Warning: be careful.
- `distincts`: returns the rows removing repeated data.
- `write`: save data.
- `printSchema()`: visualize the data structure.
  - Dataframes aways have a schema.

​	OBS: `take` vs. `show`: the key difference between these actions is that `take` takes the closest `n` rows on memory, meanwhile `show` will take the first 10.

## Examples

```scala
val clientDataFrame = spark.read.json("customer.json")
clientDataFrame.printSchema()
clientDataFrame.count()
clientDataFrame.first()
clientDataFrame.take(5)
clientDataFrame.show(5)
clientDataFrame.distinct()
// clientDataFrame.collect()

```

​	All these methods (except for write) works right without the `()` parentheses after the action name. `take` and `show` will return 5 rows by default.

### `write`

```scala
clientDataFrame.write.save("parquetFile")
clientDataFrame.write.json("jsonFile")
clientDataFrame.write.csv("csvFile")
clientDataFrame.write.saveAsTable("hiveTable") // saves on /user/hive/warehouse
```
