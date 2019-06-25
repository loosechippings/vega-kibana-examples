# Example Vega Kibana visualisations

## Pre-requisites

You'll need at least version 7 of Kibana with the e-commerce sample data set installed. 

Either use the [online demo](https://demo.elastic.co/) or run as docker containers locally:

Start Elasticsearch:

`docker run -d --rm --name elasticsearch --net elastic -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.0.1`

Start Kibana:

`docker run -d --rm --name kibana --net elastic -p 5601:5601 kibana:7.0.1`

Create a new Vega visualisation in Kibana and copy-paste in the example code.
