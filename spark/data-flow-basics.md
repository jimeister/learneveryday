# Data Flow Basics

- Executor-driver communication scales with number of partitions
- Executor-executor communication is done when doing a (`shuffle`)[https://spark.apache.org/docs/latest/programming-guide.html#shuffle-operations]
- Avoiding shuffles should improve performance in general
- Greatly increasing number of partitions can lead to `spark.akka.frameSize` (errors)[https://forums.databricks.com/questions/1622/how-do-i-change-the-sparkakkaframesize.html]
- `repartition` is just `coalesce(shuffle=true)`
