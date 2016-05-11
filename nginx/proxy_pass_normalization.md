# nginx `proxy_pass` URI normalization

When using `proxy_pass` functionality in nginx, specifying a URI or not affects whether the request URI is normalized or not. For example, given the following `nginx.conf`:
```
daemon off;
worker_processes auto; # Detect from cores
user nobody nobody;
error_log stderr notice;

events {
  worker_connections 1024; # Default: 512
}

http {
  # 'combined' format, except:
  #   - $time_local -> $time_iso8601
  #   - Add Host header, e.g. www.premise.com vs. warg.premise.com
  #   - Add $upstream_addr
  log_format combined_plus
    '$remote_addr - $remote_user [$time_iso8601] "$request" $status $body_bytes_sent '
    '"$http_referer" "$http_user_agent" "$host" "$upstream_addr"';

  access_log /dev/stdout combined_plus;

  upstream proxy {
    server    localhost:9200 fail_timeout=0;
  }

  server {
    server_name ""; # Accept any Host header
    listen    8000;

    location /proxy/ {
      proxy_pass http://proxy/;
    }
  }
}
```

Running `http get http://localhost:8000/proxy/user%2Fedit` shows that `%2F` is normalized to `/`:
```
$ nc -vv -l -p 9200
Listening on any address 9200 (wap-wsp)
Connection from 127.0.0.1:53439
GET /user/edit HTTP/1.0
Host: proxy
Connection: close
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: HTTPie/0.9.3

Total received bytes: 130
Total sent bytes: 0
```

If the `location` block is replaced with the following:
```
location /proxy/ {
  proxy_pass http://proxy;
}
```

Rerunning the command above shows that original URI with `%2F` is preserved:
```
$ nc -vv -l -p 9200
Listening on any address 9200 (wap-wsp)
Connection from 127.0.0.1:53469
GET /proxy/user%2Fedit HTTP/1.0
Host: proxy
Connection: close
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: HTTPie/0.9.3

Total received bytes: 138
Total sent bytes: 0
```

This behavior may have implications depending on how the upstream proxy handles the normalized path. Elasticsearch in particular appears to distinguish `/` and `%2F` in request URIs.

Useful docs:
- http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass
- https://forum.nginx.org/read.php?2,256639,256647
- http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#rewrite
- http://serverfault.com/questions/459369/disabling-url-decoding-in-nginx-proxy
