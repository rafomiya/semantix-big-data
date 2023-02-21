# Replica Set

​	In MongoDB, a replica set is a set of `mongod` (nodes) that keeps the same data. It provides data redundancy and increases the data availability.

## Structure

- Primary Node (1): one of the nodes is elected to be the primary node. It will receive all the write operations and register them into the `oplog` (operation log).
- Secondary Nodes (N): from times to times, the remaining nodes will replicate the `oplog` from the primary node.

![Diagram of default routing of reads and writes to the primary.](https://docs.mongodb.com/manual/images/replica-set-read-write-operations-primary.bakedsvg.svg)

​	Since the read requests would go from the primary to the secondary nodes, you can configure your replica set to sent the read requests directly to the secondary nodes.

![Diagram of an application that uses read preference secondary.](https://docs.mongodb.com/manual/images/replica-set-read-preference-secondary.bakedsvg.svg)

### Failure on the primary node

​	When the primary node goes down for more than the `electionTimeoutMillis` (10 seconds by default), the cluster no longer processes write operations. After that, a valid secondary node calls for an election to nominate itself as the new primary node. The cluster attempts to complete the election of a new primary and resume normal operations.

![Diagram of an election of a new primary. In a three member replica set with two secondaries, the primary becomes unreachable. The loss of a primary triggers an election where one of the secondaries becomes the new primary](https://docs.mongodb.com/manual/images/replica-set-trigger-election.bakedsvg.svg)

## Replica set commands

- `rs.conf()`: displays the configurations of the replica set.
- `rs.status()`: displays the current status of the replica set.
