# 图像混合层接口

### 简介
图像混合模块在GPU上实现，支持将多个输入Texture在指定位置混合后输出一个Texture, 属于GPU图像处理模块的一种，除实现GPU处理模块的指定接口外，还需实现以下接口：

## 接口定义
- 设置混合后输出的Texture的分辨率.
```
public void setTargetSize(int outWidth, int outHeight);
```
- 混合图层配置
指定输入源在混合时的位置及透明度信息, 其中位置参数为以输出分辨率为参考的归一化值。
```
public void setRenderRect(int idx, RectF rect, float alpha);
```
- 缩放模式配置
指定输入源设置混合时的缩放模式，缩放模式支持 SCALING_MODE_FULL_FILL,SCALING_MODE_BEST_FIT, SCALING_MODE_CENTER_CROP等。
```
public void setScalingMode(int idx, int mode);
```
- 设置镜像
```
public void setMirror(int idx, boolean mirror);
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



