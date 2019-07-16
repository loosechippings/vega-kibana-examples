# Using Elasticsearch date_range data type

Described [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/range.html).

Documents can have a date range. Date range queries may then return documents that intersect a range (or a point in time if the query gte and lte are the same). We can use this to record time ranges that a version of a document was valid between and so query for a view of the world at a point in time. 


```
DELETE foo

PUT foo
{
  "settings": {
    "number_of_shards": 2
  },
  "mappings": {
    "properties": {
      "time_frame": {
        "type": "date_range",
        "format": "yyyy-MM-dd HH:mm:ss||yyyy-MM-dd||epoch_millis"
      },
      "timestamp": {
        "type": "date",
        "format": "yyyy-MM-dd HH:mm:ss||yyyy-MM-dd||epoch_millis"
      }
    }
  }
}

PUT foo/_doc/1
{
  "color": "green",
  "time_frame": {
    "gte": "2019-07-10 00:00:00"
  },
  "timestamp": "2019-07-09 00:00:00"
}

POST foo/_doc/2
{
  "color": "blue",
  "time_frame": {
    "gte": "2019-07-01 00:00:00",
    "lte": "2019-07-20 00:00:00"
  },
  "timestamp": "2019-07-10 00:00:00"
}

POST foo/_doc/3
{
  "color": "red",
  "time_frame": {
    "gte": "2019-07-10 00:00:00",
    "lte": "2019-07-11 00:00:00"
  },
  "timestamp": "2019-07-11 00:00:00"
}

GET foo/_search
{
  "query": {
    "range": {
      "time_frame": {
        "gte": "2019-07-21 00:00:00",
        "lte": "2019-07-21 00:00:00"
      }
    }
  }
}
```
