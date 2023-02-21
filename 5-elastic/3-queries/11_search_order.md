# Search Order

​	There are many factors to be considered when defining the search order through our documents, such as:

- How many times the term appears on the attribute.
- Attribute's length.
- Term's length.
- How many times the term appears through all the documents.

​	Example:

```bash
GET client/_search
{
  "query": {
    "match": {
      "knowledge": "sqoop hive impala elk"
    }
  }
}
```

### Search operator

​	By default, the search operator is `or`. To change this, we can specify `"operator": "and"`:

```bash
GET client/_search
{
  "query": {
    "match": {
      "knowledge": {
        "query": "sqoop hive impala elk",
        "operator": "and"
      }
    }
  }
}
```

### Defining a minimum match

​	We can define how much of our query must mandatorily match our results:

```bash
GET client/_search
{
  "query": {
    "match": {
      "knowledge": {
        "query": "sqoop hive impala elk",
        "minimum_should_match": "50%"
      }
    }
  }
}
```

​	The value of this attribute can be passed as percentage or integer, depending on what is best for our use cases.

### Searching on multiple attributes

​	It is possible to search the same value on more than one attribute:

```bash
GET client/_search
{
  "query": {
    "bool": {
      "should": [
        { "match": { "address": "Paulista"} },
        { "match": { "city": "Paulista"} },
        { "match": { "state": "Paulista"} }
      ]
    }
  }
}
# OR
GET client/_search
{
  "query": {
    "multi_match": {
      "query": "Paulista",
      "type": "most_fields",
      "fields": ["address", "city", "state"]
    }
  }
}
# obs: can't be used with `operator` or `minimum_should_match`
```
