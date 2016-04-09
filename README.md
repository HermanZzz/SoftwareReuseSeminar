## 软件复用——讨论课01 复用解决方案

### 长连接心跳机制

可以使用netty来达到实现Client与Server的长连接通讯和心跳检测的目的。（JDK1.8、netty5）

基本思路：netty服务端通过一个Map保存所有连接上来的客户端SocketChannel,客户端的Id作为Map的key。每次服务器端如果要向某个客户端发送消息，只需根据ClientId取出对应的SocketChannel,往里面写入message即可。心跳检测通过IdleEvent事件，定时向服务端放送Ping消息，检测SocketChannel是否终断。添加了idleStateHandler用于监听链接idle，如果连接到达idle时间，这个handler会触发idleEvent，之后通过重写userEventTriggered方法，完成idle事件的处理。


### 消息不遗漏/不重复


### 消息压缩