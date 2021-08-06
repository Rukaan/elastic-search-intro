## Improve Search

Go to this forlder directory and import data using
```
curl -H "Content-Type: application/json" \
-XPOST "http://localhost:9200/proximity/_bulk?pretty" \
--data-binary "@proximity.json"
```
&nbsp;

Query match phrase title with slop
```
GET /proximity/_search
{
  "query": {
    "match_phrase": {
      "title": {
        "query": "spicy sauce",
        "slop": 1
      }
    }
  }
}
```
&nbsp;

Query match title must
```
GET /proximity/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "title": {
              "query": "spicy sauce"
            }
          }
        }
      ]
    }
  }
}
```
&nbsp;

Query match title must and should
```
GET /proximity/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "title": {
              "query": "spicy sauce"
            }
          }
        }
      ],
      "should": [
        {
          "match_phrase": {
            "title": {
              "query": "spicy sauce",
              "slop": 5
            }
          }
        }
      ]
    }
  }
}
```
&nbsp;

---
&nbsp;

Query fuzzy by name
```
GET /products/_search
{
  "query": {
    "match": {
      "name": {
        "query": "l0bster",
        "fuzziness": "auto"
      }
    }
  }
}
```
&nbsp;

Query fuzzy multiple word
```
GET /products/_search
{
  "query": {
    "match": {
      "name": {
        "query": "l0bster lvie",
        "operator": "and",
        "fuzziness": 1
      }
    }
  }
}
```
&nbsp;

Stemming (?)