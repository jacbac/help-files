Elastic Stack
=============

Former Elasticsearch.

Rapid Installation
------------------

* [Download](https://www.elastic.co/downloads/elasticsearch) and unzip the Elasticsearch official distribution.
* Run `./bin/elasticsearch` on unix, or `bin\elasticsearch.bat` on windows.
* Run `curl -X GET http://localhost:9200/`.
* Start more servers …

Launch & Stop
-------------

* Start ES with `./bin/elasticsearch [-d]` (the -d option is for a ES daemon)
* Test ES with [http://localhost:9200/](http://localhost:9200/) or `curl -X GET http://localhost:9200/`. You normaly get a json response like:

```json
{
  "status" : 200,
  "name" : "USAgent",
  "cluster_name" : "elasticsearch",
  "version" : {
    "number" : "1.5.1",
    "build_hash" : "5e38401bc4e4388537a615569ac60925788e1cf4",
    "build_timestamp" : "2015-04-09T13:41:35Z",
    "build_snapshot" : false,
    "lucene_version" : "4.10.4"
  },
  "tagline" : "You Know, for Search"
}
```

* Stop ES with ``

Search Problems
---------------

* [Escaping problems and official solution in Elastic](http://www.elastic.co/guide/en/elasticsearch/guide/master/char-filters.html)

Plugins
-------

### Help

* [Elastic official plugins guide](http://www.elastic.co/guide/en/elasticsearch/reference/current/modules-plugins.html)
* [Elastic plugins study](https://blog.codecentric.de/en/2014/03/elasticsearch-monitoring-and-management-plugins/)

### Install

```shell
cd your_path/to/elasticsearch
```

* [ElasticHQ](http://www.elastichq.org/): Elasticsearch management and monitoring plugin. Install with: `bin/plugin -i royrusso/elasticsearch-HQ`. Open with: [http://localhost:9200/_plugin/HQ/](http://localhost:9200/_plugin/HQ/)
* [Elasticsearch Inquisitor](https://github.com/polyfractal/elasticsearch-inquisitor): Test and debug ES queries. Install with: `bin/plugin -i polyfractal/elasticsearch-inquisitor`. Open with: [http://localhost:9200/_plugin/inquisitor/](http://localhost:9200/_plugin/inquisitor/)
* [Elastic's Marvel](https://www.elastic.co/products/marvel): Monitor your Elasticsearch deployment and queries with Sense module. Install with: `bin/plugin -i elasticsearch/marvel/latest`. Open with: [http://localhost:9200/_plugin/marvel/](http://localhost:9200/_plugin/marvel/)
* [Elasticsearch Kopf](https://github.com/lmenezes/elasticsearch-kopf): Elasticsearch management and monitoring plugin. Install with: `bin/plugin -i lmenezes/elasticsearch-kopf/master`. Open with: [http://localhost:9200/_plugin/kopf/](http://localhost:9200/_plugin/kopf/)
* [Elasticsearch Head](http://mobz.github.io/elasticsearch-head/): Elasticsearch management and monitoring plugin. Install with: `bin/plugin -i mobz/elasticsearch-head`. Open with: [http://localhost:9200/_plugin/head/](http://localhost:9200/_plugin/head/)
* [Elasticsearch Monitoring](https://github.com/abronner/elasticsearch-monitoring)

ELK Stack
---------

### Help

* [ELK with Wooster (FR, 2014)](https://wooster.checkmy.ws/2014/04/elk-elasticsearch-logstash-kibana/)
* [ELK with Xebia (FR, 2013)](http://blog.xebia.fr/2013/12/12/logstash-elasticsearch-kibana-s01e02-analyse-orientee-business-de-vos-logs-applicatifs/)
* [ELK with Digital Ocean (EN, 2015)](https://www.digitalocean.com/community/tutorials/how-to-use-logstash-and-kibana-to-centralize-and-visualize-logs-on-ubuntu-14-04)
