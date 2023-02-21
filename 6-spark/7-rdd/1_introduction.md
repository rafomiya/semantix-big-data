# RDD

​	RDD was the first type of data format in Spark. After RDD, dataframes and datasets were created.
​	RDD stands for **R**esilient **D**istributed **D**atasets:

- Resilient: it can recreate data lost in memory.
- Distributed: runs in a cluster.
- Datasets: data can be created or imported from other sources.

​	In short, RDD is a collection of objects distributed across the nodes of a cluster. They are immutable and have two types of operations: **actions** and **transformations**.

## Operations

- Action: returns a value.
    - Collect
    - Count
    - First
    - Take
    - Reduce
    - CountByKey
    - Foreach
- Transformation: returns a new RDD.
    - Map
    - Filter
    - FlatMap
    - GroupByKey
    - ReduceByKey
    - AggregateByKey
