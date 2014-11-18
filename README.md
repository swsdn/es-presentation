es-presentation
===============

Presentation of basic elasticsearch features (in PL)

```
curl -XPUT http://10.0.0.11:9200/shakespeare -d '
{
 "mappings" : {
  "_default_" : {
   "properties" : {
    "speaker" : {"type": "string", "index" : "not_analyzed" },
    "play_name" : {"type": "string", "index" : "not_analyzed" },
    "line_id" : { "type" : "integer" },
    "speech_number" : { "type" : "integer" }
   }
  }
 }
}
';
```

`wget http://www.elasticsearch.org/guide/en/kibana/current/snippets/shakespeare.json`

`curl -XPUT 10.0.0.11:9200/_bulk --data-binary @shakespeare.json`
