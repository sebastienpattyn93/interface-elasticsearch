# Elasticsearch Interface

> Used to connect an Elasticsearch client to an Elasticsearch charm

### Usage

assuming you have a `requires` block in `metadata.yaml` accompanied by `interface:elasticsearch` in `layer.yaml`:

     requires:
       elasticsearch:
         interface: elasticsearch

then you can consume the cluster as follows:

     @when('elasticsearch.available')
     def connect_to_elasticsearch(elasticsearch):
         print(elasticsearch.host())
         print(elasticsearch.port())
         print(elasticsearch.cluster_name())


#### States

**elasticsearch.connected** - Denotes that the client has connected to the
elasticsearch node(s), but has not yet received the data to configure the
connection.

**elasticsearch.available** - Denotes that the client has connected and received
all the information from the provider to make the connection.

**elasticsearch.departed** - Denotes that the unit has departed from the elasticsearch
relationship, and should be removed from any configuration files, etc.

## Maintainers
 
 - [Matt Bruzek](mailto:matthew.bruzek@canonical.com) &lt;matthew.bruzek@canonical.com&gt;
 - [Charles Butler](mailto:charles.butler@canonical.com) &lt;charles.butler@canonical.com&gt;
