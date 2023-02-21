# Testing Analyzers

​	To test an analyzer:

```bash
POST _analyze
{
  "analyzer": "standard",
  "text": "Elasticsearch with Hadoop example usages"
}
```

```bash
POST _analyze
{
  "analyzer": "simple",
  "text": "Elasticsearch with Hadoop example usages"
}
```

​	Both of the examples above have pretty much the same output, because the `text` has no numbers.

```bash
# output:
# {
#   "tokens" : [
#     {
#       "token" : "elasticsearch",
#       "start_offset" : 0,
#       "end_offset" : 13,
#       "position" : 0
#     },
#     {
#       "token" : "with",
#       "start_offset" : 14,
#       "end_offset" : 18,
#       "position" : 1
#     },
#     {
#       "token" : "hadoop",
#       "start_offset" : 19,
#       "end_offset" : 25,
#       "position" : 2
#     },
#     {
#       "token" : "example",
#       "start_offset" : 26,
#       "end_offset" : 33,
#       "position" : 3
#     },
#     {
#       "token" : "usages",
#       "start_offset" : 34,
#       "end_offset" : 40,
#       "position" : 4
#     }
#   ]
# }
```

​	Another example:

```bash
POST _analyze
{
    "analyzer": "english",
    "text": "Elasticsearch with Hadoop example usages"
}
# output:
# {
#   "tokens" : [
#     {
#       "token" : "elasticsearch",
#       "start_offset" : 0,
#       "end_offset" : 13,
#       "type" : "<ALPHANUM>",
#       "position" : 0
#     },
#     {
#       "token" : "hadoop",
#       "start_offset" : 19,
#       "end_offset" : 25,
#       "type" : "<ALPHANUM>",
#       "position" : 2
#     },
#     {
#       "token" : "exampl",
#       "start_offset" : 26,
#       "end_offset" : 33,
#       "type" : "<ALPHANUM>",
#       "position" : 3
#     },
#     {
#       "token" : "usag",
#       "start_offset" : 34,
#       "end_offset" : 40,
#       "type" : "<ALPHANUM>",
#       "position" : 4
#     }
#   ]
# }
```
