# Exercises - Time Range

1. Verify if the index `population` exists.

```bash
HEAD population
# output:
# 200 - OK
```

2. Execute the queries on the index `population`.

a) Show the documents with the attribute `Total Population` lesser than 100.

```bash
GET population/_search
{
  "query": {
    "range": {
      "Total Population": {
        "lt": 100
      }
    }
  }
}
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
#       "value" : 9,
#       "relation" : "eq"
#     },
#     "max_score" : 1.0,
#     "hits" : [
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "AaNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 1,
#           "Total Households" : 1,
#           "Total Females" : 1,
#           "Zip Code" : 91371,
#           "Median Age" : 73.5,
#           "Total Males" : 0,
#           "Average Household Size" : 1.0
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "PqNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 15,
#           "Total Households" : 0,
#           "Total Females" : 2,
#           "Zip Code" : 90071,
#           "Median Age" : 45.5,
#           "Total Males" : 13,
#           "Average Household Size" : 0.0
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "QaNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 0,
#           "Total Households" : 0,
#           "Total Females" : 0,
#           "Zip Code" : 90079,
#           "Median Age" : 0.0,
#           "Total Males" : 0,
#           "Average Household Size" : 0.0
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "Q6Nl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 0,
#           "Total Households" : 0,
#           "Total Females" : 0,
#           "Zip Code" : 90090,
#           "Median Age" : 0.0,
#           "Total Males" : 0,
#           "Average Household Size" : 0.0
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "RaNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 3,
#           "Total Households" : 2,
#           "Total Females" : 1,
#           "Zip Code" : 90095,
#           "Median Age" : 52.5,
#           "Total Males" : 2,
#           "Average Household Size" : 1.5
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "eKNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 0,
#           "Total Households" : 0,
#           "Total Females" : 0,
#           "Zip Code" : 90506,
#           "Median Age" : 0.0,
#           "Total Males" : 0,
#           "Average Household Size" : 0.0
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "mqNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 0,
#           "Total Households" : 0,
#           "Total Females" : 0,
#           "Zip Code" : 90747,
#           "Median Age" : 0.0,
#           "Total Males" : 0,
#           "Average Household Size" : 0.0
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "qKNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 0,
#           "Total Households" : 0,
#           "Total Females" : 0,
#           "Zip Code" : 90831,
#           "Median Age" : 0.0,
#           "Total Males" : 0,
#           "Average Household Size" : 0.0
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "_aNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 0,
#           "Total Households" : 0,
#           "Total Females" : 0,
#           "Zip Code" : 91608,
#           "Median Age" : 0.0,
#           "Total Males" : 0,
#           "Average Household Size" : 0.0
#         }
#       }
#     ]
#   }
# }
```

b) Show the documents with the attribute `Median Age` greater than 70.

```bash
GET population/_search
{
	"query": {
		"range": {
			"Median Age": {
				"gt": 70
			}
		}
	}
}
# output:
# {
#   "took" : 3,
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
#     "max_score" : 1.0,
#     "hits" : [
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "AaNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 1,
#           "Total Households" : 1,
#           "Total Females" : 1,
#           "Zip Code" : 91371,
#           "Median Age" : 73.5,
#           "Total Males" : 0,
#           "Average Household Size" : 1.0
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "taNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 156,
#           "Total Households" : 114,
#           "Total Females" : 105,
#           "Zip Code" : 91046,
#           "Median Age" : 74.0,
#           "Total Males" : 51,
#           "Average Household Size" : 1.37
#         }
#       }
#     ]
#   }
# }
```

c) Show the documents 50 (`Zip Code`: 90056) to 60 (`Zip Code`: 90067).

```bash
GET population/_search
{
	"query": {
		"range": {
			"Zip Code": {
				"gte": 90056,
				"lte": 90067
			}
		}
	}
}
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
#       "value" : 11,
#       "relation" : "eq"
#     },
#     "max_score" : 1.0,
#     "hits" : [
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "MaNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 7827,
#           "Total Households" : 3371,
#           "Total Females" : 4391,
#           "Zip Code" : 90056,
#           "Median Age" : 48.4,
#           "Total Males" : 3436,
#           "Average Household Size" : 2.32
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "MqNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 44998,
#           "Total Households" : 15658,
#           "Total Females" : 20698,
#           "Zip Code" : 90057,
#           "Median Age" : 31.2,
#           "Total Males" : 24300,
#           "Average Household Size" : 2.81
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "M6Nl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 3223,
#           "Total Households" : 892,
#           "Total Females" : 1668,
#           "Zip Code" : 90058,
#           "Median Age" : 26.0,
#           "Total Males" : 1555,
#           "Average Household Size" : 3.6
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "NKNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 40952,
#           "Total Households" : 9596,
#           "Total Females" : 21329,
#           "Zip Code" : 90059,
#           "Median Age" : 25.7,
#           "Total Males" : 19623,
#           "Average Household Size" : 4.19
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "NaNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 26872,
#           "Total Households" : 6892,
#           "Total Females" : 13823,
#           "Zip Code" : 90061,
#           "Median Age" : 28.4,
#           "Total Males" : 13049,
#           "Average Household Size" : 3.85
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "NqNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 32821,
#           "Total Households" : 9155,
#           "Total Females" : 17101,
#           "Zip Code" : 90062,
#           "Median Age" : 31.8,
#           "Total Males" : 15720,
#           "Average Household Size" : 3.55
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "N6Nl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 55758,
#           "Total Households" : 13260,
#           "Total Females" : 27915,
#           "Zip Code" : 90063,
#           "Median Age" : 29.0,
#           "Total Males" : 27843,
#           "Average Household Size" : 4.19
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "OKNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 25403,
#           "Total Households" : 10968,
#           "Total Females" : 13106,
#           "Zip Code" : 90064,
#           "Median Age" : 40.0,
#           "Total Males" : 12297,
#           "Average Household Size" : 2.29
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "OaNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 45527,
#           "Total Households" : 14476,
#           "Total Females" : 22654,
#           "Zip Code" : 90065,
#           "Median Age" : 36.1,
#           "Total Males" : 22873,
#           "Average Household Size" : 3.12
#         }
#       },
#       {
#         "_index" : "population",
#         "_type" : "_doc",
#         "_id" : "OqNl3n8B3FV1DW-nLDu_",
#         "_score" : 1.0,
#         "_source" : {
#           "Total Population" : 55277,
#           "Total Households" : 23985,
#           "Total Females" : 27563,
#           "Zip Code" : 90066,
#           "Median Age" : 37.3,
#           "Total Males" : 27714,
#           "Average Household Size" : 2.29
#         }
#       }
#     ]
#   }
# }
```

3. Import through Kibana the file `weekly_MSFT.csv`. Pre visualize the document (`dataset/weekly_MSFT.csv`) with the index `stock`

```bash
# done through Kibana.
```

4. Executar as consultas no índice `stock`

a) Visualizar os documentos do dia `"2019-01-01"` à `"2019-03-01"`. (hits = 9).

```bash
GET stock/_search
{
	"query": {
		"range": {
			"timestamp": {
				"format": "yyyy-MM-dd",
				"gte": "2019-01-01",
				"lte": "2019-03-01"
			}
		}
	}
}
# output:
# {
#   "took" : 3,
#   "timed_out" : false,
#   "_shards" : {
#     "total" : 1,
#     "successful" : 1,
#     "skipped" : 0,
#     "failed" : 0
#   },
#   "hits" : {
#     "total" : {
#       "value" : 9,
#       "relation" : "eq"
#     },
#     "max_score" : 1.0,
#     "hits" : [
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "0QXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 119359497,
#           "high" : 113.24,
#           "@timestamp" : "2019-03-01T00:00:00.000-03:00",
#           "low" : 110.88,
#           "close" : 112.53,
#           "open" : 111.76,
#           "timestamp" : "2019-03-01"
#         }
#       },
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "0gXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 96472580,
#           "high" : 111.2,
#           "@timestamp" : "2019-02-22T00:00:00.000-03:00",
#           "low" : 106.29,
#           "close" : 110.97,
#           "open" : 107.79,
#           "timestamp" : "2019-02-22"
#         }
#       },
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "0wXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 110757176,
#           "high" : 108.3,
#           "@timestamp" : "2019-02-15T00:00:00.000-02:00",
#           "low" : 104.965,
#           "close" : 108.22,
#           "open" : 106.2,
#           "timestamp" : "2019-02-15"
#         }
#       },
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "1AXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 130472196,
#           "high" : 107.27,
#           "@timestamp" : "2019-02-08T00:00:00.000-02:00",
#           "low" : 102.77,
#           "close" : 105.67,
#           "open" : 102.87,
#           "timestamp" : "2019-02-08"
#         }
#       },
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "1QXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 201611213,
#           "high" : 106.48,
#           "@timestamp" : "2019-02-01T00:00:00.000-02:00",
#           "low" : 102.17,
#           "close" : 102.78,
#           "open" : 106.26,
#           "timestamp" : "2019-02-01"
#         }
#       },
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "1gXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 112628578,
#           "high" : 107.88,
#           "@timestamp" : "2019-01-25T00:00:00.000-02:00",
#           "low" : 104.86,
#           "close" : 107.17,
#           "open" : 106.75,
#           "timestamp" : "2019-01-25"
#         }
#       },
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "1wXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 155699162,
#           "high" : 107.9,
#           "@timestamp" : "2019-01-18T00:00:00.000-02:00",
#           "low" : 101.26,
#           "close" : 107.71,
#           "open" : 101.9,
#           "timestamp" : "2019-01-18"
#         }
#       },
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "2AXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 157833149,
#           "high" : 104.88,
#           "@timestamp" : "2019-01-11T00:00:00.000-02:00",
#           "low" : 100.98,
#           "close" : 102.8,
#           "open" : 101.64,
#           "timestamp" : "2019-01-11"
#         }
#       },
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "2QXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 155142140,
#           "high" : 102.51,
#           "@timestamp" : "2019-01-04T00:00:00.000-02:00",
#           "low" : 97.2,
#           "close" : 101.93,
#           "open" : 101.29,
#           "timestamp" : "2019-01-04"
#         }
#       }
#     ]
#   }
# }
```

b) Visualizar os documentos do dia `"2019-04-01"` até agora. (hits = 3).

```bash
GET stock/_search
{
	"query": {
		"range": {
			"timestamp": {
				"format": "yyyy-MM-dd",
				"gte": "2019-04-01",
				"lte": "now"
			}
		}
	}
}
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
#       "value" : 3,
#       "relation" : "eq"
#     },
#     "max_score" : 1.0,
#     "hits" : [
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "ygXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 48874731,
#           "high" : 121.85,
#           "@timestamp" : "2019-04-17T00:00:00.000-03:00",
#           "low" : 120.1,
#           "close" : 121.77,
#           "open" : 120.94,
#           "timestamp" : "2019-04-17"
#         }
#       },
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "ywXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 83159600,
#           "high" : 120.98,
#           "@timestamp" : "2019-04-12T00:00:00.000-03:00",
#           "low" : 118.58,
#           "close" : 120.95,
#           "open" : 119.81,
#           "timestamp" : "2019-04-12"
#         }
#       },
#       {
#         "_index" : "stock",
#         "_type" : "_doc",
#         "_id" : "zAXLAoABpb1bobqyMjEY",
#         "_score" : 1.0,
#         "_source" : {
#           "volume" : 99731237,
#           "high" : 120.43,
#           "@timestamp" : "2019-04-05T00:00:00.000-03:00",
#           "low" : 118.1,
#           "close" : 119.89,
#           "open" : 118.95,
#           "timestamp" : "2019-04-05"
#         }
#       }
#     ]
#   }
# }
```
