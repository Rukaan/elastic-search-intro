## Index Mapping

Add index with static mapping and dynamic parameter
```
PUT /books
{
  "mappings": {
    "dynamic": "true",
    "properties": {
      "name": { 
        "type" : "text"
      },
      "status": {
        "type" : "keyword"
      },
      "author": {
        "type" : "nested",
        "properties": {
          "name": {
            "type":"text"
          }
        }
      },
      "review": {
        "type" : "object"
      }
    }
  }
}
```

Get index mapping
```
GET /books/_mapping
```

Add document 1
```
PUT /books/_doc/1
{
  "name": "How to impress cook simple dinner",
  "status":"PUBLISHED",
  "author": { "name" : "john doe" },
  "review": { "comment": "Good book" }
}
```

Add document 2
```
PUT /books/_doc/2
{
  "name": "How to train your dragon",
  "status":"REVIEW",
  "author": { "name" : "jane doe" },
  "review": { "comment": "i can tame a dragon now" },
  "description":"books about adventure"
}
```

Get all data in index
```
GET /books/_search
{
    "query": {
      "match_all": {}
    }
}
```

Query by name
```
GET /books/_search
{
    "query": {
      "match": { "name": "how" }
    }
}
```

Query by description
```
GET /books/_search
{
    "query": {
      "match": { "description": "books" }
    }
}
```

Query by status
```
GET /books/_search
{
    "query": {
      "match": { "status": "PUBLISHED" }
    }
}
```

Query nested by author name
```
GET /books/_search
{
  "query": {
    "nested": {
      "path": "author",
      "query": {
        "bool": {
          "must": [
            { "match": { "author.name": "doe" } }
          ],
          "should": [
            { "match": { "author.name": "jane" } }
          ],
          "must_not": [
            { "match": { "author.name": "john" } }
          ]
        }
      }
    }
  }
}
```

Error query if not object not nested
```
GET /books/_search
{
  "query": {
    "nested": {
      "path": "review",
      "query": {
        "bool": {
          "must": [
            { "match": { "review.comment": "dragon" } }
          ]
        }
      }
    }
  }
}
```

Add mapping to existing index
```
PUT /books/_mapping
{
  "properties": {
    "created_at": { "type" : "date" }
  }
}
```

**Delete mapping is not possible**

Delete index
```
DELETE /books
```