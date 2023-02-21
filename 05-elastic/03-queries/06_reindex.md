# Reindex

​	Every time we need to alter the mapping of a document, we will need to reindex this data.

​	The most basic way of reindex consists in two simple steps:

- setting a new index, with the new mapping and metadata; and
- use it as destiny (`"dest"`) on a reindex operation, with the old index as source (`"source"`).

​	Example:

```bash
POST _reindex
{
  "source": {
    "index": "test"
  },
  "dest": {
    "index": "new_test"
  }
}
```
