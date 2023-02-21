# MongoDB Commands

## Databases

- `show dbs`: lists existing databases.
- `use <dbname>`: creates/uses a database.
- `db`: displays the current database.
- `db.dropDatabase()`: drops the current database.

​	OBS: if you create a database and it wasn't included on the `show dbs` command, it is probably because the database is empty (has no documents).

## Collections

- `db.createCollection('<collectionname>')`: creates a collection.
  - Returns `{ "ok" : 1 }` if everything went right.
- `show collections`: lists the collections from the current database.
- `db.collection.drop()`: drops the specified collection.
- `db.collection.rename('<newname>')`: renames the collection to the specified new name.

### Insertion

- `db.collection.insertOne({<json>})`: inserts a document into the collection.
- `db.collection.insertMany([{<json>}, {<json>}, {<json>}])`: inserts a series of documents into the collection.

#### Data types

- `ObjectId`
- `String`
- Numbers
  - `Long`
  - `Int`
  - `Decimal`
  - `Double`
- `Boolean`
- `Array`
- `Date`
- `Null`
- `Regex`
- `Timestamp`

​	To see more data types and specifications, read [this](https://docs.mongodb.com/manual/reference/bson-types).

#### Nested documents

​	JSON and BSON supports nested documents. That means that the value of a key can be another object, containing its own keys and values.

​	Example:

```json
db.customer.insertOne({
    "name": "Rafael",
    "knowledge": ["big data", "spark", "mongodb"],
    "address": {
    	"street": "some street",
    	"number": "19B",
    	"city": "los angeles"
    }
})
```

### Reading

- `db.collection.find(<query>, <fields>)`: displays the results of the query, showing only the specified fields.
- `db.collection.findOne(<query>, <fields>)`: displays only the first result of the query, showing only the specified fields.

