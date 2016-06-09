# Using `paste` to concat file lines

```
$ printf "a\nb\nc\n"
a
b
c

$ printf "a\nb\nc\n" | paste -sd ','
a,b,c
```
