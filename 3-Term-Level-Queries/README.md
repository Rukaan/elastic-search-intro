## Term Level Queries

**Effective for data type date, number, and keyword**
&nbsp;

Go to this forlder directory and import data using
```
curl -H "Content-Type: application/json" \
-XPOST "http://localhost:9200/products/_bulk?pretty" \
--data-binary "@products.json"
```
&nbsp;

Query match by name (text)
```
GET /products/_search
{
  "query": {
    "match": {
      "name": "Wine"
    }
  }
}
```
&nbsp;

Query term by name (text)
```
GET /products/_search
{
  "query": {
    "term": {
      "name": "Wine"
    }
  }
}

```
&nbsp;

Query term by status (boolean)
```
GET /products/_search
{
  "query": {
    "term": {
      "is_active": true
    }
  }
}
```
&nbsp;

Query terms by tags (array keyword)
```
GET /products/_search
{
  "query": {
    "terms": {
      "tags.keyword": ["Soup", "Vegetable"]
    }
  }
}
```
&nbsp;

Query by ids
```
GET /products/_search
{
  "query": {
    "ids": {
      "values": [1,69,420]
    }
  }
}
```
&nbsp;

Query by tag prefix
```
GET /products/_search
{
  "query": {
    "prefix": {
      "tags.keyword": "Vege"
    }
  }
}
```
&nbsp;

Query by tag wildcard
```
GET /products/_search
{
  "query": {
    "wildcard": {
      "tags.keyword": "Vege*bl?"
    }
  }
}
```
&nbsp;

Query by stock range
```
GET /products/_search
{
  "query": {
    "range": {
      "in_stock": {
        "gte": 5,
        "lte" : 10
      }
    }
  }
}
```