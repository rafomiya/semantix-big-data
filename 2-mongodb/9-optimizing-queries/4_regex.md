# Regex

​	To use regular expressions inside our queries, we can use the `$regex` operator as follows:

```javascript
// first way
db.collection.find({ <attribute>: { $regex: /pattern/, $options: <options> } })

// second way
db.collection.find({ <attribute>: { $regex: '/pattern/', $options: '<options>' } })

// third way (most used)
db.collection.find({ <attribute>: { $regex: /pattern/<options> } })
```

​	Example:

```javascript
db.customer.find({ name: { $regex: /rafael/i } }); // searches for the word 'rafael' with case insensitivity
db.customer.find({ cpf: { $regex: /^423/ } }) // searches for cpfs starting with '423'
```

