# Index documents
`PUT` the doc into the index (name) and if the index doesn't exist, then it will be created
```
PUT /<index_name>/_doc/1
{
    "<field>": "<value>"
}
```

# Search an index
`GET` all docs from the index (name)
```
GET /<index_name>/_search
{
  "query": { "match_all": {} },
  "sort": [
    { "<sorted_field>": "<asc|desc>" }
  ]
}
```
## Paging
`GET` 10 through 19
```
GET /<index>/_search
{
  "query": { "match_all": {} },
  "sort": [
    { "<field>": "<direction>" }
  ],
  "from": 10,
  "size": 10
}
```

## Match searching
`GET` docs matching a value as keywords in a specific field
```
GET /<index>/_search
{
  "query": { "match": { "<field>": "<word1> <word2>" } }
}
```
``GET` docs matching a value as a phrase in a specific field
```
GET /<index>/_search
{
  "query": { "match_phrase": { "<field>": "<phrase>" } }
}
```
`GET` docs that are required (must match), desirable (should match), or undesirable (must not match)
```
GET /<index>/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "<text filed>": "<value>" } }
      ],
       "should": [
        { "term": { "<filed>": "<value>" } }
      ], 
      "must_not": [
        { "match": { "<text filed>": "<value>" } }
      ]
    }
  }
}
```
`GET` docs through a filter with a range
```
GET /<index>/_search
{
  "query": {
    "bool": {
      "must": { "match_all": {} },
      "filter": {
        "range": {
          "<filed>": {
            "gte": <lower limit (close)>,
            "lte": <upper limit (close)>
          }
        }
      }
    }
  }
}
```