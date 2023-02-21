# Joins in MongoDB

​	To combine the attributes from two collections in one single search, we can use the `$lookup` aggregation pipeline stage. It performs a left outer join in our collections, similar to what would happend in a ordinary RDBMS table.

​	Syntax:

```javascript
db.collection.aggregate([
    {
        $lookup: {
            from: '<collection>',
            localField: '<localAttr>',
            foreignField: '<foreignAttr>',
            as: '<outputAttributeName>'
        }
    }
])
```

​	Example:

```javascript
db.employee.aggregate([
    {
        $lookup: {
            from: 'sales',
            localField: 'employee_id',
            foreignField: 'employee_id',
            as: 'employeeSales'
        }
    },
    {
        $project: {
            _id: 0,
            cod_func: 1,
            'employeeSales.customer_id': 1
        }
    }
])
```