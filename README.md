# elastic-search-intro

Repostiory to introduce elastic search syntax to beginner level

## Running Elastic and Kibana on Localhost Linux

1. Download Elastic Search From [Here](https://www.elastic.co/downloads/elasticsearch)

2. Download Kibana From [Here](https://www.elastic.co/downloads/kibana)

3. Unzip both file

4. Check your java using `which java`

5. Set `ES_JAVA_HOME` to your java, but without `/bin/java`, e.g:
if java in `/usr/bin/java`, use `export ES_JAVA_HOME=/usr` 

6. (Optional if error) Go to elastic search directory,
Go to folder `config` and open `elasticsearch.yml`
Add `xpack.ml.enabled: false`

7. Go to elastic search directory and type `bin/elasticsearch`
It will run on `localhost:9200`

8. Go to kibana directory and type `bin/kibana`
It will run on `localhost:5601`