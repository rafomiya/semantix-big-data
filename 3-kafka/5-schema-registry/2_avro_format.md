# The Avro Format

## What is Avro?

​	Avro is a data serialization structure based on the JSON format. It is a binary format, meaning it is compact and not human readable.

​	Advantages:

- The schema of the data is stored separated from the data itself.
- The data is automatically compressed.
- The documentation is embedded into the schema, and it is possible to documentate field by field.
- Supported by Hadoop and many other big data technologies.
- The schema can evolve through time in a safe way.

## Schemes in Avro

​	Schemes are stored in JSON in Avro.

​	The following fields are defines:

- `name`: the name of the schema.
- `namespace`: equivalent to the Java package (optional).
- `doc`: the documentation (optional).
- `aliases`: other names for the schema (optional).
- `type`: the schema type. It will usually be `'record'`.
- `fields`: 
  - `name`: the name of the field.
  - `doc`: the field documentation (optional).
  - `type`: the type of the field.
  - `default`: the default value for the field (optional).

### Avro Schema Example 

​	Fields of the schema: `id`, `name` and `status`.

​	File `names.avsc`

```json
{
    "type": "record",
    "name": "user",
    "namespace": "example.avro",
    "doc": "Example of a user schema",
    "fields": [
        { "name": "id", "type": "int" },
        { "name": "name", "type": "string" },
        { "name": "status", "type": "boolean", "default": true }
    ]
}
```

