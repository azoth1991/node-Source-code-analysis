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
> 参考文章[《http.agent理解》](https://www.jianshu.com/p/cf8ce464c8a0)
主要调用
```ecmascript 6
const net = require('net');
const EventEmitter = require('events');
```

