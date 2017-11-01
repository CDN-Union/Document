# 视频采集模块
视频采集模块用来输出Texture或RGBA/I420/NV12格式的图像数据，需实现以下接口：
## 通用格式定义
- 图片纹理定义
```
public class ImgTexFrame {
    public static final int NO_TEXTURE = -1;

    public static final int FLAG_KEY_FRAME = 1;     // BUFFER_FLAG_KEY_FRAME
    public static final int FLAG_CODEC_CONFIG = 2;  // BUFFER_FLAG_CODEC_CONFIG
    public static final int FLAG_END_OF_STREAM = 4; // BUFFER_FLAG_END_OF_STREAM

    public ImgTexFormat format;
    public int textureId;
    public final float[] texMatrix;
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
}
```
- 图像纹理格式定义
```
public class ImgTexFormat {
    public static final int COLOR_RGBA = 1;
    public static final int COLOR_YUVA = 2;
    public static final int COLOR_EXTERNAL_OES = 3;

    public final int colorFormat;
    public final int width;
    public final int height;
}
```
- 图像buffer 帧定义
```
public class ImgBufFrame {
    public static final int FLAG_KEY_FRAME = 1;     // BUFFER_FLAG_KEY_FRAME
    public static final int FLAG_CODEC_CONFIG = 2;  // BUFFER_FLAG_CODEC_CONFIG
    public static final int FLAG_END_OF_STREAM = 4; // BUFFER_FLAG_END_OF_STREAM
    /**
     * Image frame format
     */
    public ImgBufFormat format;
    /**
     * A/V Frame buffer, must be direct buffer
     */
    public ByteBuffer buf;
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
}
```
- 图像ImgBufFrame格式定义
```
public class ImgBufFormat {
    public static final int FMT_OPAQUE = 0x00;
    public static final int FMT_NV21 = 0x01;
    public static final int FMT_YV12 = 0x02;
    public static final int FMT_I420 = 0x03;
    public static final int FMT_ARGB = 0x04;
    public static final int FMT_RGBA = 0x05;
    public static final int FMT_BGR8 = 0x06;
    public static final int FMT_AVC  = 0x100;
    public static final int FMT_HEVC = 0x101;
    public static final int FMT_GIF  = 0x102;

    public int format;  // FMT_XXX
    public int orientation;
    public int width;
    public int height;
    public int[] stride;
    public int strideNum;
}
```

### 接口定义
- 输出视频数据
实现输出类型为ImgTexFrame的SrcPin, 以实现Texture图像的输出
```
public SrcPin<ImgTexFrame> getImgTexSrcPin();
```

- 配置视频采集分辨率
```
public void setPreviewSize(int width, int height);
```
- 配置采集帧率
```
public void setPreviewFps(float fps);
```
- 配置采集预览的方向
```
public void setOrientation(int degrees);
```
- 开始采集
```
public void start();
```
- 停止采集
```
public void stop();
```

释放相关资源
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



