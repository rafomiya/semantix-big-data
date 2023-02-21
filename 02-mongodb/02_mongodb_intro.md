# MongoDB

​	MongoDB is a distributed, NoSQL and document oriented database, using the BSON (binary JSON) file format. It also allows flexible schemes, and was made to fit cases in which we need to handle a high volumetry of data.

## History

​	It was created in 2007 by the company 10gen, today called MongoDB Inc. Although, its was first released only in 2009, 

## Flexible schema

​	Many say that MongoDB doesn't even have a schema, since you can always alter or add/remove your fields from a collection, differently from what would happen in a relational database.

## Versions

- MongoDB Community: free and [open source](https://github.com/mongodb/mongo/).
- MongoDB Enterprise:
  - Isn't free :pensive:
  - Has additional resources, very important for companies:
    - LDAP
    - Kerberos
    - Disk cryptography

​	MongoDB releases are documented and explained [here](https://docs.mongodb.com/manual/release-notes/).

## Structure

| Relational | MongoDB                   |
| ---------- | ------------------------- |
| Database   | Database                  |
| Table      | Collection                |
| Row        | Document                  |
| Column     | Attribute (never collumn) |
| Index      | Index                     |

​	Since version 3.2, schemes validations are supported, and since version 4.2, distributed transactions are also supported. However, transactions aren't to be used in every part of your application, only in specific points.

## JSON and BSON

### JSON

​	JSON stands for Javascript Object Notation, meaning it is the way Javascript represents objects' properties, following a key-value structure.
- Key: string.
- Value: string, number, object.
- Flexible schema.
- Replaced XML place in web development.


​	Example:

```json
{
    "_id": 1,
    "name": "Rafael",
    "phone": {
        "residential": "53753642846",
        "cellphone": "14365823748"
    }
}
```

### BSON

​	BSON is a binary and expanded JSON file format.

- Isn't a text file, so it is much cheaper to store.
- Implements data types that doesn't exist on JSON, such as date time and floating points.

