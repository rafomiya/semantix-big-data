# Updating arrays

## The `$` operator

​	When updating an item inside the array, we can do so with the `$` operator.

​	It will update one element from the array, and this element will be specified through the filter (first parameter of the update methods).

​	Example:

```javascript
db.customer.updateOne(
    { _id: 4, "knowledge": "Mongo" },
    { $set: { "knowledge.$": "MongoDB" } }
)
// updates the array `knowledge`, altering
// the item 'Mongo' to 'MongoDB'
```

​	The `$` operator indicates that only the first appearance of `'Mongo'` will be replaced with `'MongoDB'`.

## The `$pull` operator

​	`$pull` is used to remove an element from an array.

​	Example:

```javascript
db.customer.updateOne(
    { _id: 3 },
    { $pull: { knowledge: 'MongoDB' } }
) // removes the element 'MongoDB' from the array `knowledge`
```



## The `$push` operator

​	`$push` is used to add an element to the array.

​	Example:

```javascript
db.customer.updateOne(
    { _id: 3 },
    { $push: { knowledge: "Hadoop" } }
) // adds the element 'Hadoop' at the array `knowledge`
```

