# Use `tr` to concatenate file lines

To concatenates the lines of a file together with some delimeter - say `,` - use `tr`.

Example:
```
$ cat test
a
b
c

$ cat test | tr '\n' ','
a,b,c,
```

Note trailing comma

[reference](http://stackoverflow.com/questions/15580144/concatenate-many-lines-of-output-to-one-line)
