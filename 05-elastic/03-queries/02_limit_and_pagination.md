# Limit and Pagination

​	When retrieving results from a query, we can increase readability and performance limiting the amount of results and paginating them.

- Size: an integer defining the amount of results to be retrieved.
- From: an integer defining from which document the results are gonna be shown.

​	Examples:

- `GET products/_serch?q=mouse&size=3&from=7`. The results retrieved are of number 7, 8, 9.
- `GET products/_search?q=laptop&size=100&from=300`: shows results from 300 to 399.
- ```
  GET products/_search
  {
  	"size": 100,
  	"from": 300,
  	"query": {
  		...
  	}
  }
  ```
  
- `GET products/_search?q=mouse`: by default, `size=10` and `from=0`.

​	In short, to define the `from` and `size` parameters:

- First document of the results (starting by 1): `from + 1`
- Last document of the results: `from + size`
- Page: `from / size + 1`