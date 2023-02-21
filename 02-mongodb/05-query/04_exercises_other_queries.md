# Exercises - Other Query Options

1. Show all the documents of the collection `product`.

```javascript
db.product.find()
```

2. Do the following queries on the collection `product`:

    1. Show all the documents sorted by `nome` in alphabetical order.

    ```javascript
    db.product.find().sort({ nome: 1 })
    // output:
    // { "_id" : 1, "nome" : "cpu i5", "qtd" : "15" }
    // { "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB", "armazenamento" : "500GB", "so" : [ "Windows 10", "Windows 8", "Windows 7" ] } }
    // { "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
    // { "_id" : 3, "nome" : "mouse", "qtd" : 50, "descricao" : { "conexao" : "USB", "so" : [ "Windows", "Mac", "Linux" ] } }
    ```

    2. Show the first 3 documents sorted by `nome` and `qtd`.

    ```javascript
    db.product.find().sort({ nome: 1, qtd: 1 }).limit(3)
    // output:
    // { "_id" : 1, "nome" : "cpu i5", "qtd" : "15" }
    // { "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB", "armazenamento" : "500GB", "so" : [ "Windows 10", "Windows 8", "Windows 7" ] } }
    // { "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
    ```

    3. Show one document that contains `conexao` equals to `'USB'`.

    ```javascript
    db.product.findOne({ 'descricao.conexao': 'USB' })
    // output:
    // {
    //     "_id" : 3,
    //     "nome" : "mouse",
    //     "qtd" : 50,
    //     "descricao" : {
    //         "conexao" : "USB",
    //         "so" : [
    //             "Windows",
    //             "Mac",
    //             "Linux"
    //         ]
    //     }
    // }
    ```

    4. Show the documents that contains the attribute `conexao` equals to `'USB'` and `qtd` lesser than `25`.

    ```javascript
    db.product.find({ 'descricao.conexao': 'USB', qtd: { $lt: 25 } })
    // output:
    // { "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB", "armazenamento" : "500GB", "so" : [ "Windows 10", "Windows 8", "Windows 7" ] } }
    ```

    5. Show the documents that contains the attribute `conexao` equals to `'USB'` or `qtd` lesser than `25`.

    ```javascript
    db.product.find({
        $or: [
            { 'descricao.conexao': 'USB' },
            { qtd: { $lt: 25 } }
        ]
    })
    // output:
    // { "_id" : 2, "nome" : "memória ram", "qtd" : 10, "descricao" : { "armazenamento" : "8GB", "tipo" : "DDR4" } }
    // { "_id" : 3, "nome" : "mouse", "qtd" : 50, "descricao" : { "conexao" : "USB", "so" : [ "Windows", "Mac", "Linux" ] } }
    // { "_id" : 4, "nome" : "hd externo", "qtd" : 20, "descricao" : { "conexao" : "USB", "armazenamento" : "500GB", "so" : [ "Windows 10", "Windows 8", "Windows 7" ] } }
    ```

    6. Show only the `_id` of documents with the attribute `conexao` equals to `'USB'` or `qtd` lesser than `25`.

    ```javascript
    db.product.find(
        {
            $or: [{ 'descricao.conexao': 'USB' }, { qtd: { $lt: 25 } }],
        },
        { _id: 1 }
    )
    // output:
    // { "_id" : 2 }
    // { "_id" : 3 }
    // { "_id" : 4 }
    ```
