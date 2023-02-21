# Queries and Filters

​	Queries and filters are the ways of doing searches on Elasticsearch.

## Queries

​	On queries, all the results are ordered by a score, defining how much the results corresponds with the search parameters, and the output is not stored in cache.

​	There are many types of queries, such as `term`, `terms`, `range`, `match`, `exists`, etc. All of them calculates a `_score` attribute. If you don't want the score of the results, you can add the `constant_score` option. This way, all the `_score`s will be 1.

​	Examples:

```bash
GET client/_search
{
  "query": {
    "term": {
      "name": "joão"
    }
  }
}
# output:
# {
#   "took": 5,
#   ...
#   "hits": [
#     {
#       "_index": "client",
#       "_type": "_doc",
#       "_id": 1,
#       "_score": 0.9808291,
#       "_source": {
#         "name": "João",
#         "age": 20
#       }
#     }
#   ]
# }
```

```bash
GET client/_search
{
  "query": {
    "terms": {
      "age": [30, 20]
    }
  }
}
# output:
# {
#   "took": 5,
#   ...
#   "hits": [
#     {
#       "_index": "client",
#       "_type": "_doc",
#       "_id": 1,
#       "_score": 0.9808291,
#       "_source": {
#         "name": "João",
#         "age": 20
#       }
#     }
#   ]
# }
```

## Filters

​	When working with filters, there is no such idea of a score. The only information retrieved is if the document corresponds to the document or not. And, for performance reasons, filter's data is stored on the cache.

​	Example:

```bash
GET client/_search
{
  "query": {
    "constant_score": {
      "filter": {
        "term": {
          "name": "João"
        }
      }
    }
  }
}
# output:
# {
#   "took": 1,
#   ...
#   "hits": [
#     {
#       "_index": "client",
#       "_type": "_doc",
#       "_id": 1,
#       "_score": 1.0,
#       "_source": {
#         "name": "João",
#         "age": 20
#       }
#     }
#   ]
# }
```

​	In this search, the `took` attribute shows that this search was faster than the equivalent query.
