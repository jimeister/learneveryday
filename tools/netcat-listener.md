# Using netcat as listener

Use netcat in very verbose mode to see request details.

Start request:
```
$ http get http://localhost:9200/api/get-item
```

See request details:
```
$ nc -vv -l -p 9200
Listening on any address 9200 (wap-wsp)
Connection from 127.0.0.1:61504
GET /api/get-item HTTP/1.1
Host: localhost:9200
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: HTTPie/0.9.3

Total received bytes: 147
Total sent bytes: 0
```
