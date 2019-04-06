# _http_client

client提供了客户端创建请求的方法,创建过程大概可以分为一下几步

### 1、获取请求option
```ecmascript 6
  if (typeof input === 'string') {
    const urlStr = input;
    try {
      input = urlToOptions(new URL(urlStr));
    } catch (err) {
      input = url.parse(urlStr);
      if (!input.hostname) {
        throw err;
      }
      if (!urlWarningEmitted && !process.noDeprecation) {
        urlWarningEmitted = true;
        process.emitWarning(
          `The provided URL ${urlStr} is not a valid URL, and is supported ` +
          'in the http module solely for compatibility.',
          'DeprecationWarning', 'DEP0109');
      }
    }
  } else if (input && input[searchParamsSymbol] &&
             input[searchParamsSymbol][searchParamsSymbol]) {
    // url.URL instance
    input = urlToOptions(input);
  } else {
    cb = options;
    options = input;
    input = null;
  }

  if (typeof options === 'function') {
    cb = options;
    options = input || {};
  } else {
    options = Object.assign(input || {}, options);
  }
```

### 2、使用agent创建请求

``const defaultAgent = options._defaultAgent || Agent.globalAgent;``

### 3、定义请求path、port、host

### 4、请求method

### 5、定义请求回调，侦听response事件
```ecmascript 6
  if (cb) {
    this.once('response', cb);
  }
```

### 6、设置请求头