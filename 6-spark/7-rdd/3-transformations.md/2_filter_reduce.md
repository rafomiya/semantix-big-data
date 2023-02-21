# Filter & Reduce

​	Now, we will see two new transformations: filter and reduce.

## Filter

​	The filter removes rows from the original dataframe, filtering the results.
​	It takes a boolean function as parameter. This function is applied to each item, and it works like a "test". If the item doesn't passes the test, it is removed (filtered).

​	Example:

```python
fA = words.filter(lambda x: x.lower().startswith("a"))
fLength = words.filter(lambda x: len(x) > 5)
fEven = numbers.filter(lambda x: x % 2 == 0)
```

## Reduce

​	Example: below, we have a dataframe in which each word is the key of a key-value pair, and the value is always `1`.

```python
lowerWithLength = words.flatMap(lambda x: x.split()).map(lambda x: x.lower()).map(lambda x: (x, 1))
lowerWithLength.collect()
# output:
# [('big', 1),
#  ('data', 1),
#  ('2019', 1),
#  ('semantix', 1),
#  ('hadoop', 1),
#  ('semantix', 1),
#  ('sp', 1),
#  ('hadoop', 1),
#  ('2019', 1),
#  ('curso', 1),
#  ('hadoop', 1),
#  ('data', 1),
#  ('hadoop', 1),
#  ('semantix', 1),
#  ('sp', 1),
#  ('data', 1)]
```

​	We can use a `reduceByKey` to get the amount of times each word appears:

```scala
val amountAppearances = lowerWithLength.reduceByKey(_+_)
amountAppearances.take(3)
// [('big', 1),
//  ('2019', 2),
//  ('hadoop', 4)]
```
