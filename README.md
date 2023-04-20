# 介绍

基于 `grpc-gateway` 的，统一处理由 `grpc` 返回给 `http` 的数据。包括以下几点：

- `http` 统一返回的 `json` 格式： 由 `code/msg/data` 组成
- 按照谷歌标准将 `grpc` 错误码转成 `http` 的错误码
- 请求成功后，处理后返回给前端只有一个 `response`

# 使用

引入包

```shell
go get "github.com/janrs-io/Jgrpc-response"
```

在 `grpc-gateway` 启动 `http` 服务的中间件添加以下方法：

```shell
mux := runtime.NewServeMux(
	runtime.WithErrorHandler(Jgrpc_response.HttpErrorHandler),
	runtime.WithForwardResponseOption(Jgrpc_response.HttpSuccessResponseModifier),
	runtime.WithMarshalerOption("*", &Jgrpc_response.CustomMarshaller{}),
)
```

`proto` 设置统一返回的数据格式为以下格式：

```protobuf
// http 返回数据
message Response {
  int64 code = 1;
  string msg = 2;
  google.protobuf.Any data = 3;
}
```

**当 `rpc` 按照以上格式返回后，添加了 `http` 处理中间件会自动处理 `rpc` 返回的数据然后返回给前端。**
