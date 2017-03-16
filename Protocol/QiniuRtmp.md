# 增加 Metadata 字段
增加 cdn_ip 字段，为边缘节点 IP
增加 x-reqid 字段，为流对应的请求 ID，便于调试

# 延迟测量方法
在推流 SDK 中每隔 15s 发送 `"currentTime", 1489631528` 的 CommandMessage。参数为当前时间戳，客户端收到后可以测量延迟。
