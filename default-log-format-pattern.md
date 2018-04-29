# nginx default log format pattern

1. If your log format is default

```
log_format combined '$remote_addr - $remote_user [$time_local] '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent"';
```

## nginx access log pattern

```
NGINX_ACCESSLOG_COMBINED %{IPORHOST:clientip} - %{USER:ident} \[%{HTTPDATE:timestamp}\] \"%{DATA:request}\" %{INT:status} %{NUMBER:bytes_sent} \"%{DATA:http_referer}\" \"%{DATA:http_user_agent}\"
```

## nginx error log pattern

```
NGINX_ERRORLOG_ERROR (?<timestamp>%{YEAR}[./]%{MONTHNUM}[./]%{MONTHDAY} %{TIME}) \[%{LOGLEVEL:level}\] %{POSINT:pid}#%{NUMBER:threadid}\: \*%{NUMBER:connectionid} %{GREEDYDATA:message}, client: %{IP:clientip}, server: %{GREEDYDATA:server}, request: "(?<request>%{WORD:method} %{UNIXPATH:path} HTTP/(?<httpversion>[0-9.]*))"(, )?(upstream: "(?<upstream>[^,]*)")?(, )?(host: "(?<host>[^,]*)")?
```