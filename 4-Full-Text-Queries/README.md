## Full Text Queries

Go to this forlder directory and import data using
```
curl -H "Content-Type: application/json" \
-XPOST "http://localhost:9200/recipes/_bulk?pretty" \
--data-binary "@recipes.json"
```
&nbsp;

Query match by title (text)
```
GET /recipes/_search
{
  "query": {
    "match": {
      "title": "Recipes with pasta or spaghetti"
    }
  }
}
```
&nbsp;

Query match by title with operator
```
GET /recipes/_search
{
  "query": {
    "match": {
      "title": {
        "query": "Recipes with pasta or spaghetti",
        "operator": "and"
      }
    }
  }
}

```
&nbsp;

Query match phrases by title (order matters)
```
GET /recipes/_search
{
  "query": {
    "match_phrase": {
      "title": "spaghetti puttanesca"
    }
  }
}
```
&nbsp;

Query multi match fields
```
GET /recipes/_search
{
  "query": {
    "multi_match": {
      "query": "pasta",
      "fields": [ "title", "description" ]
    }
  }
}
```
&nbsp;

---

Query ingredient name and preparation range with must
```
GET /recipes/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "ingredients.name": "parmesan"
          }
        },
        {
          "range": {
            "preparation_time_minutes": {
              "lte": 15
            }
          }
        }
      ]
    }
  }
}
```
&nbsp;

Query ingredient name and preparation range with must and filter (with debugging)
```
GET /recipes/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "ingredients.name": {
              "query": "parmesan",
              "_name": "parmesan_must"
            }
          }
        }
      ],
      "filter": [
        {
          "range": {
            "preparation_time_minutes": {
              "lte": 15,
              "_name": "prep_time_filter"
            }
          }
        }
      ]
    }
  }
}
```
&nbsp;

