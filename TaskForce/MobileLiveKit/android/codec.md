# 编码器接口
音视频编码模块共用接口，根据输入、输出数据类型的差异，部分接口的参数不同。
1.  音频编码模块实现将输入的PCM数据编码后输出。
2.  视频编码模块包含两类:
    - 输入图像为Texture;
  - 输入图像为I420格式的ByteBuffer数据.

### 数据结构定义
- 音频编码参数
```
public class AudioEncodeFormat {
    private int codecId;
    private int profile;
    private int sampleFmt;
    private int sampleRate;
    private int channels;
    private int bitrate;
}
```
- 视频编码参数
```
public class VideoEncodeFormat {
    private int pixFmt;
    private int codecId;
    private int width;
    private int height;
    private int bitrate;
    private float framerate;
    private float iframeinterval;
    // 场景编码参数.
    private int scene;
    // 性能编码参数
    private int profile;
    private int crf;
    private boolean liveStreaming;
}
```

### 接口定义
音视频编码模块需要实现的接口如下：
- 接收数据
实现接收音视频数据的SinkPin, 此处为泛型, 根据输入格式的不同, 指定不同的类型。
音频编码器实现对AudioBufFrame格式数据的处理；
视频编码器实现对ImgTexFrame或ImgBufFrame格式数据的处理。
```
public SinkPin<I> getSinkPin();
```
- 输出数据
实现输出编码后数据的SrcPin, 此处为泛型, 根据输出格式的不同，指定不同的类型。
音频编码器的输出为AudioBufFrame。
视频编码器的输出为ImgBufFrame。
```
public SrcPin<O> getSrcPin();
```
- 配置编码参数
音频编码器接收的参数格式为AudioEncodeFormat。  
视频编码器接收的参数格式为VideoEncodeFormat。  
```
public void configure(Object encodeFormat);
```
- 获取当次编码过程中丢掉的frame数量
```
public int getFrameDropped();
```
- 获取当次编码过程中已编码的frame数量
```
public int getFrameEncoded();
```
- 编码过程中动态设置输出码率
```
public void adjustBitrate(int bitrate);
```
- flush当前编码器
```
public void flush();
```
- 开始编码
```
public void start();
```
- 停止编码
```
public void stop();
```
- 释放相关资源
```
public void release();
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