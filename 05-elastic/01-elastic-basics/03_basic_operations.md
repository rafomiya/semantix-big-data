# Basic Operations

- HEAD: returns the HTTP header, commonly used to know if the document exists.

  - `curl -XHEAD -v http://localhost:9200/client/_doc/1`
  - `HEAD client/_doc/1`

- PUT: create or reindex an entire document.

  - ```bash
    PUT client/_create/1
    {
    	"nome": "Luke",
    	"age": 23
    }
    # with `_create`, the document is only indexed if it doesn't exists yet.
    ```
  - ```bash
    PUT client/_doc/1
    {
    	"nome": "Luke",
    	"age": 23
    }
    # with `_doc`, the document is created or updated, depending on if it already exists or not.
    ```

- POST: create a document with `_id` or partially update a document.

  - ```bash
    POST client/_update/1
    {
    	"doc": {
    		"name": "Skywalker"
    	}
    }
    # updates only the `name` of the document of id 1
    ```

  - ```bash
    POST client/_doc
    {
    	"name": "Skywalker"
    }
    # creates the document with an incremental id
    ```

- DELETE: deletes a document or an entire index.

  - ```bash
    DELETE client/_doc/1
    # deletes the client of `id` 1
    ```

  - ```bash
    DELETE client
    # deletes the entire index `client`
    ```

- GET: retrieves information from the indexes.

  - ```bash
    # gets informations about the elasticsearch node
    GET /

    # gets all the documents from an index
    GET client/_search

    # gets a specific document from an index
    GET client/_doc/1

    # gets the amount of documents inside an index
    GET client/_count

    # gets the data from a specific document from and index
    GET client/_source/1
    # SQL equivalent to 'select * from client where id = 1'
    ```


