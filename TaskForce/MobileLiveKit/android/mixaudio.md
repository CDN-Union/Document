# 音频混合层接口
音频混合模块实现将多路PCM数据混合为一路后输出，包含多个AudioBufFrame格式的SinkPin和 一个AudioBufFrame格式的SrcPin. 需实现以下接口：

- 定义当前模块支持的输入引脚数目
```
public int getSinkPinNum();
```
- Frame处理
根据索引获取当前模块AudioBufFrame格式的SinkPin, 当前模块需实现对这些输入frame的处理。
```
public SinkPin<AudioBufFrame> getSinkPin(int index);
```
- 输出PCM数据
实现输出类型为AudioBufFrame的SrcPin, 以输出混音后的PCM音频数据.
```
public SrcPin<AudioBufFrame> getSrcPin();
```
- 设置主驱动SinkPin的索引
混音操作以该输入源数据进行驱动，继承该输入源的时间戳信息。
```
public final void setMainSinkPinIndex(int index);
```
- 设置音量
配置每个输入源在混音时的音量, vol取值一般为[0.0f-1.0f]。
```
public void setInputVolume(int idx, float vol);
```
获取每个输入源混音时配置的音量信息
```
public float getInputVolume(int idx);
```
设置/获取混音后是否输出静音数据
```
public void setMute(boolean mute);
public boolean getMute();
```
释放相关资源
```
public void release();
```

### 支持性

### 可用组件列表
// @TODO：完善可用组件链接  
|name|link|provider|
|---|---|---|
|？|？|？|


### 相关资料
// @TODO: 完善可用链接
- [UnionStreamingKit](/)
- [PLMediaStreamingKit](/)

### 贡献者
**Teams**
- [金山云](http://www.ksyun.com/)
- [七牛云](https://www.qiniu.com/)
- [熊猫直播](https://www.panda.tv/)

**Individuals**
