# Mapping

​	At each PUT/POST on our indexes, Elastic tries to define a mapping (equivalent to schema in a SQL analogy) for our data.

​	If you want to see this mapping:

```bash
GET client/_mapping
```

## Data types

​	Core:

- Text:
    - `text`
    - `keyword`
- Number:
    - `long`
    - `integer`
    - `short`
    - `byte`
    - `double`
    - `float`
- `Date`
- `Binary`
- `Boolean`
- `Ip`

​	Complex:

- `Object`
- `Nested`

## Get mappings:

```bash
GET product/_mapping
GET product/_mapping/field/name
GET product/_mapping/field/name,price,descript*
```

## Define mapping

```bash
PUT product/_mapping/
{
  "properties": {
    "name": { "type": "text" },
    "price": { "type": "long" },
    "quantity" { "type": "long" }
  }
}
```
