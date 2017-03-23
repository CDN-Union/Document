一、HTTP POST 接口：

/reports        cdn推流打点汇报（批量）

参数 | 是否必须 | 参数类型 | 参数说明 
----|------|----|----
biz | true | string | 服务名，cdn
plat | true | string | 服务商标识,
check | true | string | 校验数据，可为随机数或设备id
sign | true | string | 签名（见sign签名生成规则）
data | true | json 数组 | 批量打点数据（见data字段的单个Json）


{"errno":0,"errmsg":"success","data":${成功个数}}

data字段的单个Json （约定单推流线路每5秒上报一次） 

参数 | 是否必须 | 参数类型 | 参数说明 
----|------|----|----
type | true | string | cdnpush、 等
n | true | string | 推流域名+流名称
vr | true | string | 视频码率，单位 kb/s
fr | true | string | 帧率，单位帧数
tm | true | string | unix时间戳
cnet | true | string | 端网络，2G/3G/4G/wifi
cip | true | string | 端ip
cver | true | string | 端版本

sign签名生成规则

md5(md5(${biz}.${check}.$(plat).length($data)))
最后的lenth($data) 为 批量打点数据条数
