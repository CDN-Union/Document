# 音频采集模块

### 简介
- 采集参数配置，比如:采样率；
- 启动，停止，暂停和恢复音频采集；
- 采集声音数据回调输出接口；  

## 接口定义
音频采集采样率配置，需要在创建音频采集模块时指定
```
- (id) initWithSampleRate:(double)sampleRate;
```

启动，停止，暂停和恢复音频采集
```
- (BOOL)startCapture;
- (void)stopCapture;
- (BOOL)pauseCapture;
- (BOOL)pauseWithMuteData;
- (BOOL)resumeCapture;
```

采集声音数据回调输出接口
```
@property(nonatomic, copy) void(^audioProcessingCallback)(CMSampleBufferRef sampleBuffer);
@property(nonatomic, copy) void(^pcmProcessingCallback)(uint8_t** pData, int len, const AudioStreamBasicDescription* fmt, CMTime timeInfo);
```

以上回调二选一， 采用CMSampleBufferRef时和iOS系统的原生API交互比较方便。
选择指针类型的数据，与其他开源模块的交互比较方便。其中AudioStreamBasicDescription定义了音频数据的格式，具体定义参见
https://developer.apple.com/documentation/coreaudio/audiostreambasicdescription。
pData 为两级指针是为了应对多路非交织数据输入的情况，比如双声道，非交织的数据，左右声道可能分别存放在两块不同的内存区域中， 为了避免拷贝， 此时可以的PData可以指向存放了左右声道数据指针的数组。
```
uint8_t* pLeftChannelData = {…};
uint8_t* pRightChannelData = {…};
uint8_t* pData[] = { pLeftChannelData ,pRightChannelData };
```

### 支持性
|method/functions|UnionStreamingKit|PLMediaStreamingKit|
|---|---|---|
|initWithSampleRate|1.0|?|
|startCapture|1.0|?|
|stopCapture|1.0|?|
|pauseCapture|1.0|?|
|pauseWithMuteData|1.0|?|
|resumeCapture|1.0|?|
|audioProcessingCallback|1.0|?|
|pcmProcessingCallback|1.0|?|

### 可用组件列表
// @TODO
|name|link|provider|
|---|---|---|


### 相关资料
// @TODO
- [UnionStreamingKit](/)
- [PLMediaStreamingKit](/)

### 贡献者
**Teams**
- [金山云](http://www.ksyun.com/)
- [七牛云](https://www.qiniu.com/)
- [熊猫直播](https://www.panda.tv/)

**Individuals**



