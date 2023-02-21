# Introduction

## Spark shell vs. Spark applications

​	Spark shell/Pyspark Jupyter notebooks are interactive environments in which we can explore and manipulate data.
​	In Spark applications, the programs/scripts run by themselves, without someone watching or analyzing this data in real time. It is possible to create jobs for ETL and/or streaming. To access Spark's resources, it is necessary to create `SparKSession` (`spark`) and `SparkContext` (`sc`) objects, usually automatically instantiated on Spark shell environments

## Running a Spark application

```bash
spark-submit <options>
```

​	To run the applications, we use `spark-submit`. It is a very used and complex command. Here are some of the options available:

- `--help`: displays a guide with all the options.
- `--master`: how the application will be runned. e.g.: local, yarn, spark standalone, etc.
- `--jars`: adds `.jar` files.
- `--py-files`: adds a list of Python files (`.py`, `.zip`, `.egg`).
- `--driver-java-options`: parameters for the JVM driver.
- `--deploy-mode`: `client` (single machine) or `cluster` (parallel).
- `--driver-memory`: memory allocated for the Spark driver (defaults to 1G. Not recommended to be greater than 8G).
- `--executor-memory`: memory allocated for the application.
- `--num-executors`: amount of executors to execute the application.
- `--driver-cores`: amount of cores allocated for the Spark driver.
- `--queue`: run on yarn's queue.

​	Example:

```bash
spark-submit --class NameList MyJarFile.jar people.json namelist/
```
