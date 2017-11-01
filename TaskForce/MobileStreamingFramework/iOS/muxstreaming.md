# 封包与推流接口
Librtmp实现了发送接口，则使用librtmp推流。其他上行协议实现发送接口，则可以无缝接入推流。
## 接口定义
- 推流参数配置
```
@property (nonatomic, assign) BOOL bWithVideo;
@property (nonatomic, assign) BOOL bWithAudio;
@property (nonatomic, readwrite) UnionAudioFmt *aFmt;
@property (nonatomic, readwrite) UnionVideoFmt *vFmt;
@property (nonatomic, readonly) NSURL* url
```
配置音频、视频格式，是否推送音频，是否推送视频。
- 启动推流
```
(void) startStream: (NSURL*) url;
```
- 发送数据
```
(void) sendPacket:(uint8_t *)packet size:(int)size timeInfo:(CMTime)timeInfo type:(UnionPacketType)type
```
- 停止推流
```
(void) stopStream 
```

### 接入用例

### 支持性

### 可用组件列表
- [联盟推流组件]https://github.com/CDN-Union/StreamingFramework

### 相关资料
// @TODO: 完善可用链接
- [UnionStreamingKit](/)
- [PLMediaStreamingKit](/)

### 贡献者
**Teams**
- [星域CDN](https://www.xycdn.com/)
- [金山云](http://www.ksyun.com/)
- [七牛云](https://www.qiniu.com/)
- [熊猫直播](https://www.panda.tv/)

**Individuals**
