## 1 背景
根据直播开源协议初稿，直播分为视频流和业务流。

此文档在于对业务流协议进行定义。

业务流为非数据流，用于支撑直播业务的业务数据，例如弹幕，多视角，vr业务数据等等。

业务流协议建议采用独立于音视频数据的通道传输。

## 2 协议
### 2.1 基准
此协议基于RTMP标准协议，并对其进行扩展以支持直播业务流。
### 2.2 createStream命令消息
业务客户端发送createStream消息给服务器，用于创建业务消息通信通道。
此命令格式与rtmp createStream命令相同。
### 2.3 NetStream命令消息
Netstream增加serve消息，用于客户端向服务端请求/创建业务流，类似play/publish。
客户端serve消息格式如下：

|Filed Name    |Type  |Description|
|--------------|------|-----------|
|CommandName   |String|serve|
|Transaction ID|Number|Transaction ID set to 0|
|Command Object|null  |null type|
|Service Name  |String|Name of the service|

服务端收到serve消息后，如果service name 不存在，则创建新的service。
如果存在的话，则将客户端加入到服务端的service中。
服务端响应格式如下：

|Filed Name |Type  |Description|
|-----------|------|-----------|
|CommandName|String|Onstatus|
|Description|String|NetStream.Serve.Create: if service created successful<br>NetStream.Serve.Attache: the service exists and attache successful<br>NetStream.Serve.Error: error happens|

### 2.4 Service Message业务消息
为方便调试，Service Message采用rtmp的call command 传输， 定义如下：

|Filed Name     |Type  |Description|
|-------------- |------|-----------|
|Produre Name   |String|业务标识符，标识是一个业务消息<br>暂定cdnunion20170314<br>|
|Transaction ID |Number|0|
|Service Header |Object|业务消息头部|
|Service Content|Object|业务消息内容，如果为空则为null type|

不同的业务消息，服务端会做不同的响应，或者不做响应，具体由业务消息定义。
服务端响应消息采用相同的消息格式。

#### 2.4.1 Service Header Object格式

|Property     |Type   |Description|
|-------------|-------|-----------|
|version      |Number |协议版本，当前版本为0|
|transimitType|Number |转发类型<br>0 for 广播，1 for CDN边缘节点， 2 for 源站，由客户端设置，用于控制服务端如何转发/处理消息<br>10 for 服务端响应，表明是服务端给客户端的响应消息，由服务端设置|
|serviceType  |Number |业务消息类型， 0 for 弹幕，1 for 能力协商|
|priority     |Number |消息的优先级，0 最高，7最低|
|abandon      |Boolean|0 for 不可丢弃消息，1 for 可丢弃消息|
|messageID    |String |消息的唯一标识，由客户端设置。服务端响应消息应设置为客户端消息的原始messageID|
|networkID    |String |消息产生的网络ID, networkID需向联盟注册|

#### 2.4.2 Service Content Object 格式

Service Content由不同的业务类型决定，客户可自定义。

## 3 交互
业务客户端与服务端交互过程如下：
* 客户端与服务端进行rtmp标准握手
* 客户端发送connect命令，服务端通过_result返回结果
* 客户端发送createStream命令，服务端返回_result结果
* 客户端发送serve命令，服务端通过onStatus返回结果
* 客户端和服务端开始互相发送业务消息

## 4 具体业务消息
### 4.1 业务能力查询消息
业务能力查询消息主要用于不同网络间的能力协商。
#### 4.1.1 客户端查询消息
查询消息的transmitType为1，serviceType为1。
消息内容为null type。
#### 4.1.2 服务端响应消息
服务端响应消息的transimitType为3，serviceType为1。
响应消息的service content object如下：

|Property   |Type  |Description         |
|-----------|------|--------------------|
|networkName|String|网络名称             |
|live       |String|直播能力,rtmp/udp/no |
|rtc        |String|RTC能力,rtmp/udp/no |
|service    |Number|支持的业务流协议版本   |
|danmu      |String|弹幕能力，danmu/no   |

### 4.2 弹幕
#### 4.2.1 弹幕业务消息格式
弹幕的transmitType是0，serviceType是0。
弹幕消息不需要服务端进行响应。
其Service Content Object包含以下字段：

|Property  |Type  |Description|
|----------|------|-----------|
|userID    |String|用户名|
|userLevel |String|用户等级|
|deviceType|Number|0 for PC, 1 for mobile|
|roomID    |String|房间名|
|timeStamp |Date  |弹幕时间戳，单位ms|
|danmuType |Number|弹幕类型，0 for 自定义消息，非0 for 礼物类型|
|content   |String|自定义消息内容或礼物数量|

## 5 Data Message
基于标准协议 1.0 7.1.2节，Data message用于传输metadata及其他用户信息。messageType 18 用于标识AMF0，messageType 15 用于标识AMF3

### 5.1 metadata 字段
用于标识 metadata，及其他可一次性描述的用户信息。必填字段：

|Property  |Type  |Description|
|----------|------|-----------|
|cdn_ip    |String|CDN节点IP|
|framerate |Number|视频比特率|

### 5.2 latency
间隔15s发送， 用于检测观看端与推流端的延迟时间。参考[QiniuRTMP Latency](QiniuRtmp.md#latency-benchmark)。
