# Indexes

​	Indexes are a recurse used to optimize queries in many databases, including MongoDB.

​	Basically, indexes are special data structures that stores the data ordered by a specific attribute, somehow limiting the amount of documents to be scanned to perform a query.

​	Example:

![Diagram of a query that uses an index to select and return sorted results. The index stores ``score`` values in ascending order. MongoDB can traverse the index in either ascending or descending order to return sorted results.](https://docs.mongodb.com/manual/images/index-for-sort.bakedsvg.svg)

## Default index

​	By default, MongoDB already have a built-in index: the `_id` attribute.

- The used of this index is highly encouraged by the MongoDB docs.
  - If the database doesn't use the default `ObjectId` object as id, the application must guarantee its uniqueness.

## Creating indexes

```javascript
db.collection.createIndex({ <attribute>: <value> }, <options>)
```

- `attribute`: the field to be used as index.
- `value`: `1` or `-1`, whether the order the order order ascending or descending, respectively.
- `options`: optional parameter, specifying more options of the index.

​	Example:

```javascript
db.customer.createIndex({ name: 1 })
// output:
// {
//     "createdCollectionAutomatically": false,
//     "numIndexesBefore": 1,
//     "numIndexesAfter": 2,
//     "ok": 1
// }
```

### Other options

#### List indexes

​	To see all the indexes from a collection, we use the method `getIndexes()`:

```javascript
db.customer.getIndexes()
// output:
[
    {
        "v": 2,
        "key": {
            "_id": 1
        },
        "name": "_id_"
    },
    {
        "v": 2,
        "key": {
            "name": 1
        },
        "name": "name_1"
    }
]
```

#### Name indexes

​	The default name of the index follows the pattern `attribute_value_attribute_value<...>`, extending as much attributes there are on the index. This name can be changed on the index creation:

```javascript
db.customer.createIndex({ age: -1, name: 1 }, { name: 'old_to_young' })
```

#### Uniqueness

​	If our attribute is unique, just like the `_id`, we can define it on the options when creating the index:

```javascript
db.customer.createIndex({ user_id: 1 }, { unique: true })
```

## Remove indexes

- `db.collection.dropIndex(<key>)`: deletes a specific index.
  - Example: `db.customer.dropIndex({ name: 1 })`
- `db.collection.dropIndexes()`: drops all the indexes from the collection.