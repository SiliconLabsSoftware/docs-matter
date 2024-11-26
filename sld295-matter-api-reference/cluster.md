# Cluster

Each Cluster is either a Client, Server, or both​. A Cluster is a collection of Attributes and Commands that are logically related.

- Client: Stateless. Interacts with a server cluster by Reading, Writing, or Subscribing to an attribute​
- Server: Holds the State of Data or Attribute

Clusters contain: Attributes, Events, Commands​.

For more details see: [Matter Data Model](../sld288-matter-fundamentals-data-model/index.md/##Clusters).

## Header File

The header file below contains namespaces and IDs of Clusters. In Simplicity Studio, this will be generated in the autogen/zap-generated/ folder of the matter project.

- [Cluster](https://github.com/project-chip/connectedhomeip/tree/master/zzz_generated/app-common/app-common/zap-generated/ids/Clusters.h)
