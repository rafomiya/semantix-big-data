# More Query Options

## Query options

​	`GET index/_search` retrieves all the documents inside the index. Using the same format, we can increase specificity and do more interesting queries:

- `GET index/_search?q=parameter`: searches for the given parameter in all the attributes.
- `GET index/_search?q=name:parameter`: searches for the given parameter on a specific attribute.
   - Example with two attributes:

```
GET client/_search?q=name:John&age:20
```

- Query DSL (Domain Specific Language): based on JSON.

```
GET client/_search?q=Hadoop
{
	"query": {
		"match_all": {}
	}
}	
```

## Query output  

```bash
{
  "took" : 3,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 319,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    <...>
  }
}
```

- `took`: time took in milliseconds.
- `timed_out`: if the query has timed out or not.
- `_shards`: amount of shards used, and if they had any errors.
- `hits`: informations about the results:
  - `total`: amount of documents retrieved.
  - `max_score`: result's similarity score (from 0 to 1).

## Query on multiple indexes

```bash
# searches through all the indexes. This is not used with much frequency, since it takes too much time.
GET _all/_search?q=<query_parameter>

# retrieves data from all the indexes listed. Throws `index_not_found_exception` if the index doesn't exists.
GET index1,index2/_count?q=<query_parameter>
```
