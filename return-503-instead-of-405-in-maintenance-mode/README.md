# メンテナンスモードでPOSTリクエストに対し405ではなく503を返す設定

## ビルドと起動

```shell
$ docker build -t nginx-mizzy .
$ docker run -ti -p 8080:80 nginx-mizzy
```

## 動作確認

### メンテナンスモードOff

```shell
$ curl -s --verbose -X POST localhost:8080
*   Trying 127.0.0.1:8080...
* Connected to localhost (127.0.0.1) port 8080 (#0)
> POST / HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.79.1
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 405 Not Allowed
< Server: nginx/1.23.1
< Date: Mon, 15 Aug 2022 03:43:47 GMT
< Content-Type: text/html
< Content-Length: 157
< Connection: keep-alive
<
<html>
<head><title>405 Not Allowed</title></head>
<body>
<center><h1>405 Not Allowed</h1></center>
<hr><center>nginx/1.23.1</center>
</body>
</html>
* Connection #0 to host localhost left intact
```

### メンテナンスモードOn

```shell
$ curl -s --verbose -X POST localhost:8080
*   Trying 127.0.0.1:8080...
* Connected to localhost (127.0.0.1) port 8080 (#0)
> POST / HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.79.1
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 503 Service Temporarily Unavailable
< Server: nginx/1.23.1
< Date: Mon, 15 Aug 2022 03:43:01 GMT
< Content-Type: text/html
< Content-Length: 17
< Connection: keep-alive
< ETag: "62f9a5e9-11"
<
Maintenance mode
* Connection #0 to host localhost left intact
```
