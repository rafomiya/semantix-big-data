# Query Documents

## `db.collection.find`

​	The most basic way to query a collection is through the `find` command:

```javascript
db.collection.find({<querycriterion>}, {<projection>})
```

### `querycriterion`

This parameter defines the operator to be used with each field:
- Syntax:
  - `{ <attribute>: <value> }`
  - `{ <attribute>: { <operator>: <value> } }`

#### Operators

- `$eq`:
  - `==`
  - `{ name: 'Rafael' }`
  - `{ name: { $eq: 'Rafael' } }`
- `$ne`:
  - `!=`
  - `{ amount: { $ne: 0 } }`
- `$gt`:
  - `>`
  - `{ amount: { $gt: 0 } }`
- `$gte`:
  - `>=`
  - `{ amount: { $gte: 1 } }`
- `$lt`:
  - `<`
  - `{ price: { $lt: 100.0 } }`
- `$lte`:
  - `<=`
  - `{ price: { $lte: 150.0 } }`
- `$in`:
  - contained in list.
  - `{ os: { $in: [ "Linux", "MacOS" ] } }`
- `$nin`:
  - not contained in list.
  - `{ products: { $nin: [ "mouse", "headset", "monitor" ] } }`
- `$not`: it is a little bit obsolete, since all the operators already have a "negative" version.
  - not operator.
    - `{ price: { $not: { $eq: 24 }}}`
    - `{ price: { $ne: 24 }}`

#### Example

  - `{}`: returns all the documents.
  - `{ nome: "John" }`: returns all the documents **where** the `nome` is `"John"`.
  - `{ "address.city": "New York" }`
  - `{ age: { $lt: 18 } }`: returns all the documents where the age is lesser than 18.

### `projection`

​	This parameter defines which attributes are gonna appear on the results of the query:

- Syntax:
  - `{ <attribute>: 0 }`: won't appear in results.
  - `{ <attribute>: 1 }`: will appear in results

#### Example

  - `{}`
  - `{ name: 0, age: 1 }`
  - `{ name: 1 }`
  - `{ _id: 0, name: 1 }`
