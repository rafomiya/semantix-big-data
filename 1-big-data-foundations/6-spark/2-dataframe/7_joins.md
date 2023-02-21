# Joins

​	When dealing with a lot of tables, we may want to use a `join` to see data from more than one table on a single `select`.
​	Spark's syntax supports many of the joins from SQL, such as `inner join`, `left join` or `right join`.

​	Syntax:

```scala
df1.join(df2, df1("<column_name>") === df2("<column_name>"), "<jointype>")
```

​	Example: imagine we have two CSV files:

1. `customer.csv`

```
id,name,id_city
1,John,3
2,Karl,1
3,Monica,2
4,Phoebe,2
```

2. `city.csv`

```
id,name
1,New York
2,New Jersey
3,São Paulo
```

```scala
val customer = spark.read.option("header", "true").csv("customer.csv")
val city = spark.read.option("header", "true").csv("city.csv")

val customer_city = customer.join(city, customer("id_city") === city("id"), "left_outer")
```

