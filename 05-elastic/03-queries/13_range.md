# Range Queries

​	Range queries are queries in which the values are filtered based on a range. The four attributes used to control these ranges are:

- `gte`: greater than or equals.
- `gt`: greater than.
- `lte`: lesser than or equals.
- `lt`: lesser than.

​	Example:

```bash
GET employee/_search
{
  "query": {
    "range": {
      "age": {
        "gte": 18,
        "lte": 60
      }
    }
  }
}
# retrieves all the employees with age between 18 and 60
```
