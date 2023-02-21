# Redis

​	Redis stands for **Re**mote **Di**ctionary **S**erver. It is a NoSQL database engine, the most used to handle key-value structures. NoSQL stands for "not only SQL", meaning its manipulation isn't done just with the structured query language (SQL).

​	Characteristics:

- Distributed architecture.
- Fluid schema.
- Horizontal scalability.
- High performance.
- In memory storage.
  - Fast read/write data operations.
- It is not the kind of database to store **all** your data.
- TCP server.
  - Client-server architecture.
  - Atomic commands.
    - Single-threaded.
    - One command at a time.
  - Done through an application or the Redis CLI.

## Types of databases:

- SQL: row oriented (MySQL, Oracle, PostgreSQL, etc)
- NoSQL:
  - Column oriented (Cassandra).
  - Key-value oriented (Redis).
    - Simpler structures.
  - Graph oriented (Neo4j).
  - Document oriented (MongoDB).
  - Others.

## History

- Created by Salvatore Sanfilippo in 2009.
- Sponsored by Pivotal Software and Vmware.
- Became Redis Labs in 2015.
