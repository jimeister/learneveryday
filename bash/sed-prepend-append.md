# Using `sed` to prepend and append to lines

To prepend to each line:
```
$ printf '1\n2\n3\n' | sed "s/^/'/"
'1
'2
'3
```

To append to each line:
```
$ printf '1\n2\n3\n' | sed "s/$/'/"
1'
2'
3'
```

Both at once:
```
$ printf '1\n2\n3\n' | sed "s/.*/'&'/"
'1'
'2'
'3'
```

[regex reference](https://en.wikipedia.org/wiki/Regular_expression#POSIX_basic_and_extended)
