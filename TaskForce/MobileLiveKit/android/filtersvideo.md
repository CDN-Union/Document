# 图像处理接口

### 简介
图像处理模块包含两种实现，一种是GPU上对Texture图像的处理，一种是CPU上对图像buffer的处理。

## 接口定义
### GPU图像处理接口
GPU上的图像处理模块支持多Texture输入，处理之后输出一个处理后的Texture, 需实现以下接口：
- 当前模块支持的输入引脚数目.
```
public int getSinkPinNum();
```
- 获取输入引脚
根据索引获取当前模块ImgTexFrame格式的SinkPin, 当前模块需实现对这些输入frame的处理.
```
public SinkPin<ImgTexFrame> getSinkPin(int idx);
```
- 获取输出引脚
实现输出类型为ImgTexFrame的SrcPin, 以输出处理后的Texture图像。
```
public SrcPin<ImgTexFrame> getSrcPin();
```
- 设置主驱动SinkPin的索引
图像处理与输出应以该index的SinkPin所接收的数据进行驱动。
```
public final void setMainSinkPinIndex(int index);
```

5.3.2.  CPU图像处理接口
对图像buffer数据的处理模块，与Texture的处理模块类似，仅将输入、输出的frame格式更改为ImgBufFrame。
- 当前模块支持的输入引脚数目.
```
public int getSinkPinNum();
```
- 获取输入引脚
根据索引获取当前模块ImgBufFrame格式的SinkPin, 当前模块需实现对这些输入frame的处理.
```
public SinkPin<ImgBufFrame> getSinkPin(int idx);
```
- 获取输出引脚
实现输出类型为ImgBufFrame的SrcPin, 以输出处理后的图像。
```
public SrcPin<ImgBufFramee> getSrcPin();
```
- 设置主驱动SinkPin的索引
图像处理与输出应以该index的SinkPin所接收的数据进行驱动。
```
public final void setMainSinkPinIndex(int index);
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
