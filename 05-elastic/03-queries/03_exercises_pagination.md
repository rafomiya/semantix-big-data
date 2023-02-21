# Exercises - Pagination

1. Search on the index `product` the documents with the following attributes:

a) `name="mouse"`
b) `quantity=30`
c) `description="USB"`
d) `name="hd"` e `description="windows"`
e) `name="memória"` e `description="GB"`

```bash
# a
GET product/_search?q=name:mouse
# output:
# {
#   "took" : 4,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 1,
#       "relation" : "eq"
#     },
#     "max_score" : 1.5697745,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 1.5697745,
#         "_source" : {
#           "name" : "mouse",
#           "quantity" : 50,
#           "description" : "com fio USB, compatível com Windows, Mac e Linux"
#         }
#       }
#     ]
#   }
# }

# b
GET product/_search?q=quantity:30
# output:
# {
#   "took" : 2,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 1,
#       "relation" : "eq"
#     },
#     "max_score" : 1.0,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "3",
#         "_score" : 1.0,
#         "_source" : {
#           "name" : "memória ram",
#           "quantity" : 30,
#           "description" : "8GB, DDR4"
#         }
#       }
#     ]
#   }
# }

# c
GET product/_search?q=description:USB
# output:
# {
#   "took" : 1,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 2,
#       "relation" : "eq"
#     },
#     "max_score" : 0.6739812,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 0.6739812,
#         "_source" : {
#           "name" : "mouse",
#           "quantity" : 50,
#           "description" : "com fio USB, compatível com Windows, Mac e Linux"
#         }
#       },
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "2",
#         "_score" : 0.6011622,
#         "_source" : {
#           "name" : "hd",
#           "quantity" : 20,
#           "description" : "Interface USB 2.0, 500GB, Sistema: Windows 10, Windows 8, Windows 7"
#         }
#       }
#     ]
#   }
# }

# d
GET product/_search?q=name:hd&q=description:windows
# output:
# {
#   "took" : 2,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 2,
#       "relation" : "eq"
#     },
#     "max_score" : 1.1103506,
#     "hits" : [
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "2",
#         "_score" : 1.1103506,
#         "_source" : {
#           "name" : "hd",
#           "quantity" : 20,
#           "description" : "Interface USB 2.0, 500GB, Sistema: Windows 10, Windows 8, Windows 7"
#         }
#       },
#       {
#         "_index" : "product",
#         "_type" : "_doc",
#         "_id" : "1",
#         "_score" : 0.6739812,
#         "_source" : {
#           "name" : "mouse",
#           "quantity" : 50,
#           "description" : "com fio USB, compatível com Windows, Mac e Linux"
#         }
#       }
#     ]
#   }
# }

# e
GET product/_search?q=name:memória&q=description:GB
# output:
# {
#   "took" : 1,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 0,
#       "relation" : "eq"
#     },
#     "max_score" : null,
#     "hits" : [ ]
#   }
# }

```

2. Pesquisar todos os índices, limitando a pesquisa em 5 documentos em cada página e visualizar a 4 página (Documentos entre 16 á 20 )

```bash
GET _all/_search?size=5&from=15
# output:
# {
#   "took" : 6,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 8,
#     "successful" : 8,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 388,
#       "relation" : "eq"
#     },
#     "max_score" : 1.0,
#     "hits" : [
#       {
#         "_index" : ".kibana_1",
#         "_type" : "_doc",
#         "_id" : "ui-metric:console:GET_get",
#         "_score" : 1.0,
#         "_source" : {
#           "ui-metric" : {
#             "count" : 1
#           },
#           "type" : "ui-metric",
#           "updated_at" : "2022-03-31T03:43:16.686Z"
#         }
#       },
#       {
#         "_index" : ".kibana_1",
#         "_type" : "_doc",
#         "_id" : "ui-metric:console:DELETE_delete",
#         "_score" : 1.0,
#         "_source" : {
#           "ui-metric" : {
#             "count" : 1
#           },
#           "type" : "ui-metric",
#           "updated_at" : "2022-03-31T03:44:47.159Z"
#         }
#       },
#       {
#         "_index" : ".kibana_1",
#         "_type" : "_doc",
#         "_id" : "ui-metric:console:POST_index",
#         "_score" : 1.0,
#         "_source" : {
#           "ui-metric" : {
#             "count" : 4
#           },
#           "type" : "ui-metric",
#           "updated_at" : "2022-03-31T03:44:47.159Z"
#         }
#       },
#       {
#         "_index" : ".kibana_1",
#         "_type" : "_doc",
#         "_id" : "config:7.9.2",
#         "_score" : 1.0,
#         "_source" : {
#           "config" : {
#             "buildNum" : 33984,
#             "defaultIndex" : "203cf040-b0b0-11ec-a341-df094b430206"
#           },
#           "type" : "config",
#           "references" : [ ],
#           "migrationVersion" : {
#             "config" : "7.9.0"
#           },
#           "updated_at" : "2022-03-31T05:05:05.044Z"
#         }
#       },
#       {
#         "_index" : ".kibana_1",
#         "_type" : "_doc",
#         "_id" : "application_usage_daily:home:2022-03-31",
#         "_score" : 1.0,
#         "_source" : {
#           "application_usage_daily" : {
#             "appId" : "home",
#             "timestamp" : "2022-03-31T00:00:00.000Z",
#             "minutesOnScreen" : 1.8615,
#             "numberOfClicks" : 29
#           },
#           "type" : "application_usage_daily",
#           "references" : [ ],
#           "updated_at" : "2022-03-31T04:54:50.757Z"
#         }
#       }
#     ]
#   }
# }
```
