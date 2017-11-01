# 音频混合层接口
多路音频混合模块能够接收各种不同格式的PCM数据输入，统一转为的输出格式后送入缓存，每路音频的输入缓存各自独立。需要在输入的各路音频中指定一个主路，以该路音频数据的时间戳作为参考，其他路的时间戳则忽略。最后按照主路音频的节奏将当前可用的所有音频数据叠加混合为一路，通过输出回调函数送出。
### 接口定义
- 查询和设置每一路音频的使能状态
```
(BOOL) setTrack:(int) trackId
           enable:(BOOL)onOff;
(BOOL) getTrackEnable:(int) trackId;
```
- 查询和设置每一路音频的音量比例
```
(float) getMixVolume:(int) trackId;
(BOOL) setMixVolume:(float) vol
                  of:(int) trackId;
```
- 选择主路, 通常选择实时采集的麦克风对应的通路为主路。
```
@property(nonatomic, assign) int mainTrack;
 设置输出音频的格式，包括采样率，输出频率，通道数等
@property (nonatomic, assign) int sampleRate;
@property (nonatomic, assign) int frameSize;
@property(nonatomic, assign) BOOL bStereo;
```
- 送入音频PCM数据的接口
```
(BOOL)processAudioData:(uint8_t**)pData
                nbSample:(int)len
              withFormat:(const AudioStreamBasicDescription*)fmt
                timeinfo:(CMTime)pts
                      of:(int) trackId;
```
- 送出混音后的音频数据的回调接口
```
@property(nonatomic, copy) void(^audioProcessingCallback)(CMSampleBufferRef sampleBuffer);
@property(nonatomic, copy) void(^pcmProcessingCallback)(uint8_t** pData, int nbSample, CMTime pts);
```
- 与采集模块的数据输出接口考虑一致。
```
@property(nonatomic, copy) void(^audioProcessingCallback)(CMSampleBufferRef sampleBuffer);
@property(nonatomic, copy) void(^pcmProcessingCallback)(uint8_t** pData, int len, const AudioStreamBasicDescription* fmt, CMTime timeInfo);
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
