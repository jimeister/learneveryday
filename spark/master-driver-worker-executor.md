# Notes on master/driver and worker/executor

### Master/Worker
- Exist only to allocate executor processes, all work is driver/executor communication
- Master process lives master node of cluster (1 per cluster)
- Worker processes live on worker nodes of cluster (N per cluster)

### Driver/Executor
- Driver process represents invocation of `spark-submit` (1 per invocation)
  - Driver process runs on master node in client mode
  - Possible to run driver process on a node that's different than master process
  - `spark-submit` specifies which master to talk to which in turn determines which workers are used and where executors run
- Executor process does computation and stores data (N per invocation)
  - Always run on worker node, since they're forked by worker process
- Driver process must be IP addressable from executor processes, since executor processes initiate TCP conns back to driver after launch

[cluster overview](http://spark.apache.org/docs/latest/cluster-overview.html)</br>
[spark submit](http://spark.apache.org/docs/latest/submitting-applications.html#launching-applications-with-spark-submit)
