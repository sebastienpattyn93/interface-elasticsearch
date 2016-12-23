# Elasticsearch Interface

 This is a Juju charm interface layer. This interface is used for
 connecting to an Elasticsearch unit.

### Examples

#### Requires

If your charm needs to connect to ElasticSearch:

  `metadata.yaml`

```yaml
requires:
  elasticsearch:
    interface: elasticsearch
```

  `layer.yaml`

```yaml
includes: ['interface:elasticsearch']
```  

  `reactive/code.py`

```python
@when('elasticsearch.available')
def connect_to_elasticsearch(elasticsearch):
    print(elasticsearch.host())
    print(elasticsearch.port())
    print(elasticsearch.cluster_name())

```


#### Provides

If your charm needs to provide Elasticsearch connection details:

  `metadata.yaml`

```yaml
provides:
  elasticsearch:
    interface: elasticsearch
```

  `layer.yaml`

```yaml
includes: ['interface:elasticsearch']
```

  `reactive/code.py`

```python
@when('client.connected', 'elasticsearch.configured')
def connect_to_client(connected_clients):
    conf = config()
    cluster_name = conf['cluster-name']
    port = conf['port']
    connected_clients.configure(port, cluster_name)
    clients = connected_clients.list_connected_clients_data
    for c in clients:
        //do something
```

### States

**{relation_name}.connected** - Denotes that the client has connected to the
Elasticsearch node(s), but has not yet received the data to configure the
connection.

**{relation_name}.available** - Denotes that the client has connected and
received all the information from the provider to make the connection.

**{relation_name}.departed** - Denotes that the unit has departed from the
 Elasticsearch relationship, and should be removed from any configuration
 files, etc.

### Data

- **host** - The units private address
- **port** - TCP Port to use
- **cluster_name** - The Elasticsearch clusters' name

## Maintainers

 - Matt Bruzek &lt;matthew.bruzek@canonical.com&gt;
 - Charles Butler &lt;charles.butler@canonical.com&gt;
