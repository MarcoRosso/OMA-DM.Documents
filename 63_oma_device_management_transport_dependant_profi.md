# 6.3 OMA Device Management Transport Dependant Profiles OMA设备管理传输依赖配置文件
The following sections illustrate the transport dependant profiles for sending a trigger from OMA Device Management Server to a OMA Device Management Client.<br/>
以下部分说明了用于将触发器从OMA设备管理服务器发送到OMA设备管理客户端的传输依赖配置文件。

## 6.3.1 Package #0 delivered using WAP Push 使用WAP Push传送包＃0
The WAP Push framework provides a means for a Push Initiator (PI) to send information to a mobile terminal via a Push Proxy Gateway (PPG) in an asynchronous manner (see [PROVARCH] for an overview). It is assumed that the OMA DM server will act as a PI, but it is also possible for the server to communicate directly with the mobile terminal if it is able to operate as a PPG.<br/>
WAP推送框架提供了用于推送发起者（PI）以异步方式经由推送代理网关（PPG）向移动终端发送信息的手段（参见[PROVARCH]概述）。假定OMA DM服务器将充当PI，如果其能够进行PPG操作，则服务器也可以与移动终端直接通信。

When the WAP Push framework is used to deliver Package #0, the non-secure connectionless WSP [WSP] session service is utilized as defined in [PUSHOTA]. The following rules MUST be adhered to as well as the order of the WSP headers:<br/>
当WAP Push框架用于传递包＃0时，应如[PUSHOTA]中定义的那样使用非安全的无连接WSP[WSP]会话服务。必须遵守以下规则以及WSP头的顺序：

* The Content-Type header [PUSHMSG] MUST include the MIME media type for Packet #0 as defined in [IANA]. The Content-Type code 0x44 MUST be used instead of the textual representation of the MIME code.<br/>
内容类型报头[PUSHMSG]必须包含[IANA]中定义的数据包＃0的MIME媒体类型。必须使用内容类型代码0x44而不是MIME代码的文本表示。

* The X-WAP-Application-ID header [PUSHMSG] MUST include the application-id associated with the SyncML Device Management User Agent. The application-id code 0x07 MUST be used instead of the textual representation of the Application-id.<br/>
X-WAP应用程序ID头[PUSHMSG]必须包括与SyncML设备管理用户代理相关联的应用程序标识符。必须使用应用程序标识代码0x07，而不是应用程序标识的文本表示。

* Other headers may be included if it is known that the OMA DM Client can interpret them in a useful manner. However, it must be ensured that the total length of the WDP and WSP headers never exceeds 48 bytes to ensure that there is sufficient space for the payload.<br/>
如果已知OMA DM客户端可以以有效的方式解释它们，则其他报头可以被包括在内。但是，必须确保WDP和WSP头的总长度不会超过48字节，以确保有效负载有足够的空间。

* The push message is sent to the default non-secure connectionless push port (2948).<br/>
推送消息被发送到默认的非安全无连接推送端口（2948）。

The message payload has been designed to fit into a single short message when SMS is used to deliver WAP Push. If the
WAP Push message does not fit into a single SMS message the concatenated messages MUST be used.<br/>
当SMS用于传送WAP推送时，消息有效载荷被设计成适合单个短消息。如果
WAP推送消息不适合单个SMS消息，必须使用连接的消息。

### 6.3.1.1 Using non WAP Push capable devices 使用非WAP推送功能的设备
If the receiver is not a WAP device, it is very unlikely that any other application would be active on the same port, which has been publicly registered with IANA. The decoding of the message headers is very straightforward even if the device lacks a full WAP stack and therefore the device MUST examine if the message has been sent to the WAP push port (2948) and if the Application-ID and the MIME type are one assigned to the OMA DM Notification Initiation Package. If this information is correct then the message MUST be routed to the OMA Device Management application.<br/>
如果接收方不是WAP设备，则任何其他应用程序在已向IANA公开注册的同一端口上处于活动状态的可能性不大。消息报头的解码是非常简单的，即使设备缺少完整的WAP栈，因此设备必须检查消息是否已经发送到WAP推送端口（2948），以及应用程序ID和MIME类型是否是一个分配给OMA DM的通知发起包。如果此信息正确，则必须将消息路由到OMA设备管理应用程序。
## 6.3.2 Package #0 over OBEX 包＃0通过OBEX
Local Notification Initiated Session over OBEX is done inside the PUT command of the OBEX protocol. This happens in the same way as sending the DM messages over OBEX to a SyncML client (See the SyncML OBEX Binding specification [SYNCOBEX].<br/>
通过OBEX的本地通知发起的会话在OBEX协议的PUT命令内完成。这与通过OBEX向SyncML客户端发送DM消息相同（参见SyncML OBEX绑定规范[SYNCOBEX]）。

