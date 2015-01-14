#Going through the best parts from Elasticsearch: The Definitive Guide#

The idea for this section is to quickly go over many of the basic concepts in Elasticsearch.

Try creating the samples in Sense or Fiddler first to se how they behave in pure JSON and after that implement them using NEST

Here is a bulk import of the tweet sample data they use in a lot of the examples

	POST /_bulk
	{ "create": { "_index": "us", "_type": "user", "_id": "1" }}
	{ "email" : "john@smith.com", "name" : "John Smith", "username" : "@john" }
	{ "create": { "_index": "gb", "_type": "user", "_id": "2" }}
	{ "email" : "mary@jones.com", "name" : "Mary Jones", "username" : "@mary" }
	{ "create": { "_index": "gb", "_type": "tweet", "_id": "3" }}
	{ "date" : "2014-09-13", "name" : "Mary Jones", "tweet" : "Elasticsearch means full text search has never been so easy", "user_id" : 2 }
	{ "create": { "_index": "us", "_type": "tweet", "_id": "4" }}
	{ "date" : "2014-09-14", "name" : "John Smith", "tweet" : "@mary it is not just text, it does everything", "user_id" : 1 }
	{ "create": { "_index": "gb", "_type": "tweet", "_id": "5" }}
	{ "date" : "2014-09-15", "name" : "Mary Jones", "tweet" : "However did I manage before Elasticsearch?", "user_id" : 2 }
	{ "create": { "_index": "us", "_type": "tweet", "_id": "6" }}
	{ "date" : "2014-09-16", "name" : "John Smith",  "tweet" : "The Elasticsearch API is really easy to use", "user_id" : 1 }
	{ "create": { "_index": "gb", "_type": "tweet", "_id": "7" }}
	{ "date" : "2014-09-17", "name" : "Mary Jones", "tweet" : "The Query DSL is really powerful and flexible", "user_id" : 2 }
	{ "create": { "_index": "us", "_type": "tweet", "_id": "8" }}
	{ "date" : "2014-09-18", "name" : "John Smith", "user_id" : 1 }
	{ "create": { "_index": "gb", "_type": "tweet", "_id": "9" }}


##Mapping and Analytics##

mapping and analytics is a introduction to how the basics of mapping works and how analyzers are used to analyze fulltext strings and break them into tokens.

1. [mapping and analytics](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/mapping-analysis.html)
	1. [dealing with human language](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/languages.html)
	1. [analysis and analyzers](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/analysis-intro.html)
		1. [analysis reference link](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/analysis.html)
		1. [using _analyze to test analyzers on text samples](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/indices-analyze.html#indices-analyze)
	2. [basic mapping](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/mapping-intro.html)
		1. [dynamic date formats](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/mapping-root-object-type.html#_dynamic_date_formats)
		1. [multi fields](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/mapping-core-types.html#_multi_fields_3)
		1. [dynamic templates](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/mapping-root-object-type.html#_dynamic_templates)
	3. [complex core fields](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/complex-core-fields.html)

Here are a few things that would be good to try out in this secion

- **Things to learn**
	- Create and delete indexes
	- add mappings to indexes
	- Try combining dynamic templates and multifields see [http://tsswks01.vertica.dk:9200/da-dk/_mapping/product?pretty](http://tsswks01.vertica.dk:9200/da-dk/_mapping/product?pretty) for details
	- use _analyze to test out the danish analyzer to see how the tokens look
	- create a custom analyzer using using a combination of the keyword analyzer and a lowercase filter, this is a great analyzer for ID's from SQL

## Using Queries and Filters ##
In this section we will look at the types of queries and filters in Elasticsearch and get a understanding of what queries and filters are used for

1.	[search - the basic tools](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/search.html)
2.	[full-body search](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/full-body-search.html)
3.	[search in depth](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/search-in-depth.html)
4.	[the most important queries and filters](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/_most_important_queries_and_filters.html)
5.	[query dsl - reference](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl.html)

- **Things to learn**
	- Whats the difference between a query and a filter?
	- how do you use a match query to search multiple fields?
	- how do you filter a search result so that you only get the results that are newer than the specified date?
	- how do you use bool filters and queries to structure complex searches?
	- why is the order of filters important for performance?
	- does Elasticsearch start with filtering or querying when performing a search request?

## Facetting using Aggregations ##
In this section we will look at the types of queries and filters in Elasticsearch and get a understanding of what queries and filters are used for

Sample data used for aggregations

	POST /cars/transactions/_bulk
	{ "index": {}}
	{ "price" : 10000, "color" : "red", "make" : "honda", "sold" : "2014-10-28" }
	{ "index": {}}
	{ "price" : 20000, "color" : "red", "make" : "honda", "sold" : "2014-11-05" }
	{ "index": {}}
	{ "price" : 30000, "color" : "green", "make" : "ford", "sold" : "2014-05-18" }
	{ "index": {}}
	{ "price" : 15000, "color" : "blue", "make" : "toyota", "sold" : "2014-07-02" }
	{ "index": {}}
	{ "price" : 12000, "color" : "green", "make" : "toyota", "sold" : "2014-08-19" }
	{ "index": {}}
	{ "price" : 20000, "color" : "red", "make" : "honda", "sold" : "2014-11-05" }
	{ "index": {}}
	{ "price" : 80000, "color" : "red", "make" : "bmw", "sold" : "2014-01-01" }
	{ "index": {}}
	{ "price" : 25000, "color" : "blue", "make" : "ford", "sold" : "2014-02-12" }


1.	[aggregations](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/aggregations.html)
	1.	[aggregation test drive](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/_aggregation_test_drive.html) go through the sub topics
	1.	[filtered queries and aggregations](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/_filtering_queries_and_aggregations.html)
4.	[aggregations reference](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/search-aggregations.html)
	1.	[terms aggregation](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/search-aggregations-bucket-terms-aggregation.html) the most used aggregation
	1.	[range aggregation](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/search-aggregations-bucket-range-aggregation.html) and the one used for most ranges
5.	[query dsl - reference](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl.html)

- **Things to learn**
	- Try using two aggs in a single request and filter both down like one value was selected what is returned in the actual results for the whole query?
	- Try using the range on a number field
	- Try combining a match query with filters and aggregations
	- why should most facet data be indexed as not_analyzed?


##Cluster failover##

Try starting multiple instances of Elasticsearch and configure NEST to use a list of Uri's in the connections settings 

Elasticsearch automaticly maps the next free port to any extra nodes started on the same machine so try with tree nodes and the addresses should be localhost:9200, localhost:9201, localhost:9202

verify that the indexed data has been distributed across the cluster

create a loop that searches into the index every 1 seconds and try closing closing a node.

- **Things to learn**
	- Does the failover kick in?
	- What options are there for failover configuration in NEST?
	


