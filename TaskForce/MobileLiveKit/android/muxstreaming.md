# 封包与推流接口
封包发送模块支持将编码后的音视频数据封包后推送到远端服务器或保存到本地，可以根据需求实现不同的协议。该模块包含一个音频输入的SinkPin, 一个视频输入的SinkPin, 需实现以下接口：
实现视频编码后数据的输入接口
```
public SinkPin<ImgBufFrame> getVideoSink();
```
- 实现音频编码后数据的输入接口

```
public SinkPin<AudioBufFrame> getAudioSink();
```
设置输入的视频数据的码率，单位为bps
```
public void setVideoBitrate(int videoBitrate);
```
设置输入的音频数据的码率, 单位为bps
```
public void setAudioBitrate(int audioBitrate);
```
设置输入的视频数据的帧率
```
public void setFramerate(float framerate);
```
设置/获取是否为纯音频模式
```
public void setAudioOnly(boolean audioOnly);
public boolean isAudioOnly();
```
设置/获取是否为纯视频模式
```
public void setVideoOnly(boolean videoOnly);
public boolean isVideoOnly();
```
设置/获取封包发送的目标地址
```
public void setUrl(String url);
public String getUrl();
```
添加自定义封包的meta信息
```
public void addMetaOption(String key, String value);
```
开始/停止/释放资源接口
```
public boolean start();
public void stop();
public void release();
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
