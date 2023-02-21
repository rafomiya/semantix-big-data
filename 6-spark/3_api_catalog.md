# API Catalog

​	The Catalog is an object that allows us to manage the metadata of SparkSQL.

​	Example:

```python
table = spark.sql("select * from bdtest.user").show(10)

spark.catalog.listDatabases()
spark.catalog.setCurrentDatabase("bdtest")
spark.catalog.listTables.show()

table = spark.sql("select * from user").show(10)
```
