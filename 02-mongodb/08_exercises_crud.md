# Exercises - CRUD

1. Create the collection `test` on the database `rafael`.

```javascript
use rafael
db.createCollection('test')
// output:
// { "ok" : 1 }
```

2. Insert the following documents:

- Attribute: `user`, value: `'Semantix'`.
- Attribute: `date_access`, value: current date in ISODate.

```javascript
db.test.insertOne({
    user: 'Semantix',
    date_access: new Date()
})
// output:
// {
//         "acknowledged" : true,
//         "insertedId" : ObjectId("621ee1048313ee129dcb3703")
// }
```

3. Query all the documents where `date_access >= 2020`

```javascript
db.test.find({ date_access: { $gte: new Date('2020') } })
// output:
// { "_id" : ObjectId("621ee1048313ee129dcb3703"), "user" : "Semantix", "date_access" : ISODate("2022-03-02T03:14:12.788Z") }
```

4. Update the field `date_access` to timestamp with the value of update of the user Semantix.

```javascript
db.test.updateOne({ user: 'Semantix' }, { $currentDate: { date_access: { $type: 'timestamp' } } })
// output:
// { "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

5. Query all documents.

```javascript
db.test.find().pretty()
// output:
// {
//         "_id" : ObjectId("621ee1048313ee129dcb3703"),
//         "user" : "Semantix",
//         "date_access" : Timestamp(1646190881, 1)
// }
```

6. Delete the created document by `_id`.

```javascript
db.test.deleteOne({ _id: ObjectId("621ee1048313ee129dcb3703") })
// output:
// { "acknowledged" : true, "deletedCount" : 1 }
```

7. Delete the collection.

```javascript
db.test.drop()
// output:
// true
```

