# elastic-search-intro

Repostiory to introduce elastic search syntax to beginner level

## Running Elastic Search on Localhost Linux

1. Download Elastic Search From [Here](https://www.elastic.co/downloads/elasticsearch)

2. Unzip file

3. Check your java directory using `which java`

4. Set `ES_JAVA_HOME` to your java directory, if java in `/usr/bin/java`, use `export ES_JAVA_HOME=/usr` 

5. (Optional) In elastic search directory, open `config/elasticsearch.yml`, then add `xpack.ml.enabled: false`

6. To run, type `bin/elasticsearch`

7. It will run on `localhost:9200`


## Running Kibana on Localhost Linux

1. Download Kibana From [Here](https://www.elastic.co/downloads/kibana)

2. Unzip file

3. To run, type `bin/kibana`

4. It will run on `localhost:5601`
