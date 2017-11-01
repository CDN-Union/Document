# Android接口说明
SDK设计为采用分模块Pipeline化的结构，支持模块间自由连接以及运行时的动态重连接。
## 统一接口说明
该部分主要用来说明SDK内部各个模块之间连接方式以及数据流的传送机制。
在搭建推流Pipeline的时候，各个模块之间的连接使用 SrcPin 和 SinkPin 来完成数据连接。基本准则：  
- 一个Module包含若干个Pin, Module之间的连接由Pin来实现；
- Pin包含SrcPin和SinkPin, 分别产生和消耗数据流；
- SrcPin及SinkPin均是泛型类，创建时需要指定数据格式，相同数据格式的Pin才可以连接，例如：
```
SrcPin<ImgTexFrame> -> SinkPin<ImgTexFrame>
SrcPin<ImgBufFrame> -> SinkPin<ImgBufFrame>
SrcPin<AudioBufFrame> -> SinkPin<AudioBufFrame>
```
- 一个SrcPin可以连接多个SinkPin, 一个SinkPin只能跟一个SrcPin连接；
- 所有连接或断开连接的操作均由SrcPin端操作；

### Pin接口定义
调用SrcPin的connect接口连接两个模块
```
public void connect(SinkPin<T> sinkPin)
   调用SrcPin的disconnect接口断开连接
public void disconnect (boolean recursive)
public void disconnect (SinkPin<T> sinkPin, boolean recursive)
   SrcPin调用disconnect后，SinkPin端可以收到onDisconnect事件
public abstract void onDisconnect (boolean recursive)
   处理onFormatChanged
```

该接口表示数据的初始化完成以及数据格式的改变，源端数据初始化完成及发生改变时均需要触发改事件， Sink端一般需要在该回调中进行一些初始化的工作。

- 包含SrcPin的模块需要在合适的时机触发onFormatChanged;
- 包含SinkPin的模块需要根据需要处理SrcPin触发的onFormatChanged事件；
   处理onFrameAvailable

该接口表示数据输入。
1.  包含SrcPin的模块需要在新的一帧数据ready时触发onFrameAvailable;
2.  包含SinkPin的模块在onFrameAvailable中可以获取新的一帧数据；
