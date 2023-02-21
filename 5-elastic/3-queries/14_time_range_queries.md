# Time Range

​	When dealing with time values in Elastic, we can make some customizations, such as the date format and the time zone.

```bash
"format": "dd/MM/yyyy||yyyy",
"time_zone": "+03:00"
```

​	Examples:

```bash
# get all the dates after 01/01/2012 and before 2013:
GET client/_search
{
  "query": {
    "range": {
      "birthday": {
        "gt": "01/01/2012",
        "lt": "2013",
        "format": "dd/MM/yyyy||yyyy"
      }
    }
  }
}
# the `format` field specified two date formats, separated with "||".
```

```bash
# get all the dates between now and yesterday:
GET client/_search
{
  "query": {
    "range": {
      "birthday": {
        "gte": "now-1d",
        "lt": "now"
      }
    }
  }
}
# 
```
