# 2.1 Multiple Messages In Package 包中的多个信息
## 2.1.1  Description 描述
The OMA Device Management protocol provides the functionality to transfer one SyncML package using multiple SyncML messages. This is necessary when one SyncML package is too large to be transferred in one SyncML message. For example, this limitation may be caused by the transport protocol or by the limitations of a small footprint device.<br/>
OMA设备管理协议提供使用多个SyncML消息传输一个SyncML包的功能。当一个SyncML包太大而无法在一个SyncML消息中传输时，这是必需的。例如，这种限制可能由传输协议或小型脚印装置的限制引起。

In OMA Device Management, the role of the package as a logical grouping of items is very limited. Most restrictions occur on messages, not on packages. For example, a command must fit entirely into one message. This includes the Sequence and Atomic commands, each of which must fit entirely into one message.<br/>
在OMA设备管理中，包作为项目的逻辑分组的作用非常有限。大多数限制发生在消息上，而不是在包上。例如，命令必须完全适合于一个消息。这包括序列和原子命令，每个命令必须完全适合一个消息。

In order to avoid overwhelming a client with limited resources, a server is not permitted to send new commands to a client that has not yet returned a status to previous commands. In other words, most messages sent by the server to the client will correspond to a (one message) package, except in the case where a server is sending a large object or asking for more messages (using Alert 1222). A package containing a large object datum will span as many messages as necessary to transmit the large object, as specified in Section 2.2.<br/>
为了避免使用有限资源的客户端宕机，服务器不允许向尚未向先前命令返回状态的客户端发送新命令。换句话说，除了在服务器发送大对象或请求更多消息（使用警报1222）的情况下，服务器发送到客户端的大多数消息将对应于（一个消息）一个包。包含大对象数据的包将传输大对象所需的许多消息，如第2.2节中所述。

