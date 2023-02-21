# Updating dates

## Date data types

​	There are four ways to create date/time attributes:

- `Date()`: returns the current date as `string`.
- `new Date()`: returns the current date as a UTC date object (ISODate).
- `new Date('YYYY-mm-ddTHH:MM:ssZ')`:
- `new Timestamp()`: returns the current timestamp.

​	Example:

```javascript
db.example.insertOne({
	_id: 1,
    date: new Date(),
    date_string: Date(),
    custom_date: new Date('2021-08'),
    timestamp: new Timestamp()
})
```

## Updating attributes

- `$currentDate`: sets to the current date.
  - Syntax: `{ $currentDate: { <attribute>: { $type: <type> } }, <...> }`
  - Example:

```javascript
db.example.updateOne(
  { _id: 1 },
  {
    $currentDate: {
      date: true,
      date_string: { $type: 'date' },
      custom_date: { $type: 'date' },
      timestamp: { $type: 'timestamp' }
    }
  }
)
```

