# elasticsearch-learning
## Query:
### Basic query types:
#### Terms:
The term query finds documents that contain the exact term specified in the inverted index. Used for direct text matching. There's no any analyzing on a data(for example: upper-case and lower-case searched term will give you different results).
```json
GET my_blog/post/_search
{
    "query": {
        "term": {
           "post_text": "green"
        }
    }
}
```
#### Match.
A family of match queries that accepts text/numerics/dates, analyzes them, and constructs a query.There are three types of `match` query: `boolean`, `phrase`, and `phrase_prefix`:
```json
GET my_blog/post/_search
{
    "query": {
        "match": {
           "post_text": "green"
        }
    }
}

GET my_blog/post/_search
{
    "query": {
        "match" : {
            "post_text" : {
                "query" : "green sky",
                "operator" : "and"
            }
        }
    }
}

```
`multi_match` allows multi-field queries. Fields can be specified with wildcards:
```json
GET my_blog/post/_search
{
    "query": {
        "multi_match": {
            "fields": [
               "user_*",
               "post_word_count"
            ],
            "query": 2, 
            "operator":"and"
        }
    }
}
```
The `match_phrase` query analyzes the text and creates a phrase query out of the analyzed text. For example:
```json
GET my_blog/post/_search
{
    "query": {
        "match_phrase": {
           "post_text":"green sky"
        }
    }
}
```
And we can use `match_phrase_prefix`.
#### Range. Matches documents with fields that have terms within a certain range. The range query accepts the following parameters:
* `gte` - Greater-than or equal to
* `gt` - Greater-than
* `lte` - Less-than or equal to
* `lt` - Less-than
* `boost` - Sets the boost value of the query, defaults to 1.0
Formatted dates will be parsed using the `format` specified on the date field by default, but it can be overridden by passing the format parameter to the range query:`"format": "dd/MM/yyyy||yyyy"`.
When running range queries on fields of type date, ranges can be specified using the section called "Date Math":
```json
{
    "range" : {
        "date" : {
            "gte" : "now-1d/d",
            "lt" :  "now/d"
        }
    }
}
```

#### Filter

### Specialized query types
### Combining quueries

