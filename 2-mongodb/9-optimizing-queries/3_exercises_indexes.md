# Exercise - Indexes

1. Show all the documents of the collection `product` from the database `rafael`.

```javascript
use rafael
db.product.find()
// output:
// { "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
// { "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
// { "_id" : 3, "nome" : "mouse", "qtd" : 30, "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-03-02T00:02:16.084Z"), "ts_modificacao" : Timestamp(1646179761, 1) }
// { "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-03-02T00:03:48.523Z") }
```

2. Create the index `query_produto` to search the attribute `nome` in alphabetical order.

```javascript
db.product.createIndex({ nome: 1 }, { name: 'query_product' })
// output:
// {
//     "numIndexesBefore" : 1,
//     "numIndexesAfter" : 2,
//     "createdCollectionAutomatically" : false,
//     "ok" : 1
// }
```

3. Show all the indexes of the collection `product`.

```javascript
db.product.getIndexes()
// output:
// [
//     {
//         "v" : 2,
//         "key" : {
//             "_id" : 1
//         },
//         "name" : "_id_"
//     },
//     {
//         "v" : 2,
//         "key" : {
//             "nome" : 1
//         },
//         "name" : "query_product"
//     }
// ]
```

4. Show all the documents of the collection `product`.

```javascript
db.product.find()
// output:
// { "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
// { "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
// { "_id" : 3, "nome" : "mouse", "qtd" : 30, "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-03-02T00:02:16.084Z"), "ts_modificacao" : Timestamp(1646179761, 1) }
// { "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-03-02T00:03:48.523Z") }
```

5. Visualize the execution plan of the exercise 4.

```javascript
db.product.find().explain()
// output:
// {
//     "explainVersion": "1",
//     "queryPlanner": {
//         "namespace": "rafael.product",
//         "indexFilterSet": false,
//         "parsedQuery": {

//         },
//         "queryHash": "8B3D4AB8",
//         "planCacheKey": "D542626C",
//         "maxIndexedOrSolutionsReached": false,
//         "maxIndexedAndSolutionsReached": false,
//         "maxScansToExplodeReached": false,
//         "winningPlan": {
//             "stage": "COLLSCAN",
//             "direction": "forward"
//         },
//         "rejectedPlans": []
//     },
//     "command": {
//         "find": "product",
//         "filter": {

//         },
//         "$db": "rafael"
//     },
//     "serverInfo": {
//         "host": "3710d3c393f0",
//         "port": 27017,
//         "version": "5.0.6",
//         "gitVersion": "212a8dbb47f07427dae194a9c75baec1d81d9259"
//     },
//     "serverParameters": {
//         "internalQueryFacetBufferSizeBytes": 104857600,
//         "internalQueryFacetMaxOutputDocSizeBytes": 104857600,
//         "internalLookupStageIntermediateDocumentMaxSizeBytes": 104857600,
//         "internalDocumentSourceGroupMaxMemoryBytes": 104857600,
//         "internalQueryMaxBlockingSortMemoryUsageBytes": 104857600,
//         "internalQueryProhibitBlockingMergeOnMongoS": 0,
//         "internalQueryMaxAddToSetBytes": 104857600,
//         "internalDocumentSourceSetWindowFieldsMaxMemoryBytes": 104857600
//     },
//     "ok": 1
// }
```

6. Show all the documents of the collection `product`, using the index `query_produto`.

```javascript
db.product.find().hint({ nome: 1 })
// output:
// { "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
// { "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] }, "data_modificacao" : ISODate("2022-03-02T00:03:48.523Z") }
// { "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
// { "_id" : 3, "nome" : "mouse", "qtd" : 30, "descricao" : { "conexao" : "USB 3.0", "sistema" : [ "Windows 10", "Linux" ] }, "data_modificacao" : ISODate("2022-03-02T00:02:16.084Z"), "ts_modificacao" : Timestamp(1646179761, 1) }
```

7. Visualize the execution plan of the exercise 7.

```javascript
db.product.find().hint({ nome: 1 }).explain()
// output:
// {
//     "explainVersion": "1",
//     "queryPlanner": {
//         "namespace": "test.product",
//         "indexFilterSet": false,
//         "parsedQuery": {

//         },
//         "maxIndexedOrSolutionsReached": false,
//         "maxIndexedAndSolutionsReached": false,
//         "maxScansToExplodeReached": false,
//         "winningPlan": {
//             "stage": "EOF"
//         },
//         "rejectedPlans": []
//     },
//     "command": {
//         "find": "product",
//         "filter": {

//         },
//         "hint": {
//             "nome": 1
//         },
//         "$db": "test"
//     },
//     "serverInfo": {
//         "host": "3710d3c393f0",
//         "port": 27017,
//         "version": "5.0.6",
//         "gitVersion": "212a8dbb47f07427dae194a9c75baec1d81d9259"
//     },
//     "serverParameters": {
//         "internalQueryFacetBufferSizeBytes": 104857600,
//         "internalQueryFacetMaxOutputDocSizeBytes": 104857600,
//         "internalLookupStageIntermediateDocumentMaxSizeBytes": 104857600,
//         "internalDocumentSourceGroupMaxMemoryBytes": 104857600,
//         "internalQueryMaxBlockingSortMemoryUsageBytes": 104857600,
//         "internalQueryProhibitBlockingMergeOnMongoS": 0,
//         "internalQueryMaxAddToSetBytes": 104857600,
//         "internalDocumentSourceSetWindowFieldsMaxMemoryBytes": 104857600
//     },
//     "ok": 1
// }
```

8. Remove the index `query_produto`.

```javascript
db.product.dropIndex({ nome: 1 })
// output:
// { "nIndexesWas" : 2, "ok" : 1 }
```

9. Show all the indexes of the collection `product`.

```javascript
db.product.getIndexes()
// output:
// [ { "v" : 2, "key" : { "_id" : 1 }, "name" : "_id_" } ]
```

