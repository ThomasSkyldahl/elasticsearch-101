#Getting Started with Elasticsearch.net and NEST#

So first of we need to create a new project

Create a Console Application and reference the nuget package for [NEST](https://www.nuget.org/packages/NEST/)

Setting up the basic connection to Elasticsearch looks like the following

	var uri = new Uri("http://localhost:9200"); // replace localhost with ipv4.fiddler to see the traffic in fiddler
	var settings = new ConnectionSettings(uri).SetDefaultIndex("sample");
	var client = new ElasticClient(settings);

	// Index a customer
	client.Index<Customer>(new IndexRequest<Customer>(new Customer
			{ 
				Id = "vertica", 
				ContactName = "Sune Hansen",
				CompanyName = "Vertica A/S",
				Address = "Studsgade 29",
				City = "Aarhus C",
				PostalCode = "DK-8000",
				Country = "Danmark"
			}
		)
	);

	public class Customer {
		public string Id { get; set; }
		public string CompanyName{ get; set; }
		public string ContactName{ get; set; }
		public string ContactTitle{ get; set; }
		public string Address{ get; set; }
		public string City{ get; set; }
		public string PostalCode{ get; set; }
		public string Country{ get; set; }
		public string Phone{ get; set; }
		public string Fax{ get; set; }
	}

*If it makes sense for you you could now add a test framework and use it to implement all the samples*

##After setting up the basics##

Try running over the basics from [Indexing Documents](indexing-documents.md) using NEST to see the differences in the API.

Use both the Object request model and the expression request model for doing requests to see what you like the best