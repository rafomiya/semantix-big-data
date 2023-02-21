# Exercises - MongoDB Commands

1. Create a database `rafael`.

```javascript
use rafael
// output:
// switched to db rafael
```

2. List the databases.

```javascript
show dbs
// output:
// admin   0.000GB
// config  0.000GB
// local   0.000GB
```

3. Create a collection `product` on the database `rafael`.

```javascript
db.createCollection('product')
// output:
// { "ok" : 1 }
```

4. List the databases.

```javascript
show dbs
// output:
// admin   0.000GB
// config  0.000GB
// local   0.000GB
// rafael  0.000GB
```

5. List the collections.

```javascript
show collections
// output:
// product
```

6. Insert the following documents into the collection `product`:

- `_id: 1, "nome": "cpu i5", "qtd": "15"`
- `_id: 2, nome: "memória ram", qtd: 10, descricao: {armazenamento: "8GB”, tipo:"DDR4"}`
- `_id: 3, nome: "mouse", qtd: 50, descricao: {conexao: "USB”, so: ["Windows”, "Mac”, "Linux"]}`
- `_id: 4, nome: "hd externo", "qtd": 20, descricao: {conexao: "USB”, armazenamento: "500GB”, so: ["Windows 10”, "Windows 8”, "Windows 7”]}`

```javascript
db.product.insertMany([
    {
		_id: 1,
		"nome": "cpu i5",
		"qtd": "15"
    },
    {
		_id: 2,
		nome: "memória ram",
		qtd: 10,
		descricao: {
			armazenamento: "8GB",
			tipo: "DDR4"
        }
    },
    {
		_id: 3,
		nome: "mouse",
		qtd: 50,
		descricao: {
        	conexao: "USB",
        	so: [ "Windows", "Mac", "Linux" ]
        }
    },
    {
		_id: 4,
		nome: "hd externo",
		"qtd": 20,
		descricao: {
			conexao: "USB",
			armazenamento: "500GB",
			so: [ "Windows 10", "Windows 8", "Windows 7" ]
        }
	}
])
// output:
// { "acknowledged" : true, "insertedIds" : [ 1, 2, 3, 4 ] }
```

7. Show the documents.

```javascript
db.product.find().pretty()
// output:
// { "_id" : 1, "nome" : "cpu i5", "qtd" : "15" }
// {
//         "_id" : 2,
//         "nome" : "memória ram",
//         "qtd" : 10,
//         "descricao" : {
//                 "armazenamento" : "8GB",
//                 "tipo" : "DDR4"
//         }
// }
// {
//         "_id" : 3,
//         "nome" : "mouse",
//         "qtd" : 50,
//         "descricao" : {
//                 "conexao" : "USB",
//                 "so" : [
//                         "Windows",
//                         "Mac",
//                         "Linux"
//                 ]
//         }
// }
// {
//         "_id" : 4,
//         "nome" : "hd externo",
//         "qtd" : 20,
//         "descricao" : {
//                 "conexao" : "USB",
//                 "armazenamento" : "500GB",
//                 "so" : [
//                         "Windows 10",
//                         "Windows 8",
//                         "Windows 7"
//                 ]
//         }
// }
```
