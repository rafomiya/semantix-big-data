# Other Query Options

## Logical operators

### `and`

​	`and` is the default operator when using more than0 one operator per field.

​	Example:

```javascript
db.product.find({
    amount: {
        $gt: 0,
        $lte: 100
    }
})
// returns all the products with
// amount greater than 0 AND lesser
// than or equals to 100.
```

### `or`

​	To use the​	`or` operator, we must create an array with the conditions to be checked.

​	Example:

```javascript
db.product.find({
    $or: [
        { nome: { $eq: "mouse" } },
        { _id: 2 }
    ]
})
// returns all the products with
// nome equals to 'mouse' OR '_id'
// equals to 2.
```

### `$and` and `$or`

​	We can also use both operators in the same query:

```javascript
db.customer.find({
    os: "Windows",
    { $or: [
        { "address.city": "São Paulo" },
        { age: { $gte: 18 }}
    ]}
})
```

## Ordering results

​	The `sort` method is equivalent to the `order by` keyword in SQL.

​	Syntax:

```javascript
db.collection.find(<...>).sort({ '<attribute>': '<value>', '<attribute>': '<value>' })
```

- attribute: the attribute that will be used to order the results.
- value: `1` or `-1`, to order as ascending or descending.

​	You can also order the results by more than one attribute, simply adding more items in the parameters.

​	Example:

```javascript
db.product.find({}).sort({ price: 1, name: 1 })
```

## Limit the results

​	If we want just a specific amount of documents to be returned, we can specify this amount throught the `limit` method:


​	Syntax:

```javascript
db.collection.find().limit(<amount>)
```

- amount: the amount of documents to be returned.

​	Example:

```javascript
db.product.find({}).sort({ price: 1, name: 1 }).limit(3)
```

### `findOne`

​	If we want simply one document as result, we can use the `findOne()` method instead of specifying `.limit(1)` at the end of a `find()`.

​	Syntax:

```javascript
db.collection.findOne({...})
```

​	Example:

```javascript
db.product.findOne({ _id: 3 })
```