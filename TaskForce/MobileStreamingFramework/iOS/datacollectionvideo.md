# 视频采集模块

### 简介
采集参数配置接口
- 采集分辨率，iOS的API主要通过一组预定义的preset来设置采集的分辨率；
- 采集帧率；
- 输出的像素格式；

摄像头控制接口
- 启动，停止摄像头采集；
- 暂停，恢复摄像头采集；
- 前后摄像头切换, 以及相应的当前摄像头状态查询的属性；
- 闪光灯相关的查询和控制接口；

数据回调接口
- 视频数据的回调接口，启动采集后，按照设定的采集帧率，以CMSampleBufferRef的形式回调输出的图像数据， 该结构体包含了图像的时间戳，图像宽高信息，像素格式，数据地址等信息。

## 接口定义
- 采集分辨率，字符串定义参见
https://developer.apple.com/documentation/avfoundation/avcapturesessionpreset
```
@property (readwrite, nonatomic, copy) NSString *captureSessionPreset;
```
- 采集帧率
```
@property (readwrite) int32_t frameRate;
```
- 输出像素格式，枚举定义参见 
https://developer.apple.com/documentation/corevideo/1563591-pixel_format_types
```
@property (readwrite) OSType outputPixelFmt;
```
- 启动、停止，暂停恢复采集
```
(void)startCameraCapture;
(void)stopCameraCapture;
(void)pauseCameraCapture;
(void)resumeCameraCapture;
```
- 前后摄像头切换
```
(void)rotateCamera;
(AVCaptureDevicePosition)cameraPosition;
```
- 闪光灯
```
(BOOL) isTorchSupported;
(void) toggleTorch;
```
- 数据回调输出
```
@property(nonatomic, copy) void(^videoProcessingCallback)(CMSampleBufferRef sampleBuffer);
```
CMSampleBufferRef 定义和相关操作参见
https://developer.apple.com/documentation/coremedia/cmsamplebuffer?language=objc
该结构体中需要包含视频帧的像素数据， 像素格式，时间戳等信息。


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



