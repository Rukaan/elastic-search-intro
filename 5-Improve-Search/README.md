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

---
&nbsp;

Add data example
```
POST /highlighting/1
{
  "description": "Let me tell you a story about Elasticsearch. It's a full-text search engine that is built on Apache Lucene. It's really easy to use, but also packs lots of advanced features that you can use to tweak its searching capabilities. Lots of well-known and established companies use Elasticsearch, and so should you!"
}
```
&nbsp;

Query highlight with tags
```
GET /highlighting/_search
{
  "_source": false,
  "query": {
    "match": { "description": "Elasticsearch story" }
  },
  "highlight": {
    "pre_tags": [ "<strong>" ],
    "post_tags": [ "</strong>" ],
    "fields": {
      "description" : {}
    }
  }
}
```