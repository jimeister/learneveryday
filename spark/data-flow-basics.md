# Data Flow Basics

- Executor-driver communication scales with number of partitions
- Number of tasks scales with number of partitions (one task per partition)
- Executor-executor communication is done when doing a [`shuffle`](https://spark.apache.org/docs/latest/programming-guide.html#shuffle-operations)
- Avoiding shuffles should improve performance in general, [example](http://www.cloudera.com/documentation/enterprise/latest/topics/admin_spark_tuning1.html)
- Greatly increasing number of partitions can lead to `spark.akka.frameSize` [errors](https://forums.databricks.com/questions/1622/how-do-i-change-the-sparkakkaframesize.html)
- `repartition` is just `coalesce(shuffle=true)`
- OutOfMemory
  - when executor process OOM, they will send exceptions back to driver and driver will report
  - when OS kills JVM forcefully, no message is sent back to driver and driver may spin up another executor
- pyspark
  - because of GIL, spark will create one python process per core for maximum parallelism
  - data is passed from JVM process to python process via pickling/unpickling
