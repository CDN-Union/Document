# 编码器接口
多路音频混合模块能够接收各种不同格式的PCM数据输入，统一转为的输出格式后送入缓存，每路音频的输入缓存各自独立。需要在输入的各路音频中指定一个主路，以该路音频数据的时间戳作为参考，其他路的时间戳则忽略。最后按照主路音频的节奏将当前可用的所有音频数据叠加混合为一路，通过输出回调函数送出。
### 共用数据类型定义
- 包类型定义：
```
typedef NS_ENUM(NSUInteger, UnionPacketType) {
    UnionPacketType_Unknown = 0, // 未知的数据包类型
    UnionPacketType_Video, // 视频数据包
    UnionPacketType_Audio, // 音频数据包
};
```
- 音频格式定义
```
typedef struct _UnionAudioFmt{
    int codecId; // 编码类型
    int sampleFmt; // 采样格式
    int sampleRate; // 采样率
int channels; // 声道数
int bitrate; // 编码码率, 单位是kbps
}UnionAudioFmt;
```

- 视频格式定义
```
typedef struct _UnionVideoFmt{
    int codecId; // 编码类型
    int width; // 视频宽度
    int height; // 视频高度
}UnionVideoFmt;
```

### 编码器接口定义
- 外部注册编码器
```
(int)registeEncoder(void *codec)
```
- 启动编码器
```
(int)startEncoder()
```
- 停止编码器
```
(int)stopEncoder()
```
- 对原始图像数据进行编码
```
(void)processVideoSampleBuffer:(CMSampleBufferRef)sampleBuffer onComplete:(void (^)(BOOL))completion;
(void)processVideoPixelBuffer:(CVPixelBufferRef)pixelBuffer timeInfo:(CMTime)timeInfo onComplete:(void (^)(BOOL))completion;
```
- 对音频数据进行编码
```
(void)processAudioSampleBuffer:(CMSampleBufferRef)sampleBuffer
onComplete:(void (^)(BOOL))completion;
(void)processAudioDataBuffer:(uint8_t *data  size:(int)size absd:(const AudioStreamBasicDescription *)asbd timeInfo:(CMTime)timeInfo
onComplete:(void (^)(BOOL))completion;
```
- 编码数据包输出
```
@property(nonatomic, copy) void(^encodedPacketCallback)(uint8_t *packet, int size, CMTime timeInfo, UnionPacketType type);
```

### 接入用例

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