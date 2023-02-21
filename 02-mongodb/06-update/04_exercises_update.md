# Exercises - Update data

1. Show all the documents of the collection `product`.

```javascript
db.product.find()
// output:
// { "_id" : 1, "nome" : "cpu i5", "qtd" : "15" }
// { "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
// { "_id" : 3, "nome" : "mouse", "qtd" : 50, "descricao" : { "conexao" : "USB", "so" : [ "Windows", "Mac", "Linux" ] } }
// { "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB", "armazenamento" : "500GB", "so" : [ "Windows 10", "Windows 8", "Windows 7" ] } }
```

2. Update the value of the attribute `nome` to `'cpu i7'` where `_id: 1`.

```javascript
db.product.updateOne({ _id: 1 }, { $set: { nome: 'cpu i7' }})
// output:
// { "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

3. Update the attribute `qtd` to the `qtd` from the `_id: 1`.

```javascript
db.product.findOne({ _id: 1 }, { qtd: 1 })
// output:
// { "_id" : 1, "qtd" : "15" }

db.product.updateOne({ _id: 1 }, { $set: { qtd: 15 } })
// output:
// { "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

4. Update the value from the attribute `qtd` to `30` in all the documents with `qtd` greater or equal than `30`.

```javascript
db.product.updateOne({ qtd: { $gte: 30 } }, { $set: { qtd: 30 } })
// output:
// { "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

5. Update the name from the attribute `descricao.so` to `'descricao.sistema'`, in all documents.

```javascript
db.product.updateMany({}, { $rename: { 'descricao.so': 'descricao.sistema' } })
// output:
// { "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 2 }
```

6. Update the value from the attribute `descricao.conexao` to `'USB 2.0'` in all documents with `descricao.conexao` equals to `'USB'`.

```javascript
db.product.updateMany({ 'descricao.conexao': 'USB' }, { $set: { 'descricao.conexao': 'USB 2.0' } })
// output:
// { "acknowledged" : true, "matchedCount" : 2, "modifiedCount" : 2 }
```

7. Update the value from the attribute `descricao.conexao` to `'USB 3.0'` in all documents with `descricao.conexao` equals to `'USB 2.0'`. And add the attribute `data_modificacao`, with the update date of the documents.

```javascript
db.product.updateMany(
    { 'descricao.conexao': 'USB 2.0' },
    {
        $set: { 'descricao.conexao': 'USB 3.0' },
        $currentDate: { data_modificacao: true }
    }
)
// output:
// { "acknowledged" : true, "matchedCount" : 2, "modifiedCount" : 2 }
```

8. Update one of the elements of the array `descricao.sistema` from `'Windows'` to `'Windows 10'`, where `_id: 3`.

```javascript
db.product.updateOne(
    { _id: 3, 'descricao.sistema': 'Windows' },
    { $set: { 'descricao.sistema.$': 'Windows 10' } }
)
// output:
// { "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

9. Add the value `'Linux'` to the array `descricao.sistema` where `_id: 4`

```javascript
db.product.updateOne(
    { _id: 4 },
    { $push: { 'descricao.sistema': 'Linux' } }
)
// output:
// { "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

10. Remove the value `'Mac'` from the array `descricao.sistema` on the `_id: 3`, and add the attribute `ts_modificacao`, with the timestamp of the document update.

```javascript
db.product.updateOne(
    { _id: 3 },
    {
        $pull: { 'descricao.sistema': 'Mac' },
        $currentDate: { ts_modificacao: { $type: 'timestamp' } }
    }
)
// output:
// { "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
```

