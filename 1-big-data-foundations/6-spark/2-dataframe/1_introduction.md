# DataFrame

​	Dataframes are a way of representing structured and unstructured data in the form of a table.

### Languages

​	Dataframes are used in all the languages supported by Spark, except for R.

### Operations

​	In a dataframe, there are two common operations:

- Transformation:
  - Dataframes are immutable. That means that transformations actually creates new dataframes.
    - This is pretty common in functional languages, such as Scala.
  - Depending on the transformation, the result may be a dataset, a more performative way of representing data.
    - This is one of the reasons why Scala is more performative than Python: Python doesn't have a built-in dataset data type.
- Action.
