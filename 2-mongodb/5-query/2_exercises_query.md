# Exercises - Query documents

1. Show all the documents on collection `product`.

```javascript
db.product.find().pretty()
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

2. Query the collection `product` with the following parameters:

    1. `nome 'mouse'`

    ```javascript
    db.product.find({ nome: 'mouse' }).pretty()
    // output:
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
    ```

    2. `qtd == 20` and show only the `nome` field.

    ```javascript
    db.product.find({ qtd: { $eq: 20 } }, { _id: 0, nome: 1 }).pretty()
    // output:
    // { "nome" : "hd externo" }
    ```

    3. `qtd <= 20` and show only the fields `nome` and `_id`.

    ```javascript
    db.product.find({ qtd: { $lte: 20 } }, { nome: 1 }).pretty()
    // output:
    // { "_id" : 2, "nome" : "memória ram" }
    // { "_id" : 4, "nome" : "hd externo" }
    ```

    4. `qtd` between `10` e `20`.

    ```javascript
    db.product.find({ qtd: { $gte: 10, $lte: 20 } }).pretty()
    // output:
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

    5. `conexao == 'USB'` and don't show the fields `_id` and `qtd`.

    ```javascript
    db.product.find({ 'descricao.conexao': 'USB' }, { _id: 0, qtd: 0 }).pretty()
    // output:
    // {
    //         "nome" : "mouse",
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
    //         "nome" : "hd externo",
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

    6. `so` that contains `"Windows"` or `"Windows 10"`.

    ```javascript
    db.product.find({ 'descricao.so': { $in: [ "Windows", "Windows 10" ] } }, {  }).pretty()
    // output:
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
