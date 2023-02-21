# Aggregations

​	There are types of aggregations in MongoDB.

### Single purpose

- Simpler, but more limited.
- Examples:
  - `count`: `db.collection.count(<filter>)`.
  - `distinct`: `db.collection.distinct(<attribute>)`
  - `estimatedDocumentCount`: `db.collection.estimatedDocumentCount()`
    - Uses metadata to return the count of a search.

​	Example:

```javascript
// count:
db.collection.count({<filter>})
// is equivalent to
db.collection.find({<filter>}).count()

// distinct:
db.collection.distinct('<attribute>')

// estimatedDocumentCount:
db.collection.estimatedDocumentCount()
```

### Map-reduce operations

- Traditional way of handling aggregations with big data.
- Works on top of javascript functions.
- Not so recommended. It was replaced by the aggregation pipelines.

### Aggregation pipelines

- Groups values from many documents and returns one computed result by group, based on an operation made in each group.

​	Syntax:

```javascript
db.collection.aggregate([
  { '<stage>': <parameters> }
])
```

- `stage`: basically, the operation to be done. The output of a stage is passed to the next stage.
- `parameters`: the specifications of how the stage must be calculated, grouped or whatever it does. This can vary a lot.
