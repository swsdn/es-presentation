es-presentation
===============

Presentation of basic elasticsearch features (in PL)

# Routing, ściąga:

## Domyślny index:
```sh
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
## Pobranie wszystkich dzieł Shakespeare'a:
```sh
wget http://www.elasticsearch.org/guide/en/kibana/current/snippets/shakespeare.json
```
## Wrzucenie do indexu:
```sh
curl -XPUT 10.0.0.11:9200/_bulk --data-binary @shakespeare.json```
## Usunięcie indexu:
```sh
curl -XDELETE 'http://10.0.0.11:9200/shakespeare/'```
## Mapping z routingiem:
```sh
curl -XPUT http://10.0.0.11:9200/shakespeare -d '
{  
   "settings":{  
      "number_of_shards":50,
      "number_of_replicas":2
   },
   "mappings":{  
      "_default_":{  
         "_routing":{  
            "required":"true",
            "path":"play_name"
         },
         "properties":{  
            "speaker":{  
               "type":"string",
               "index":"not_analyzed"
            },
            "play_name":{  
               "type":"string",
               "index":"not_analyzed"
            },
            "line_id":{  
               "type":"integer"
            },
            "speech_number":{  
               "type":"integer"
            }
         }
      }
   }
}';
```