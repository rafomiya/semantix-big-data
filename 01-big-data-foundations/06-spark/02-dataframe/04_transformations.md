# Transformations

​	The data contained inside a dataframe is immutable. So transformation manipulates some of the columns and sometimes returns another dataframe.

​	Some examples of transformations are:

- `select`
- `where`
- `orderBy`
- `groupBy`
- `join`
- `limit`

​	These methods works just like their SQL equivalents.

## Examples:

```scala
val amounts = productDataFrame.select("name", "amount")
val greaterFifty = amounts.where("amount > 50")
val ordered = greaterFifty.orderBy("name")
ordered.show()
// or
productDataFrame. \
	select("name", "amount"). \
	where("amount > 50"). \
	orderBy("name"). \
	show()
```

## Group by functions:

- `count`
- `max`
- `min`
- `mean`
- `sum`
- `pivot`
- `agg`

​	These methods works just like their SQL equivalents.

## The data attribute

​	There are three ways to access the data attribute:

- `"<attr>"`
- `$"<attr>"`
- `<dataframe>("<attr")`

```scala
productDataFrame.select("name", $"amount" * 1.5).show()
productDataFrame.where(productDataFrame("name").startsWith("A")).show()
```

