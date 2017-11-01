# 音频采集模块

### 简介
- 采集参数配置，比如:采样率；
- 启动，停止，暂停和恢复音频采集；
- 采集声音数据回调输出接口；  
   音频buffer帧定义
### 通用格式定义
```
public class AudioBufFrame {
    public static final int FLAG_KEY_FRAME = 1;     // BUFFER_FLAG_KEY_FRAME
    public static final int FLAG_CODEC_CONFIG = 2;  // BUFFER_FLAG_CODEC_CONFIG
    public static final int FLAG_END_OF_STREAM = 4; // BUFFER_FLAG_END_OF_STREAM

    /**
     * Audio frame format
     */
    public AudioBufFormat format;
    /**
     * Frame decode timestamp
     */
    public long dts;
    /**
     * Frame presentation timestamp
     */
    public long pts;
    /**
     * Frame flags, FLAG_XXX
     */
    public int flags;
    /**
     * A/V Frame buffer, must be direct buffer
     */
    public ByteBuffer buf;
}
```

音频buf格式
```
public class AudioBufFormat {
    public int sampleFormat;
    public int sampleRate;
    public int channels;
    public int codecId;
}
```

## 接口定义
音频采集模块用来输出pcm音频数据，需要包含一个输出类型为AudioBufFrame的SrcPin, 实现以下接口。
- 输出音频，实现输出类型为AudioBufFrame的SrcPin, 以连接后续模块
```
public SrcPin<AudioBufFrame> getSrcPin();
```

- 设置音频采样率，单位为Hz
```
public void setSampleRate(int sampleRate);
```
- 设置音频采集的声道数
```
/**
* @param channels 声道数，1表示单声道，2表示双声道
*/
public void setChannels(int channels);
```
- 开启音频采集
```
public void start();
```
- 停止音频采集
```
public void stop();
```
- 释放社保资源
```
public void release();
```

### 接入用例

### 支持性
|method/functions|[UnionLiveKit](/)|[PLMediaStreamingKit](/)|


### 可用组件列表
// @TODO：完善可用组件链接  
|name|link|provider|
|---|---|---|
|？|？|？|


### 相关资料
// @TODO: 完善可用链接
- [UnionLiveKit](/) @Provide by
- [PLMediaStreamingKit](/) @Provide by

### 贡献者
**Teams**
- [金山云](http://www.ksyun.com/)
- [七牛云](https://www.qiniu.com/)
- [熊猫直播](https://www.panda.tv/)

**Individuals**



