# Tunning

​	Deploy with dynamic allocation.

​	Parameters to use the cluster's resources:

- `--master $YARN`: `$YARN` variable will define the execution mode.
    - `$YARN == local`: local execution.
    - `$YARN == yarn`: cluster execution.
- `--deploy-mode cluster`: specify cluster mode.
- `--conf "spark.dynamic.Allocation.enable=true"`: enable dynamic allocation.
- `--conf "spark.shuffle.service.enable=true"`
- `--conf "spark.shuffle.service.port=7337"`
- `--conf "spark.dynamic.InitialExecutors=6"`:
- `--conf "spark.dynamic.maxExecutors=9"`:
- `--conf "spark.dynamic.minExecutors=3"`:

## Calculation of the resources

​	To calculate the cluster's resources allocation, we must consider the entire capacity of the infra/queue.

- `--driver-memory 8g`: `"8g"` is the recommended value.
- `--executor-memory`:
    - `int((total_memory * 0.9) / num_executors)`.
- `--conf`
- `--conf`
- `--executors-core`
- `--num-executors`
