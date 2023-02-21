# Control Center

​	Control Center is a GUI to monitor and manage Confluent. With this tool, you are able to manage brokers, topics, consumer groups, connectors and all the data flux. Beyond that, you can create alerts and develop using ksqlDB.

​	In our cluster, the Control Center can be accessed at http://localhost:9021.

## Creating topics

​	Required parameters:

- Name.
- Amount of partitions.

​	Extra settings:

- Availability.
  - Maximum: RF = 3 and min ISRs = 1
  - Balanced: RF = 3 and min ISRs = 2
  - Moderate: RF = 2 and min ISRs = 1
  - Low (do not use in production!): RF = 1 and min ISRs = 1

- Cleanup policy.
- Max message size.
