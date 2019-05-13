# Logstash grok pattern for nginx

Defined logstash grok pattern for nginx log

## How To

- Deploy pattern file to `/etc/logstash/patterns/nginx`

## Pattern

-  nginx default log format pattern

If your log format is default

```
log_format combined '$remote_addr - $remote_user [$time_local] '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent"';
```

- nginx access log pattern

```
NGINX_ACCESSLOG_COMBINED %{IPORHOST:clientip} - %{USERNAME:remote_user} \[%{HTTPDATE:date_timestamp}\] \"(?:%{WORD:method} %{NOTSPACE:request_uri}(?: HTTP/%{NUMBER:httpversion})?|%{DATA:raw_request})\" %{INT:status} %{NUMBER:body_bytes_sent} \"%{DATA:http_referer}\" \"%{DATA:http_user_agent}\"
```

- nginx access log with IO and X-Forwarded-For (first IP)

```
NGINX_ACCESSLOG_IO_COMBINED_XFORWARDEDFOR (?:%{IPV4:clientip}|-)(?:,\s[\d.]+)* (?:%{DATA:remote_user}|-) (?:%{DATA:ident}|-) \[%{HTTPDATE:date_timestamp}\] \"(?:%{WORD:method} %{NOTSPACE:request_uri}(?: HTTP/%{NUMBER:httpversion})?|%{DATA:raw_request})\" %{NUMBER:status} (?:%{NUMBER:body_bytes_sent}|-) \"%{DATA:http_referer}\" \"%{DATA:http_user_agent}\" (?:%{NUMBER:request_length}|-) (?:%{NUMBER:bytes_sent}|-) (?:%{NUMBER:request_time}|-)
```

- nginx error log pattern

```
NGINX_ERRORLOG_ERROR (?<timestamp>%{YEAR}[./]%{MONTHNUM}[./]%{MONTHDAY} %{TIME}) \[%{LOGLEVEL:level}\] %{POSINT:pid}#%{NUMBER:threadid}\: \*%{NUMBER:connectionid} %{GREEDYDATA:message}, client: %{IP:clientip}, server: %{GREEDYDATA:server}, request: "(?<request>%{WORD:method} %{UNIXPATH:path} HTTP/(?<httpversion>[0-9.]*))"(, )?(upstream: "(?<upstream>[^,]*)")?(, )?(host: "(?<host>[^,]*)")?
```
