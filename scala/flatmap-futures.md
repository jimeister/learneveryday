# Using `flatMap` with Futures

When using `Future.flatMap`, it will complete with failure if any inner Futures fail, otherwise the operation will complete with success. Example:

```
scala> import scala.concurrent.{Await, Future}
import scala.concurrent.{Await, Future}

scala> import scala.concurrent.ExecutionContext.Implicits.global
import scala.concurrent.ExecutionContext.Implicits.global

scala> import scala.concurrent.duration.Duration
import scala.concurrent.duration.Duration

scala> val f1: Future[String] = Future { "hello" }
f1: scala.concurrent.Future[String] = Success(hello)

scala> val f2: Future[String] = Future { throw new Exception("Ouch") }
f2: scala.concurrent.Future[String] = List()

scala> Await.result(f1.flatMap { x => f2.map { y => println(x); println(y) } }, Duration.Inf)
java.lang.Exception: Ouch
  at $anonfun$1.apply(<console>:14)
  at $anonfun$1.apply(<console>:14)
  at scala.concurrent.impl.Future$PromiseCompletingRunnable.liftedTree1$1(Future.scala:24)
  at scala.concurrent.impl.Future$PromiseCompletingRunnable.run(Future.scala:24)
  at scala.concurrent.impl.ExecutionContextImpl$AdaptedForkJoinTask.exec(ExecutionContextImpl.scala:121)
  at scala.concurrent.forkjoin.ForkJoinTask.doExec(ForkJoinTask.java:260)
  at scala.concurrent.forkjoin.ForkJoinPool$WorkQueue.runTask(ForkJoinPool.java:1339)
  at scala.concurrent.forkjoin.ForkJoinPool.runWorker(ForkJoinPool.java:1979)
  at scala.concurrent.forkjoin.ForkJoinWorkerThread.run(ForkJoinWorkerThread.java:107)

scala> val f3: Future[String] = Future { throw new Exception("Ouch") }
f3: scala.concurrent.Future[String] = List()

scala> val f4: Future[String] = Future { "world" }
f4: scala.concurrent.Future[String] = Success(world)

scala> Await.result(f3.flatMap { x => f4.map { y => println(x); println(y) } }, Duration.Inf)
java.lang.Exception: Ouch
  at $anonfun$1.apply(<console>:14)
  at $anonfun$1.apply(<console>:14)
  at scala.concurrent.impl.Future$PromiseCompletingRunnable.liftedTree1$1(Future.scala:24)
  at scala.concurrent.impl.Future$PromiseCompletingRunnable.run(Future.scala:24)
  at scala.concurrent.impl.ExecutionContextImpl$AdaptedForkJoinTask.exec(ExecutionContextImpl.scala:121)
  at scala.concurrent.forkjoin.ForkJoinTask.doExec(ForkJoinTask.java:260)
  at scala.concurrent.forkjoin.ForkJoinPool$WorkQueue.runTask(ForkJoinPool.java:1339)
  at scala.concurrent.forkjoin.ForkJoinPool.runWorker(ForkJoinPool.java:1979)
  at scala.concurrent.forkjoin.ForkJoinWorkerThread.run(ForkJoinWorkerThread.java:107)

scala> val f5: Future[String] = Future { "hello" }
f5: scala.concurrent.Future[String] = List()

scala> val f6: Future[String] = Future { "world" }
f6: scala.concurrent.Future[String] = List()

scala> Await.result(f5.flatMap { x => f6.map { y => println(x); println(y) } }, Duration.Inf)
hello
world
```

[reference](http://www.scala-lang.org/api/2.11.8/index.html#scala.concurrent.Future@flatMap[S](f:T=>scala.concurrent.Future[S])(implicitexecutor:scala.concurrent.ExecutionContext):scala.concurrent.Future[S])
