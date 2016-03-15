# Returning `Try[X]` from a function

To return a scala [Try](http://www.scala-lang.org/api/2.9.3/scala/util/Try.html) from a function, simply return either `Success` and `Failure` depending on the conditions you want to check in your function.

Example:
```
scala> import scala.util.{Failure, Success, Try}
import scala.util.{Failure, Success, Try}

scala> def isGood(input: Int): Try[Int] = {
     |   if (input % 2 == 0) {
     |     Success(input)
     |   } else {
     |     Failure(new Exception("your input isn't good"))
     |   }
     | }
isGood: (input: Int)scala.util.Try[Int]

scala> val g = isGood(4)
g: scala.util.Try[Int] = Success(4)

scala> g.get
res0: Int = 4

scala> val b = isGood(5)
b: scala.util.Try[Int] = Failure(java.lang.Exception: your input isn't good)

scala> b.get
java.lang.Exception: your input isn't good
  at .isGood(<console>:16)
  ... 32 elided
```

[reference](http://www.scala-lang.org/api/2.9.3/scala/util/Try.html)
