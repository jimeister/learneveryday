# Using thunks to pass block of code to another function

The following syntax allows a block of code (zero-argument function) to be passed to a function.
```
def func[X](op: => X) = {
  op
}
```

This is equivalent to:
```
def func2[X](op: () => X) = {
  op()
}
```

Example:
```
scala> def func[X](op: => X) = {
     |   op
     | }
func: [X](op: => X)X

scala> func { println("hello") }
hello

scala> def func2[X](op: () => X) = {
     |   op()
     | }
func2: [X](op: () => X)X

scala> func2 { () => println("world") }
world
```

[reference](http://stackoverflow.com/questions/22670356/scala-passing-function-as-block-of-code-between-curly-braces)
