#Managing Document

List all index
```
GET /_cat/indices?v
```

Create index
```
PUT /products
```

Get index information
```
GET /products
```

Get mapping information
```
GET /products/_mapping
```

Upsert document (all)
```
PUT /products/_doc/1
{
  "name": "Handphone",
  "description":"you can call someone with this"
}
```

Get document detail
```
GET /products/_doc/1
```

Upsert document (partial)
```
POST /products/_doc/2
{ 
  "name": "Computer",
  "description": "computer can type document and calculate"
}
```

Upsert document with Optimistic Concurrency controlling
```
PUT /products/_doc/2?if_primary_term=1&if_seq_no=28
{ 
  "name": "Computer",
  "description": "computer can type document, calculate, and access internet"
}
```

Insert document without id
```
POST /products/_doc
{ 
  "name": "laptop",
  "description": "computer but small"
}
```

Get all data in index
```
GET /products/_search
{
    "query": {
      "match_all": { }
    }
}
```

Get query data with format and source
```
GET /products/_search?format=yaml
{
    "_source": ["name","description"],
    "query": {
      "match": { "description": "computer" }
    }
}
```

Update document by query
```
POST /products/_update_by_query
{
  "conflicts" : "proceed",
  "script": {
    "source" : "ctx._source.name = ctx._source.name + ' Xiaomi' "
  }
}
```

Delete document
```
DELETE /products/_doc/1
```

Delete document by query
```
POST /products/_delete_by_query
{
    "query": {
      "match": { "description": "computer" }
    }
}
```

Delete index
```
DELETE /products
```