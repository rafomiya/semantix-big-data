# Bulk API

​	Consists on making many index/delete operations in one single API call. Doing so, it increases the index speed.

​	Syntax:

```bash
POST _bulk
{
	"index": {
		"_index": "test",
		"_id": 1
	}
}
{ "field1": "value1" }
{
	"delete": {
		"_index": "test",
		"_id": "2"
	}
}
{
	"create": {
		"_index": "test",
		"_id": 3
	}
}
{ "field1": "value3" }
{
	"update": {
		"_id": 1,
		"_index": "test"
	}
}
{
	"doc": {
		"field2": "value2"
	}
}
```

​	Example: insert the following 5 documents in one single call.

```bash
POST dealership/_bulk
{ "create": { "_id": 1 } }
{ "name": "car" }
{ "create": { "_id": 2 } }
{ "name": "automobile" }
{ "create": { "_id": 3 } }
{ "name": "truck" }
{ "create": { "_id": 4 } }
{ "name": "pickup truck" }
{ "create": { "_id": 5 } }
{ "name": "vehicle" }
```

