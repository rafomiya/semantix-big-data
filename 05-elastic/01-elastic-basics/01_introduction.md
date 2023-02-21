# Elastic

​	The entire Elastic architecture was made to solve the search problem. It has three main components:

- Elasticsearch
  - Search engine and analytics, highly scalable.
  - Database.
- Logstash
  - Transport between origin and destiny.
- Kibana
  - Elastic's GUI.
  - Data visualization.
  - Elasticsearch management.

## RDBMS vs. Elastic

| RDBMS    | Elastic   |
| -------- | --------- |
| Database | Index     |
| Table    | Type      |
| Schema   | Mapping   |
| Row      | Document  |
| Column   | Attribute |

​	Since newer versions, indexes can have only one type.

## Indexes

- Shards: divisions of the index. Stores the data.
- Alias: virtual link for a real index. Works like a nickname. It is possible to associate an alias to more than one index, creating groups of indexes.
- Analyzer: full text searches and exact values.
- Mapping: the structure of the data, like a schema.
