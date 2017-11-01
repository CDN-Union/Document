# CDN-Union Mobile Streaming framework 
## 概述
CDN-Union直播推流SDK，覆盖Android和iOS平台，完成了移动平台音视频数据的采集、处理、编码和推流工作。
### 功能列表
基于模块化设计，模块功能分为：
1.  采集
2.  音视频raw数据处理
3.  音视频raw数据混合
4.  编码
5.  基于发送情况的码控
6.  封包（直播FLV封包）
7.  发送（支持RTMP和第三方UDP发送）

### 设计目标
基于积木化设计，提供高定制线的直播SDK方案，可以应对直播业务的任意扩展。
采集、图像处理模块可从外部注册，支持连麦、美颜等组件外部注册。
编码器可以从外部注册，支持x264、ksc265、fdk_aac等任何音视频编码器的实时注册和使用。  
发送模块支持从外部注册，支持librtmp或者任意第三方发送protocol。 

### 整体框架

### 功能实现

### 支持框架列表
- [UnionLiveKit](/) @provide by  
- [PLMediaStreamingKit](/) @provide by

### TaskList
- [ ] 请开发人员将支持的框架transfer回自己厂商/个人github并添加链接.并按照 [iOS音频采集模块](iOS/datacollectionaudio.md)格式填写已支持接口列表及版本号 due: 20171106
- [ ] 请开发人员将命名及包名按照接口定义统一化 due: 20171215
- [ ] 请开发人员 @张道强 @黄尧 等，完善接口用例 due: 20171215

> Note: 后续支持框架需以UnionLiveKit命名
