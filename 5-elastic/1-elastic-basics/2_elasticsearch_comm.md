# Communication with Elasticsearch

​	The communication with the Elasticsearch is done through a REST API. The JSON body is sent in a HTTP request:

- HEAD
- GET
- POST
- PUT
- DELETE

​	Structure of a request: `<action> address:door/index/<options>`
​	Example: `PUT localhost:9200/client/_create`

​	The community is responsible for creating and mantaining many clients to access Elastic through programming languages, such as C#, Go, Java, Javacript, Python and many others.
