# Exercise - Regex

1. Show all the documents of the collection `product` from the database `rafael`.

```javascript
use rafael
db.product.find({})
```

2. Show all the documents with the attribute `nome` containing the word `'cpu'`.

```javascript
db.product.find({ nome: { $regex: /cpu/ } })
// output:
// { "_id" : 1, "nome" : "cpu i7", "qtd" : 15 }
```

3. Show all the documents with the attribute `nome` starting with `'hd'`, displaying only the fields `nome` and `qtd`.

```javascript
db.product.find({ nome: { $regex: /^cpu/ } }, { _id: 0, nome: 1, qtd: 1 })
// output:
// { "nome" : "cpu i7", "qtd" : 15 }
```

4. Show all the documents with the attribute `descricao.armazenamento` ending with `'GB'` or `'gb'`, displaying the fields `nome` and `descricao`.

```javascript
db.product.find({ 'descricao.armazenamento': { $regex: /GB$/i } }, { _id: 0, nome: 1, descricao: 1 })
// output:
// { "nome" : "memória ram", "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
// { "nome" : "hd externo", "descricao" : { "conexao" : "USB 3.0", "armazenamento" : "500GB", "sistema" : [ "Windows 10", "Windows 8", "Windows 7", "Linux" ] } }
```

5. Show all the documents with the attribute `nome` containing the word `'memória'`, ignoring the letter `'o'`.

```javascript
db.product.find({ nome: { $regex: /mem.ria/i } })
// output:
// { "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
```

6. Show all the documents with the attribute `qtd` containing letters instead of numbers.

```javascript
db.product.find({ qtd: { $regex: /[a-z]/i } })
// output:
```

7. Show all the documents with the attribute `descricao.sistema` containing exactly the word `'Windows'`.

```javascript
db.product.find({ 'descricao.sistema': 'Windows' })
// output:
```

