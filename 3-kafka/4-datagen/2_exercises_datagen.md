# Exercises - Datagen

1. Create the topic `users` with the data from `ksql-datagen`.

- `quickstart=users`
- `topic=users`

```bash
ksql-datagen \
bootstrap-server=broker:29092 \
schemaRegistryUrl=schema-registry:8081 \
quickstart=users \
topic=users
# outputed a lot of stuff
```

2. Visualize the data from the topic through KSQL.

```sql
print 'users';
-- outputed a lot of stuff too
```

3. Create the stream `users_raw` with the data from the topic `users` with the following properties:

- `kafka_topic='users'`
- `value_format='JSON'`
- `key='userid'`
- `timestamp='registertime'`

```sql
create stream users_raw (
    userid varchar,
    registertime bigint
) with (
    kafka_topic='users',
    value_format='json',
    key='userid',
    timestamp='registertime'
);
-- output:
-- 
--  Message        
-- ----------------
--  Stream created 
-- ----------------
```

4. Visualize the structure of the stream `users_raw`.

```sql
describe users_raw;
-- output:
-- 
-- Name                 : USERS_RAW
--  Field        | Type                      
-- ------------------------------------------
--  ROWTIME      | BIGINT           (system) 
--  ROWKEY       | VARCHAR(STRING)  (system) 
--  USERID       | VARCHAR(STRING)           
--  REGISTERTIME | BIGINT                    
-- ------------------------------------------
-- For runtime statistics and query details run: DESCRIBE EXTENDED <Stream,Table>;
```

5. Visualize the data from the stream `users_raw`.

```sql
select * from users_raw emit changes limit 10;
-- output:
-- +-----------------------------------------+-----------------------------------------+-----------------------------------------+-----------------------------------------+
-- |ROWTIME                                  |ROWKEY                                   |USERID                                   |REGISTERTIME                             |
-- +-----------------------------------------+-----------------------------------------+-----------------------------------------+-----------------------------------------+
-- |1501215197826                            |User_6                                   |User_6                                   |1501215197826                            |
-- |1505765682702                            |User_1                                   |User_1                                   |1505765682702                            |
-- |1518032590819                            |User_9                                   |User_9                                   |1518032590819                            |
-- |1511731626580                            |User_8                                   |User_8                                   |1511731626580                            |
-- |1493877005295                            |User_1                                   |User_1                                   |1493877005295                            |
-- |1495649458502                            |User_1                                   |User_1                                   |1495649458502                            |
-- |1496382564112                            |User_7                                   |User_7                                   |1496382564112                            |
-- |1487832244946                            |User_1                                   |User_1                                   |1487832244946                            |
-- |1498415575545                            |User_8                                   |User_8                                   |1498415575545                            |
-- |1494068819027                            |User_6                                   |User_6                                   |1494068819027                            |
-- Limit Reached
-- Query terminated
```

6. Repeat all this process to the topic `pageviews`.


- `ksql-datagen quickstart=pageviews topic=pageviews`

```bash
# 1
ksql-datagen \
bootstrap-server=broker:29092 \
schemaRegistryUrl=schema-registry:8081 \
quickstart=pageviews \
topic=pageviews
# outputed a lot of stuff
```

```sql
-- 2
print 'pageviews';
-- outputed a lot of stuff too

-- 3
create stream pageviews_raw(
    pageid varchar,
    viewtime bigint
) with (
    kafka_topic='pageviews',
    value_format='json',
    key='pageid',
    timestamp='viewtime'
);
-- output:
-- 
--  Message        
-- ----------------
--  Stream created 
-- ----------------

-- 4
describe pageviews_raw;
-- output:
-- 
-- Name                 : PAGEVIEWS_RAW
--  Field    | Type                      
-- --------------------------------------
--  ROWTIME  | BIGINT           (system) 
--  ROWKEY   | VARCHAR(STRING)  (system) 
--  PAGEID   | VARCHAR(STRING)           
--  VIEWTIME | BIGINT                    

-- 5
select * from pageviews_raw emit changes limit 10;
-- output:
-- 
-- +-----------------------------------------------------+-----------------------------------------------------+-----------------------------------------------------+-----------------------------------------------------+
-- |ROWTIME                                              |ROWKEY                                               |PAGEID                                               |VIEWTIME                                             |
-- +-----------------------------------------------------+-----------------------------------------------------+-----------------------------------------------------+-----------------------------------------------------+
-- |1647208900012                                        |�M%�                                             |Page_54                                              |1647208900012                                        |
-- |1647208900505                                        |�M'�                                             |Page_23                                              |1647208900505                                        |
-- |1647208900506                                        |�M'�                                             |Page_78                                              |1647208900506                                        |
-- |1647208900506                                        |�M'�                                             |Page_48                                              |1647208900506                                        |
-- |1647208900506                                        |�M'�                                             |Page_99                                              |1647208900506                                        |
-- |1647208900507                                        |�M'�                                             |Page_96                                              |1647208900507                                        |
-- |1647208900507                                        |�M'�                                             |Page_15                                              |1647208900507                                        |
-- |1647208900508                                        |�M'�                                             |Page_54                                              |1647208900508                                        |
-- |1647208900508                                        |�M'�                                             |Page_81                                              |1647208900508                                        |
-- |1647208900509                                        |�M'�                                             |Page_31                                              |1647208900509                                        |
-- Limit Reached
-- Query terminated
```