# Local CORS Proxy

解决本地环境跨域的问题

```
No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://localhost:3000' is therefore not allowed access. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disable
```

## 使用简介

```
npm install -g local-cors-proxy
```

[跨域的例子](https://node-cors-client.netlify.app/)：

GET https://node-cors-server.herokuapp.com/no-cors

正常情况下是访问错误的

```
Access to fetch at 'https://node-cors-server.herokuapp.com/no-cors' from origin 'http://localhost:7003' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.
```

设置 proxy, 转发端口设置为 7004

```
lcp --proxyUrl https://node-cors-server.herokuapp.com --port 7004
```

GET http://localhost:7004/proxy/no-cors

经过 proxy 代理，访问正常

```
{"text":"You should not see this via a CORS request."}
```

可以在 package.json 中设置，快速配置代理

```package.json
 "scripts": {
   "proxy": "lcp --proxyUrl https://node-cors-server.herokuapp.com --port 7004"
 }
```

## 支持的参数

| Option         | Example               | Default |
| -------------- | --------------------- | ------: |
| --proxyUrl     | https://node-cors-server.herokuapp.com |         |
| --proxyPartial | proxy                 |   proxy |
| --port         | 7004                  |    8010 |
| --credentials  | (no value needed)     |   false |
| --origin       | http://localhost:7004 |       * |
