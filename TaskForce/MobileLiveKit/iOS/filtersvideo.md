# 图像处理接口

### 简介
基于CPU的图像处理滤镜，可以直接通过CMSampleBuffer传递图像数据，可以不定义接口标准。基于GPU的图像处理滤镜，由于涉及到OpenGL ES的处理，不同实现方式的衔接比较困难，这里采用应用比较广泛的开源项目GPUImage定义的滤镜接口，方便接入。
GPUImage中的滤镜能够实现多级级联，串联成滤镜链。滤镜链中的每个节点都需要接受上级输入（GPUImageInput）和向下级输出(GPUImageOutput)，除了链条起点的节点只需要向下级输出，终点只需要接收上级输入。因此，整个处理接口定义了基类GPUImageOutput，封装实现了OpenGL ES的基础操作，需要连接下级滤镜的节点需要继承该类；由定义了GPUImageInput协议，需要接受上级输入的节点需要实现该协议规定的操作。

## 接口定义
### GPUImageOutput基类 考虑与下级连接的接口
GPUImageOutput的子类主要的作用有两种，一种是将各种来源的数据上传到GPU，并传递到下一级做后续处理；另一种是将本级滤镜的处理结果传递到下一级。
一般读取图片文件的读取类，或者衔接采集模块和处理模块的上传类属于第一种。其他图像处理滤镜属于第二种。
- 增加，移除下级节点
```
(void)addTarget:(id<GPUImageInput>)newTarget;
(void)addTarget:(id<GPUImageInput>)newTarget atTextureLocation:(NSInteger)textureLocation;
(void)removeTarget:(id<GPUImageInput>)targetToRemove;
(void)removeAllTargets;
```
- 查询下级节点
```
(NSArray*)targets;
```
- 设置输出图像的分辨率
```
(void)forceProcessingAtSize:(CGSize)frameSize;
```
- 将处理结果截图输出
```
(UIImage *)imageFromCurrentFramebuffer;
```

### GPUImageInput协议考虑接收上级处理结果的接口
实现GPUImageInput协议的类也有两种， 一种是将GPU处理结果导出，送入压缩模块；另一种是接收上级结果，用自己的shader处理后，再送入下级。图像处理滤镜是第二种，他们继承了GPUImageOutput的同时，也实现了GPUImageInput协议。
```
@interface GPUImageFilter : GPUImageOutput <GPUImageInput>
@end
```
- 接收输入属性，尺寸，旋转，FrameBuffer等：
```
(void)setInputSize:(CGSize)newSize atIndex:(NSInteger)textureIndex;
- (void)setInputRotation:(GPUImageRotationMode)newInputRotation atIndex:(NSInteger)textureIndex;
- (void)setInputFramebuffer:(GPUImageFramebuffer *)newInputFramebuffer
                    atIndex:(NSInteger)textureIndex;
```
- 接收图像渲染完成通知：
```
(void)newFrameReadyAtTime:(CMTime)frameTime atIndex:(NSInteger)textureIndex;
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
