# Shards

​	MongoDB fragments data at a collection level, so a shard is like a piece of our data inside the cluster.

## Structure

- Shard
  - Keeps a subset of the data.
  - Can be implemented as a replica set.
  - Horizontal scalability.
- Config Servers
  - Stores metadata.
  - Clusters configurations.
- Mongos: interface between the application and the shard cluster.

![Diagram of a sample sharded cluster for production purposes.  Contains exactly 3 config servers, 2 or more ``mongos`` query routers, and at least 2 shards. The shards are replica sets.](https://docs.mongodb.com/manual/images/sharded-cluster-production-architecture.bakedsvg.svg)
