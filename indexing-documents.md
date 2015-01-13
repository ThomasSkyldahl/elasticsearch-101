#Indexing Documents#

##Get a tool that's good for REST or Elasticsearch##
First of we need some kind of tool for posting content to Elasticsearch

There are a lot of good tools to use for REST based services 

- [Fiddler](http://www.telerik.com/fiddler) - use **ipv4.localhost:9200** to see requests in Fiddler
- [cURL](http://curl.haxx.se/download.html)
- [DHC](https://chrome.google.com/webstore/detail/dhc-resthttp-api-client/aejoelaoggembcahagimdiliamlcdmfm?utm_source=chrome-ntp-icon) - *this is a chrome plugin DHC is short for (Dev HTTP Client)*

### I would recommend ###

The Elasticsearch specific chrome plugin [Sense (Beta)](https://chrome.google.com/webstore/detail/sense-beta/lhjgkmllcaadmopgmanpapmpjgmfcfig?utm_source=chrome-ntp-icon)


Sense has autocomplete for the Elasticsearch API and is a great way to explore the API, 
Sense is also integrated into [Marvel](http://www.elasticsearch.org/overview/marvel/) but we will get back to that later.

You can also install the Elasticsearch Marvel plugin by running:

    bin/plugin.bat -i elasticsearch/marvel/latest

Restart Elasticsearch after this and you should be able to access [http://localhost:9200/_plugin/marvel/](http://localhost:9200/_plugin/marvel/)

Marvel gives realtime insights into the cluster and also contains Sense, its free for Development.

## Indexing a Document ##

See [http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/data-in-data-out.html](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/data-in-data-out.html) for detailes about managing documents in Elasticsearch

### Lets get started by adding some data ###

	PUT /hello_index/hello_type/1
	{
    	"message": "Hello world!!"
	}

In the code you can see the url structure of how documents are placed in Elasticsearch

*hello_index* is the index name

*hello_type* is the type of the document

*1* is the id of the document.


### Getting the document back from Elasticsearch ###

	GET /hello_index/hello_type/1

Now you should see the following

    {
       "_index": "hello_index",
       "_type": "hello_type",
       "_id": "1",
       "_version": 1,
       "found": true,
       "_source": {
       		"message": "Hello world!!"
       }
    }

### Updating documents ###

Try running the **PUT** command again

#### Optimistic Concurrency Control ####

Did you see how the _version was changed to 2 in the update?

the _version can be used for *optimistic concurrency control*

try running the following command

	PUT /hello_index/hello_type/1?version=1
	{
    	"message": "Hello world!!"
	}

This should fail with a status 409 telling you what the expected version was in the error message

Now try using the version found in the error message and see what happens.

You can read more about [optimistic concurrency control in Elasticsearch here](http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/optimistic-concurrency-control.html)