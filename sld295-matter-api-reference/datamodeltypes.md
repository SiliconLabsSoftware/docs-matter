# Data Models

The Data Model defines namespaces for endpoints, clusters, and attributes in the application. From a developper standpoint, this is handled by the ZAP tool. For Multi-Fabric devices, the data model is shared between the Fabrics.

For an review of what the Matter Data Model is and how it is used, see the [Matter Data Model](../sld288-matter-fundamentals-data-model/index.md).

## APIs

The directory [```/src/app/util```](https://github.com/SiliconLabs/matter_extension/tree/main/third_party/matter_sdk/src/app/util) contains various utilities and some of the external API headers for interacting with the data model layer. In particular, the various data type definitions and the public APIs to the data model are declared in the headers here.

## Header File

This file contains definitions and constants for various data types and identifiers used in Matter.

- [DataModelTypes](https://github.com/SiliconLabs/matter_extension/blob/main/src/lib/core/DataModelTypes.h)
