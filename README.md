# miroir-app

Surcouche d’API Elasticsearch 6.8, pour la recherche.


## Installation ES

Installer [ES 6.8.14](https://www.elastic.co/fr/downloads/past-releases/elasticsearch-6-8-14).

Howto : [https://www.elastic.co/guide/en/elasticsearch/reference/6.8/zip-targz.html](https://www.elastic.co/guide/en/elasticsearch/reference/6.8/zip-targz.html)

**Install**

```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.8.14.zip
unzip elasticsearch-6.8.14.zip
cd elasticsearch-6.8.14
```

**Run**

```
./bin/elasticsearch
```

**Configure**

[ICU Analysis Plugin](https://www.elastic.co/guide/en/elasticsearch/plugins/current/analysis-icu.html), Unicode support

```
sudo bin/elasticsearch-plugin install analysis-icu
```

**Launch**

```
service elasticsearch start
```

## Indexer le corpus

**Install venv**

```
cd miroir-app
python3.8 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

**Update dev.env**
```
ELASTICSEARCH_URL = http://localhost:9200
ELASTICSEARCH_CONFIG_DIR = 'elasticsearch'
DOCUMENT_INDEX = 'miroir_document'
COLLECTION_INDEX = 'miroir_collection'
DTS_URL = http://localhost:5050/dts
```

**Update the conf**

```
python manage.py update-conf --rebuild
```

**Index the data** 
```
python manage.py index --root_collection miroir
```

## Lancer l’application

```
python flask_app.py
```

## Tester 

```
http://localhost:5003/api/1.0/search?query=content:César
```

And use the following for offline commands:

```bash

> python manage.py --help

Usage: manage.py [OPTIONS] COMMAND [ARGS]...

Options:
  --help  Show this message and exit.

Commands:
  delete       Delete the indexes
  index        Rebuild the elasticsearch indexes
  search       Perform a search using the provided query.
  update-conf  Update the index configuration and mappings
```
