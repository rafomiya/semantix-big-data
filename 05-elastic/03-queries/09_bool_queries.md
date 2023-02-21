# Bool Queries

​	Bool queries are usually used to filter the data from big datasets. It offers a flexible structure to make complex queries.
​	These are the main attributes of a bool query:

- `must`: equivalent to the `and` (&&) operator.
- `should`: equivalent to the `or` (||) operator.
- `must_not` equivalent to a `not and` (!&&) operation.
- `filter`: used to filter the data **before** attend to the other clauses.

​	Examples:

```bash
GET client/_search
{
  "query": { # always starts with "query".
    "bool": { # declares a bool query
      "must": [{...}],
      "must_not": [{...}],
      "should": [{...}],
      "filter": [{...}]
    }
  }
}"
```

```bash
GET client/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "state": "sp" } },
        { "match": { "is_active": true } }
      ]
    }
  }
}
```

```bash
GET client/_search
{
  "query": {
    "bool": {
      "must": { "match": { "department": "sales" } },
      "should": [
        { "match": { "tags": "immutable" } },
        { "match": { "tags": "large scale" } }
      ],
      "must_not": { "match": { "is_active": false } }
    }
  }
}
```
