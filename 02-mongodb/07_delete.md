# Delete documents

​	Key commands:

```javascript
db.collection.deleteOne(<filter>)
db.collection.deleteMany(<filter>)
```

- `filter`: works just like the `where` clause from the usual SQL statements, but using the JSON syntax. It is pretty much like the first parameter of the `find()` or `updateOne()` method.

​	Example:

```javascript
// deleteOne()
db.customer.deleteOne({ _id: 3 })

// deleteMany()
db.customer.deleteMany({ status: 'Inactive' })
```