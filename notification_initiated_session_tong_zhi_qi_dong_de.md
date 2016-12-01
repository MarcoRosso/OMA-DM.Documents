# Notification Initiated Session 通知启动的会话

Many devices cannot continuously listen for connections from a management server. Other devices simply do not wish to “open a port” (i.e. accept connections) for security reasons. However, most devices can receive unsolicited messages, sometimes called “notifications”. Some handsets, for example, can receive SMS messages. Other devices may have the ability to receive other, similar datagram messages.<br/>
许多设备不能连续侦听来自管理服务器的连接。出于安全原因，其他设备不希望“打开端口”（即接受连接）。然而，大多数设备可以接收未经请求的消息，有时称为“通知”。例如，一些手机可以接收SMS消息。其他设备可以具有接收其他类似数据报消息的能力。

A management server can use this notification capability to cause the client to initiate a connection back to the management server. This connection might be over HTTP, WAP or another transport protocol.<br/>
管理服务器可以使用此通知功能来使客户端发起到管理服务器的连接。此连接可能通过HTTP，WAP或其他传输协议。

The contents of such a “Notification Initiation Alert” might be empty, but the message itself may be signed such that the client can authenticate it. The result of receiving such an alert would be for the client to initiate a connection to the management server that sent the alert. In this scenario, the client might verify that this management server is among those authorized to request such activity. Alternatively, the contents of the alert might indicate that another management server should be contacted.<br/>
这种“通知发起警报”的内容可以是空的，但是消息本身可以被签名，使得客户端可以对其进行验证。接收这样的警报的结果将是客户端发起到发送警报的管理服务器的连接。在这种情况下，客户端可能会验证此管理服务器是否被授权请求此类活动。或者，警报的内容可以指示应联系另一管理服务器。

An identical effect of receiving a Notification Initiation Alert can also be caused in other ways. For example, the user interface (UI) of the device may allow the user to tell the client to initiate a management session. Or, the management client might initiate a session as the result of a timer expiring. Of course, a fault of some type in the device could also cause the management client to initiate a session.<br/>
也可以以其他方式引起接收通知发起警报的相同效果。例如，设备的用户界面（UI）可以允许用户告诉客户端发起管理会话。或者，作为定时器到期的结果，管理客户端可以发起会话。当然，设备中某种类型的故障也可能导致管理客户端发起会话。

## Definitions 定义
Message Sequence Chart Notation used in the message sequence charts (MSC):<br/>
消息序列图（MSC）中使用的符号：

Box: Indicates the start of a procedure or an internal process in a device.<br/>
盒子：表示设备中的过程或内部过程的开始。

Hexagon: Indicates a condition that is needed to start the transaction below this hexagon.<br/>
六角形：指示在此六角形下方启动事务所需的条件。

Arrow: Represents a message, or transaction.<br/>
箭头：表示消息或事务。

## Abbreviations 缩写
MSC Message Sequence Chart 消息序列图
OMA Open Mobile Alliance 开放移动联盟


