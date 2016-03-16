# Key for dictionary from variable

When creating a dictionary object, using a variable for key name will substitute in the name of the variable itself rather than the value for that variable. The fix is to initialize an empty dictionary using `{}` and use bracket notation to assign the key/value pair.

Bad (from Chromse JS console):
```
> var k = 'my_key';
undefined
> var v = 'my_value';
undefined
> {k: v}
Object {k: "my_value"}
```

Good (from Chrome JS console):
```
> var k = 'my_key';
undefined
> var v = 'my_value';
undefined
> var d = {};
undefined
> d[k] = v;
"my_value"
> d
Object {my_key: "my_value"}
```
