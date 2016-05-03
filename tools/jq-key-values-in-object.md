# Using jq to get key/values for entries in objects

Given an object like the following:
```
{
  "abcde": {
    "id": "abcde",
    "count": 0,
    "enabled": true
  },
  "vwxyz": {
    "id": "vwxyz",
    "count": 4,
    "enabled": false
  }
}
```

`jq` can be used to get keys and values by doing the following:
```
$ echo '{
  "abcde": {
    "id": "abcde",
    "count": 0,
    "enabled": true
  },
  "vwxyz": {
    "id": "vwxyz",
    "count": 4,
    "enabled": false
  }
}' | jq '. | keys[] as $k | "\($k), \(.[$k] | .enabled)"'
"abcde, true"
"vwxyz, false"
```

[reference](http://stackoverflow.com/questions/34226370/jq-print-key-and-value-for-each-entry-in-an-object)
