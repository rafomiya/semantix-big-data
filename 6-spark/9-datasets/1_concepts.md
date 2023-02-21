# Dataset Concepts

​	A dataset is nothing more than a distributed collection of objects, with a strong typing. For that reason, there are no datasets in Python, since it is a dynamically typed language.

​	Characteristics:

- Mapped for a relational schema.
    - The schema is defined by an enconder.
    - Is related to the creation of Java Bean objects (in Java) or Case Classes (In Scala).
- Optimized by Catalyst.
- Implemented only in Java and Scala.

## Dataset vs. Dataframe

​	Dataframes:

- Table based data.
- Dynamically typed transformations.
    - Rows can contain data of any type.
    - Defined schemes are not applied until execution time.

​	Datasets:

- Represents typed and object oriented data.
- Strongly typed transformations.
    - Object's properties are typed in compilation time.

​	Spark's data representation timeline:

- 2011: RDD (version 1.0)
- 2013: Dataframe (version 1.3)
- 2015: Dataset (version 1.6)
