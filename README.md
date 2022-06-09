# Kibana

notes and projects to understand how to use Kibana

## Kibana and Elasticsearch

Elasticsearch is powering a lot of apps that people use on a daily basis:

- uber
- twilio
- adobe
- docker
- shopify
- tinder
- github
- instacart

Its a popular search function.

## Elastic Stack

This is a great tool to know. This stack is free and open source. It consists of four main tech:

- beats
- logstash
- elasticsearch
- kibana

This stack allows you to take data in any format and search and visualize it in real time.

most popular uses are:

- loggging
- metrics
- security analytics
- business analytics

The Elastic stack is this collection of products that can be mixed and matched to serve specific use-cases.

## Basics

### Elasticsearch

This is the heart of the Elastic Stack. This is where you can store, search and analyze your data.

Think about having a full stack app connected to a database. This stores all the product data and also all of the website information.

A great search experience is key to having customers by and return to your platform. Want our customers to get fast and relevant results no matter the scale.

Chances are you are workign with a large data set in a relational database.

Fetching data from those tables can cause a lag in performance, which can reduce the customer base.

Another big search factor is relevance of results. You want to be able to set criteria to have the most relevant results returned at the top. This can also be used to correct spelling mistakes. Databases are not equipped to handle this directly.

So if speed and relevance are important for your search, elasticsearch can be great.

With elasticsearch, clients send results to the middleware which talks to elasticsearch instead of the database. It's built to send relevant results back to the server, which processes the results and sends it back to the client.

### Kibana

You can analyze the user behavior using your search engine through elasticsearch, and it can be visualized through Kibana.

think of kibana as a web interface to the data stored in elasticsearch. It searches, views, and interacts with data in elasticsearch.

Kibana sends queries to elasticsearch to get and visualize the results.

You can also create a dashboard in kibana to visualize the results in graphs tables and charts to share with stakeholders.

## Architecture of Elasticsearch

This is a powerful search and analytics engine that is a distributed system.

Once elasticsearch is running on your computer, as one node. Each node has a label and they belong to a specific cluster. Starting a node starts a cluster, and a cluster can have one or multiple nodes.

These nodes will all belong to a cluster and work together to accomplish a task, like a team that distributed.

These nodes are separate machines, and are assigned one or multiple roles. One of these roles could be to hold data.

Data is stored as json documents in elasticsearch.

The documents are grouped into an index by how they are related. For instance, a grocery store could be grouped in a produce index or a wine and beer index. Indexes group documents that are related to find data.

These indexes are stored across multiple nodes, much like a topic in kafka. These indexes have shards, which are like partitions in Kafka.

You search the shards in each node. An index can have multiple shards that are stored across nodes. This distribution of the shards has some superpowers to speed up searches. Shards hold the documents, not indexes.

When you create an index, one shard is created by default and then assigned to a node.

Shard sizes are based on the disk space on the node, so you can index data that's too large to fit on one node across multiple nodes.

Since data could grow past the size provisioned past the initial number of nodes. One of the advantages of sharding is the ability to scale quickly by adding nodes with new shards to an index when needed.

Shards are also where queries are searched, not indexes. As you distribute the number of documents across shards, you reduce the number of records to search through on each search, and you can parallelize the search across all the shards and reduce the time of the search exponentially.

The example was:

given 500k documents, storing all of them in one single shard and searching for one document would take 10 seconds. Distributing the documents across 10 shards, each shard would have 50k documents, and the search could be run in parallel. This would reduce the search time by a factor of 10, processing the same number of records. This is how you can meet the service level agreements of search times when scaling by calculating the number of shards needed to maintain a low latency on the search performance.

### Failures

One way to avoid losing data if nodes fail is to add replica shards into the cluster. This is another role a node can have.

A replica node stores copies of records from other shards.

As with Kafka, the replication factor may be good to keep at 3 (this is what AWS does automatically too).

Replica shards can also improve the performance of your search.

If you're only running the search on the two primary shards, as the number of searches increase, you can increase the number of replica shards to lower the search latency.

Replica shards are exact copies of the primary shards. This can handle increased demands on search.

### Hands on Lab

Goal is to get familiar with CRUD operations a document from elasticsearch.

To start elasticsearch, download and run `bin\elasticsearch.bat` on windows.

The standard port for elasticsearch is 9200.

## Questions

Think about the metrics that are a best fit for the use-case you have.

Elasticsearch doesn't support joins or transactions, so this may not be the right tool for these purposes..

There isn't a particular size of a SQL db that is recommended to switch over to Elasticsearch, but if you have metrics for your use-case that you aren't hitting that are around searching and receiving data, elasticsearch may be the answer.

There are some error messages in running elasticsearch with Kibana. When you start Kibana, its looking for elasticsearch, and it may fail when elasticsearch isn't fully loaded and available.

Does elasticsearch have support for security? you can protect your ports for free using the authentication credentials provided. There are tutorials for this.
