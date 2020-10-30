## Axios

[axios 0.21.0]: https://github.com/axios/axios.git



### 目录结构


├─dist       // 输出
├─examples  
│  ├─all
│  ├─amd
│  ├─get
│  ├─post
│  ├─transform-response
│  └─upload
├─lib    // 核心代码
│  ├─adapters    // 适配器
│  ├─cancel        // 用于取消请求
│  ├─core    // axios原型
│  └─helpers
├─sandbox
└─test
    ├─manual
    ├─specs
    │  ├─cancel
    │  ├─core
    │  ├─helpers
    │  └─utils
    ├─typescript
    └─unit
        └─adapters



### axios实例

* [ ] axios
  * [ ] axios.Cancel 
  * [ ] axios.CancelToken
  * [x] axios.all 直接调用了Promise.all
  * [ ] axios.isCancel
  * [ ] axios.spread



**实例**

```js
// 返回的实例
function createInstance(defaultConfig) {
  var context = new Axios(defaultConfig);
    
  // instance是request
  var instance = bind(Axios.prototype.request, context);

  // Copy axios.prototype to instance
  utils.extend(instance, Axios.prototype, context);

  // Copy context to instance
  utils.extend(instance, context);

  return instance;
}
```



**Axios原型**

```js
// Axios对象 /lib/core/Axios.js
function Axios(instanceConfig) {
  this.defaults = instanceConfig;
  this.interceptors = {
    // InterceptorManager拦截器对象
    request: new InterceptorManager(),
    response: new InterceptorManager()
  };
}

// 原型链上还有 request
Axios.prototype.request = function request(config) {
  // 合并了config

  // Hook up interceptors middleware
  var chain = [dispatchRequest, undefined];
  var promise = Promise.resolve(config);

  // 将request拦截器成组加入到头部
  this.interceptors.request.forEach(function unshiftRequestInterceptors(interceptor) {
    chain.unshift(interceptor.fulfilled, interceptor.rejected);
  });
  // 将response拦截器成组加入到尾部
  this.interceptors.response.forEach(function pushResponseInterceptors(interceptor) {
    chain.push(interceptor.fulfilled, interceptor.rejected);
  });

  // 将所有拦截器组成promise链
  while (chain.length) {
    promise = promise.then(chain.shift(), chain.shift());
  }

  return promise;
};

//
Axios.prototype.getUri

// get，post 等请求直接调用request方法
```



### default config

几个重要的节点

- [ ] adapter
- [x] transformRequest
- [x] transformResponse
- [ ] validateStatus
- [ ] headers

**adapter**： 根据环境使用了不同的对象，XHR和http（/lib/adapetrs）。

**transformRequest**：转换参数和设置了默认的header Accept和Content-Type。

**transformResponse**: 仅对string尝试格式化为json，转化失败或其他返回原始数据。





### 拦截器

```js
lib\core\InterceptorManager.js

function InterceptorManager() {
  this.handlers = [];
}

// 添加新的拦截器
InterceptorManager.prototype.use

// 移除拦截器
InterceptorManager.prototype.eject

// 递归调用handlers
InterceptorManager.prototype.forEach

```





### 取消





### helper

##### buildUrl

```js
// lib\helpers\buildURL.js
function buildURL(url, params, paramsSerializer) {
  // 没有传递params，直接返回url
  
  //
  if (paramsSerializer) {
    serializedParams = paramsSerializer(params);
  } else if (utils.isURLSearchParams(params)) {
    serializedParams = params.toString();
  } else {
    // 默认array转为key[]=value;
    // 默认Date转为toISOString
    // 默认对象转为Json
      
    // 特殊字符转义
  }

  // 删除了hash 保留了url原有参数
  // 如果没设置params或为空独享则会保留下hash
  if (serializedParams) {
    var hashmarkIndex = url.indexOf('#');
    if (hashmarkIndex !== -1) {
      url = url.slice(0, hashmarkIndex);
    }

    url += (url.indexOf('?') === -1 ? '?' : '&') + serializedParams;
  }
}
```

