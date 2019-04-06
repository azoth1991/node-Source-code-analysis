# HTTP模块

### lib/http.js

http暴露的接口如下

```
module.exports = {
  _connectionListener,  // _http_server._connectionListener 侦听器
  METHODS: methods.slice().sort(), // _http_common.methods  通用方法
  STATUS_CODES, // _http_server.STATUS_CODES  状态码
  Agent: httpAgent.Agent,  //代理
  ClientRequest, //  _http_client request
  IncomingMessage,  //_http_incoming
  OutgoingMessage, // _http_outgoing
  Server, // _http_server.Server
  ServerResponse,  // _http_server.ServerResponse
  createServer,  // 返回一个new Server()
  get,  // 调用request 执行end并返回
  request // 返回一个ClientRequest的实例
};

```

涉及到的模块如下

```ecmascript 6
const httpAgent = require('_http_agent');
const { ClientRequest } = require('_http_client');
const { methods } = require('_http_common');
const { IncomingMessage } = require('_http_incoming');
const { OutgoingMessage } = require('_http_outgoing');
```

### _http_agent
> 参考文章[《http.agent理解》](https://www.jianshu.com/p/cf8ce464c8a0)[《知乎》](https://www.zhihu.com/question/58996077)
```ecmascript 6
const net = require('net');
const EventEmitter = require('events');
```
- http.agent 提供了管理http的创建,销毁和复用的方法,并提供了以下配置:
- keepAlive：{Boolean} 是否开启 keepAlive，多个请求公用一个 socket connection，默认是 false。
- maxSockets：{Number} 每台主机允许的socket的最大值，默认值为Infinity。maxFreeSockets：{Number} 处于连接池空闲状态的最大连接数， 仅当开启 keepAlive 才有效。

我们首先要知道一个概念，tcp/ip请求都是基于socket实现的，socket提供了http请求创建的API。

