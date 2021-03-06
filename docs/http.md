# \- http

## 范式
```
- http: { url: [, media:][, post:][, headers:][, async:][, path:] }
```
您可以通过**http**标签进行网络请求

## 属性
| 属性 | 类型 | 是否必须 | 备注 |
|--------|--------|--------|--------|
|   url   | [expr](datatype.md)  | √ |  发起网络请求的目标地址，可以是http或https开头 |
|   media   | [expr](datatype.md)  | x  |  post数据的媒体类型，默认为`text/plain`,可参考[MIME类型](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/MIME_types) |
|   post   | [expr](datatype.md)  | x |  |
|   headers   | [expr](datatype.md)  |  x |  头信息 可参考[HTTP Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) |
|   async   | [boolean](datatype.md)  |  x | Default = $false  |
|   path   | [path](datatype.md)  |  x | 返回结果存储路径  |

## 用法
### get请求
```yaml
- http: {url: '"http://127.0.0.1/echo"', path: "/resp"}
```

### post请求
```yaml
- http: {url: '"http://127.0.0.1/echo"', post: '"ping"' path: "/resp"}
```

### 定义media的post请求
```yaml
- put: { path: '/req/param1', value: '1' }
- put: { path: '/req/param2', value: '2' }
- jsonstr: { path: '/postBody', value: '$/req' }
- http: {url: '"http://127.0.0.1/echo"', media: 'application/json'  post: '$/postBody' path: "/resp"}
```

### 定义headers的get请求
```yaml
- put: { path: '/headers/Content_Type', value: '"text/plain"' }
- put: { path: '/headers/Custom_Param', value: '"custom param"' }
- http: {url: '"http://127.0.0.1/echo"', headers: '$/headers' , path: "/resp"}
```

### 异步请求
```yaml
- http: {url: '"http://127.0.0.1/echo"', async: '$true'}
```
