# Querying with indexes

​	To force the MongoDB query optimizer to use a specific index, we use the `hint()` method:

```javascript
db.collection.find(...).hint(<key>)
```

​	Example:

```javascript
db.customer.find({ age: { $gte: 18 } }).hint({ age: -1 })
```

## `explain()`

​	This method explains the execution plan of a query, including the use of an index. This means it is very useful to know if the index is actually being used on our queries.
