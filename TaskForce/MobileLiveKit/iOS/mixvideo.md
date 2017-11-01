# 图像混合层接口

### 简介
图像混合通常需要对图像进行缩放处理，图层之间可能还需要按照透明进行颜色混合，为了处理的效率我们通常在GPU上进行该操作，所以图像混合模块是一个GPU Image的滤镜，一个可以接受任意数量输入的滤镜。图像混合模块需要制定主图层，最终输出画面的帧率和主图层的相同。

## 接口定义
图层混合模块在GPU ImageFilter的基础上增加的接口如下：
- 设置主要图层
```
@property (nonatomic, assign) NSUInteger masterLayer;
```
- 设置各个图层的位置和大小
```
(void)setPicRect: (CGRect) rect
          ofLayer: (NSInteger) idx;
(CGRect) getPicRectOfLayer:(NSInteger) idx;
```
- 设置各个图层的透明度, 透明度(0~1.0), 0为全透明
```
(void)setPicAlpha: (CGFloat) alpha
           ofLayer: (NSInteger) idx;
(CGFloat) getPicAlphaOfLayer:(NSInteger) idx;
```
- 清除指定图层的画面内容
```
(void)clearPicOfLayer:(NSInteger) index;
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



