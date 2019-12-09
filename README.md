# OPAL Named Entity Disambiguation and indexing component 

**AGDISTIS** (Agnostic Named Entity Disambiguation) aims at delivering a framework for disambiguating a priori annotated named entities.
It has been extended in the project **LIMBO** to integrate the search engine Elasticsearch.
In the project **OPAL**, the geographical database LauNuts was integrated.

Links to other versions:

- [AGDISTIS](https://github.com/dice-group/AGDISTIS)
- [AGDISTIS Elasticsearch](https://github.com/dice-group/AGDISTIS/tree/elasticsearch_development)  
 
## Installation

The underlying indexing system is Elasticsearch 6.6.
The installation with Docker is described at the [Elasticsearch documentation](https://www.elastic.co/guide/en/elasticsearch/reference/6.6/docker.html).
The following commands can be used:

 - `docker pull docker.elastic.co/elasticsearch/elasticsearch:6.6.0`
 - `docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:6.6.0`

To import the required data, perform the following steps: 
- Download and extract the [LauNuts dataset](https://hobbitdata.informatik.uni-leipzig.de/OPAL/LauNuts/)
- Set the property *folderWithTTLFiles* in the configuration file *agdistis.properties*
- Run the *org.aksw.agdistis.indexWriter.TripleIndexCreator*
- Validate the data status on [http://localhost:9200/_cat/indices?v](http://localhost:9200/_cat/indices?v) using the [Elasticsearch cat indices API](https://www.elastic.co/guide/en/elasticsearch/reference/6.6/cat-indices.html)

Start the webservices using org.aksw.agdistis.webapp.RunApp.


## Usage

- Use the [AGDISTIS webservice URLs](https://github.com/dice-group/AGDISTIS/wiki/2-Asking-the-webservice) to disambiguate places
- Disambiguation example: `curl --data-urlencode "text='The city of <entity>Paderborn</entity> has over 150,000 inhabitants.'" -d type='agdistis' http://localhost:8080/AGDISTIS`
- Candidates example: `curl --data-urlencode "text='The city of <entity>Hamburg</entity> is also a federal state.'" -d type='candidates' http://localhost:8080/AGDISTIS`


## Credits

[Data Science Group (DICE)](https://dice-research.org/) at [Paderborn University](https://www.uni-paderborn.de/)

This work has been supported by the German Federal Ministry of Transport and Digital Infrastructure (BMVI) in the projects
[Open Data Portal Germany (OPAL)](http://projekt-opal.de/) (funding code 19F2028A)
and
[Linked Data Services for Mobility (LIMBO)](https://www.limbo-project.org/) (funding code 19F2029I).