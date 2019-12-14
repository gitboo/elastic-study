# Elastic Study


## 엘라스틱 서치 실무 가이드 예제

## Requirements

```console
  brew install jq
```

### Host setup

* [Docker Engine](https://docs.docker.com/install/) version **17.05+**
* [Docker Compose](https://docs.docker.com/compose/install/) version **1.12.0+**
* 1.5 GB of RAM

By default, the stack exposes the following ports:

* 9200: Elasticsearch HTTP
* 9300: Elasticsearch TCP transport
* 5601: Kibana


```console
$ docker-compose up
```


```console
$ docker-compose down -v
```


* user: *beauty*
* password: *beauty*


4. Restart Kibana and Logstash to apply changes

```console
$ docker-compose restart kibana logstash
```

#### On the command line

Create an index pattern via the Kibana API:

```console
$ curl -XPOST -D- 'http://localhost:5601/api/saved_objects/index-pattern' \
    -H 'Content-Type: application/json' \
    -H 'kbn-version: 7.4.1' \
    -u elastic:<your generated elastic password> \
    -d '{"attributes":{"title":"logstash-*","timeFieldName":"@timestamp"}}'
```


## Extensibility

### How to add plugins

To add plugins to any ELK component you have to:

1. Add a `RUN` statement to the corresponding `Dockerfile` (eg. `RUN logstash-plugin install logstash-filter-json`)
2. Add the associated plugin code configuration to the service configuration (eg. Logstash input/output)
3. Rebuild the images using the `docker-compose build` command

### How to enable the provided extensions
