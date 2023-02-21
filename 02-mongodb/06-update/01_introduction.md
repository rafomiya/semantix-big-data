# Update documents

​	Key commands:

```javascript
db.collection.updateOne(<filter>, <data>)
db.collection.updateMany(<filter>, <data>)
```

- `filter`: works just like the `where` clause from the usual SQL statements, but using the JSON syntax. It is pretty much like the first parameter of the `find()` method.
- `data`: the update itself. `{ <updateoperator>: { <attribute>: <value>, <...> } }`.

### Update operators

- `$set`: updates/creates the attribute.
  - If the target document doesn't exists, it will be created.
  - Example:

```javascript
db.customer.updateOne(
	{ _id: 1 },
	{
		$set: {
			age: 25,
			address: { city: "São Paulo" }
		}
	}
)
```

- `$unset`: deletes an attribute.
  - The data must always be `""`.
  - Example:

```javascript
db.customer.updateOne(
	{ _id: 1 },
	{ $unset: { age: "" } }
)
```

- `$rename`: renames an attribute.
  - Example:

```javascript
db.customer.updateMany(
	{}, // empty 'where', so it will affect all the documents
	{ rename: { 'age': 'years_spent_on_earth' } }
)
```

### Updating many documents

```javascript
db.customer.updateMany(
	{ age: { $gte: 18 } },
    { $set: { military: true } }
)
```

