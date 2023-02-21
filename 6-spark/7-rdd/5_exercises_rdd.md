# Exercises - RDD

1. Read the local files of the directory `file:///opt/spark/logs/` as RDD.

```python
logs = sc.textFile("file:///opt/spark/logs")
logs.take(2)
# output:
# ['Spark Command: /opt/java/bin/java -cp /etc/spark/:/opt/spark/jars/*:/etc/hadoop/:/etc/hadoop/*:/opt/hadoop/share/hadoop/common/lib/*:/opt/hadoop/share/hadoop/common/*:/opt/hadoop/share/hadoop/hdfs/*:/opt/hadoop/share/hadoop/hdfs/lib/*:/opt/hadoop/share/hadoop/yarn/lib/*:/opt/hadoop/share/hadoop/yarn/*:/opt/hadoop/share/hadoop/mapreduce/lib/*:/opt/hadoop/share/hadoop/mapreduce/*:/opt/hadoop/share/hadoop/tools/lib/* -Xmx1g org.apache.spark.deploy.master.Master --host localhost --port 7077 --webui-port 8080',
#  '========================================']

```

2. Using the RDD created, perform the following operations:

1. Count the amount of rows.

```python
words.count()
# output:
# 30
```

2. Visualize the first row.

```python
words.first(1)
# output:
# 'Spark Command: /opt/java/bin/java -cp /etc/spark/:/opt/spark/jars/*:/etc/hadoop/:/etc/hadoop/*:/opt/hadoop/share/hadoop/common/lib/*:/opt/hadoop/share/hadoop/common/*:/opt/hadoop/share/hadoop/hdfs/*:/opt/hadoop/share/hadoop/hdfs/lib/*:/opt/hadoop/share/hadoop/yarn/lib/*:/opt/hadoop/share/hadoop/yarn/*:/opt/hadoop/share/hadoop/mapreduce/lib/*:/opt/hadoop/share/hadoop/mapreduce/*:/opt/hadoop/share/hadoop/tools/lib/* -Xmx1g org.apache.spark.deploy.master.Master --host localhost --port 7077 --webui-port 8080'
```

3. Visualize all the rows.

```python
words.collect()
# output:
# ['Spark Command: /opt/java/bin/java -cp /etc/spark/:/opt/spark/jars/*:/etc/hadoop/:/etc/hadoop/*:/opt/hadoop/share/hadoop/common/lib/*:/opt/hadoop/share/hadoop/common/*:/opt/hadoop/share/hadoop/hdfs/*:/opt/hadoop/share/hadoop/hdfs/lib/*:/opt/hadoop/share/hadoop/yarn/lib/*:/opt/hadoop/share/hadoop/yarn/*:/opt/hadoop/share/hadoop/mapreduce/lib/*:/opt/hadoop/share/hadoop/mapreduce/*:/opt/hadoop/share/hadoop/tools/lib/* -Xmx1g org.apache.spark.deploy.master.Master --host localhost --port 7077 --webui-port 8080',
#  '========================================',
#  '20/03/18 20:31:09 INFO master.Master: Started daemon with process name: 1087@jupyter-notebook',
#  '20/03/18 20:31:09 INFO util.SignalUtils: Registered signal handler for TERM',
#  '20/03/18 20:31:09 INFO util.SignalUtils: Registered signal handler for HUP',
#  '20/03/18 20:31:09 INFO util.SignalUtils: Registered signal handler for INT',
#  '20/03/18 20:31:10 INFO spark.SecurityManager: Changing view acls to: root',
#  '20/03/18 20:31:10 INFO spark.SecurityManager: Changing modify acls to: root',
#  '20/03/18 20:31:10 INFO spark.SecurityManager: Changing view acls groups to: ',
#  '20/03/18 20:31:10 INFO spark.SecurityManager: Changing modify acls groups to: ',
#  '20/03/18 20:31:10 INFO spark.SecurityManager: SecurityManager: authentication disabled; ui acls disabled; users  with view permissions: Set(root); groups with view permissions: Set(); users  with modify permissions: Set(root); groups with modify permissions: Set()',
#  "20/03/18 20:31:10 INFO util.Utils: Successfully started service 'sparkMaster' on port 7077.",
#  '20/03/18 20:31:10 INFO master.Master: Starting Spark master at spark://localhost:7077',
#  '20/03/18 20:31:10 INFO master.Master: Running Spark version 2.4.1',
#  '20/03/18 20:31:10 INFO util.log: Logging initialized @1454ms',
#  '20/03/18 20:31:10 INFO server.Server: jetty-9.3.z-SNAPSHOT, build timestamp: unknown, git hash: unknown',
#  '20/03/18 20:31:10 INFO server.Server: Started @1504ms',
#  '20/03/18 20:31:10 INFO server.AbstractConnector: Started ServerConnector@5526ec85{HTTP/1.1,[http/1.1]}{0.0.0.0:8080}',
#  "20/03/18 20:31:10 INFO util.Utils: Successfully started service 'MasterUI' on port 8080.",
#  '20/03/18 20:31:10 INFO handler.ContextHandler: Started o.s.j.s.ServletContextHandler@78c62b96{/app,null,AVAILABLE,@Spark}',
#  '20/03/18 20:31:10 INFO handler.ContextHandler: Started o.s.j.s.ServletContextHandler@1330e23c{/app/json,null,AVAILABLE,@Spark}',
#  '20/03/18 20:31:10 INFO handler.ContextHandler: Started o.s.j.s.ServletContextHandler@3f7fb168{/,null,AVAILABLE,@Spark}',
#  '20/03/18 20:31:10 INFO handler.ContextHandler: Started o.s.j.s.ServletContextHandler@50e5c33c{/json,null,AVAILABLE,@Spark}',
#  '20/03/18 20:31:10 INFO handler.ContextHandler: Started o.s.j.s.ServletContextHandler@44d0ea1e{/static,null,AVAILABLE,@Spark}',
#  '20/03/18 20:31:10 INFO handler.ContextHandler: Started o.s.j.s.ServletContextHandler@2a362185{/app/kill,null,AVAILABLE,@Spark}',
#  '20/03/18 20:31:10 INFO handler.ContextHandler: Started o.s.j.s.ServletContextHandler@222db61{/driver/kill,null,AVAILABLE,@Spark}',
#  '20/03/18 20:31:10 INFO ui.MasterWebUI: Bound MasterWebUI to 0.0.0.0, and started at http://jupyter-notebook:8080',
#  '20/03/18 20:31:10 INFO handler.ContextHandler: Started o.s.j.s.ServletContextHandler@58cb287e{/metrics/master/json,null,AVAILABLE,@Spark}',
#  '20/03/18 20:31:10 INFO handler.ContextHandler: Started o.s.j.s.ServletContextHandler@3d2d7a89{/metrics/applications/json,null,AVAILABLE,@Spark}',
#  '20/03/18 20:31:10 INFO master.Master: I have been elected leader! New state: ALIVE']
```

4. Count the amount of words.

```python
words = logs.flatMap(lambda x: x.split())
words.count()
# output:
# 264
```

5. Convert all the words to lower case.

```python
lower_case = words.map(lambda x: x.lower())
lower_case.take(2)
# output:
# ['spark', 'command:']
```

6. Remove the words with length lesser than 2.

```python
lesser_than_two = lower_case.filter(lambda x: len(x) >= 2)
lesser_than_two.count()
# output:
# 263
```

7. Attribute the value `1` to each word.

```python
words_with_one = lesser_than_two.map(lambda x: (x, 1))
words_with_one.take(2)
# output:
# [('spark', 1), ('command:', 1)]
```

8. Count the words with the same name.

```python
words_count = words_with_one.reduceByKey(lambda x, y: x + y)
words_count.count()
# output:
# 101
```

9. Visualize in alphabetical order.

```python
words_count_sorted = words_count.sortByKey()
words_count_sorted.take(5)
# output:
# [("'masterui'", 1),
#  ("'sparkmaster'", 1),
#  ('--host', 1),
#  ('--port', 1),
#  ('--webui-port', 1)]
```

10. Visualize the amount of words in descending order.

```python
words_count_sorted_desc = words_count.sortBy(lambda x: x[1], False)
words_count_sorted_desc.take(5)
# output:
# [('20/03/18', 28),
#  ('info', 28),
#  ('20:31:10', 24),
#  ('started', 15),
#  ('handler.contexthandler:', 9)]
```

11. Remove the words with quantity de palavras greater than `1`.

```python
words_sorted_filtered = words_count_sorted_desc.filter(lambda x: x[1] > 1)
words_sorted_filtered.count()
# output:
# 31
```

12. Save the RDD on the HDFS at `/user/rafael/logs_count_word`.

```python
```

