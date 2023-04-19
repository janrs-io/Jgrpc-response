# 介绍

基于 `grpc-gateway` 的，统一处理由 `grpc` 返回给 `http` 的数据。包括以下几点：

- `http` 统一返回的 `json` 格式： 由 `code/msg/data` 组成
- 按照谷歌标准将 `grpc` 错误码转成 `http` 的错误码
- 请求成功时候，处理后只有一个 `response`

# 使用