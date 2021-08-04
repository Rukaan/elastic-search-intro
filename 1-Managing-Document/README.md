## Managing Document

List all index
```
GET /_cat/indices?v
```
&nbsp;

Create index
```
PUT /products
```
&nbsp;

Get index information
```
GET /products
```
&nbsp;

Upsert document (all)
```
PUT /products/_doc/1
{
  "name": "Handphone",
  "description":"you can call someone with this"
}
```
&nbsp;

Get document detail
```
GET /products/_doc/1
```
&nbsp;

Upsert document (partial)
```
POST /products/_doc/2
{ 
  "name": "Computer",
  "description": "computer can type document and calculate"
}
```
&nbsp;

Upsert document with `Optimistic Concurrency Control`
```
PUT /products/_doc/2?if_primary_term=1&if_seq_no=28
{ 
  "name": "Computer",
  "description": "computer can type document, calculate, and access internet"
}
```
&nbsp;

Insert document without generated id
```
POST /products/_doc
{ 
  "name": "laptop",
  "description": "computer but small"
}
```
&nbsp;

Get all data in index
```
GET /products/_search
{
    "query": {
      "match_all": { }
    }
}
```
&nbsp;

Get query data with format, source, size, and offset
```
GET /products/_search?format=yaml
{
    "_source": ["name","description"],
    "size": 2,
    "from": 0, 
    "query": {
      "match": { "description": "computer" }
    }
}
```
&nbsp;

Get mapping information
```
GET /products/_mapping
```
&nbsp;

Update document by query script
```
POST /products/_update_by_query
{
  "conflicts" : "proceed",
  "script": {
    "source" : "ctx._source.name = ctx._source.name + ' Xiaomi' "
  }
}
```
&nbsp;

Delete document
```
DELETE /products/_doc/1
```
&nbsp;

Delete document by query
```
POST /products/_delete_by_query
{
    "query": {
      "match": { "description": "computer" }
    }
}
```
&nbsp;

Delete index
```
DELETE /products
```