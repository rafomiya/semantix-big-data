# Exercises - Setup Environment

1. Configure Spark's `.jar` to accept the parquet format in Hive tables.

```bash
curl -O https://repo1.maven.org/maven2/com/twitter/parquet-hadoop-bundle/1.6.0/parquet-hadoop-bundle-1.6.0.jar
docker cp parquet-hadoop-bundle-1.6.0.jar jupyter-spark:/opt/spark/jars
```

2. Download the data directory `spark/input` (volume on the namenode).

```bash
cd input
sudo git clone https://github.com/rodrigo-reboucas/exercises-data.git .
```

3. Verify if the data is on the namenode.

```bash
docker exec -it namenode bash
ls input
# output:
# README.md       beneficio  economicFitness  entrada1.txt  escola    iris         map.py  namesbystate  populacaoLA
# WordCount.java  db-sql     empreendimento   entrada2.txt  hnpStats  juros_selic  names   ouvidoria     reduce.py
```

4. Create the structure `/user/rafael/data` on the HDFS.

```bash
# inside the namenode
hdfs dfs -mkdir -p /user/rafael/data
```

5. Put all the data from the directory `input` into the HDFS on `/user/rafael/data`.

```bash
# inside the namenode
hdfs dfs -put input/* /user/rafael/data
```

