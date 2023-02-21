# API Catalog

​	API Catalog is a resource to explore tables and manage views.

## Functions

​	API Catalog features are on `spark.catalog`. We can start using the module's functions:

- `listDatabases`: lists the available databases. If the desired database doesn't appear, that is probably due to Spark configuration problems or not imported packages.
- `setCurrentDatabase(database)`: sets the current database to be used.
- `listTables`: lists the tables of the current database.
- `listColumns(table)`: lists the columns from a table.
- `dropTempView(view)`: drops a view.

## Example

```scala
// this works
spark.sql("select * from database.table").show(5)

// defining the current database
spark.catalog.listDatabases.show
spark.catalog.setCurrentDatabase("database")
spark.catalog.listTables.show

// now this also works, even if
// we don't specify the database.
spark.sql("select * from table").show(5)
```

