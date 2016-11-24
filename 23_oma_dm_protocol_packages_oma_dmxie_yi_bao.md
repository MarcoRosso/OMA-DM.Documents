# 2.3 OMA DM Protocol packages OMA DM协议包
OMA DM Protocol consists of two parts: setup phase (authentication and device information exchange) and management phase. Management phase can be repeated as many times as the server wishes. Management sessions may start with Package 0 (the trigger). Trigger may be out-of-band depending on the environment and it is specified in DM Notification Initiated Session [DMNOTI].<br/>
OMA DM协议由两部分组成：建立阶段（认证和设备信息交换）和管理阶段。 管理阶段可以重复服务器所希望的次数。 管理会话可以从软件包0（触发器）开始。 根据环境，触发可以是带外的，并且它在DM通知发起的会话[DMNOTI]中指定。

[DMNOTI]:“OMA Device Management Notification Initiated Session, Version 1.2”. Open Mobile Alliance .
OMA-TS-DM_Notification-V1_2. URL:http://www.openmobilealliance.org

The following chart depicts the two phases.<br/>
下图描述了两个阶段。

![](2.3.jpg)
The Management Phase consists of a number of protocol iterations. The content of the package sent from the server to the client determines whether the session must be continued or not. If the server sends management operations in a package that need responses (Status or Results) from the client, the management phase of the protocol continues with a new package from client to server containing the client’s responses to those management operations. The response package from client starts a new protocol iteration. The server can send a new management operation package and therefore initiate a new protocol iteration as many times as it wishes.<br/>
管理阶段包括多个协议迭代。从服务器发送到客户端的包的内容确定会话是否必须继续。如果服务器在需要来自客户端的响应（状态或结果）的包中发送管理操作，则协议的管理阶段将从客户端到服务器的包含客户端对这些管理操作的响应的新包中继续。客户端的响应包开始新的协议迭代。服务器可以发送新的管理操作包，并且因此发起所需次数的新的协议迭代。

During the management phase when a package from server to client does not contain management operations or a challenge, the client will create a package containing only Status for SyncHdr as a response to the package received from server. In this case the entire response package MUST NOT be sent and the protocol ends. A server MUST send response packages to all client packages.<br/>
在管理阶段，当从服务器到客户端的包不包含管理操作或挑战时，客户端将创建只包含SyncHdr状态的包作为对从服务器接收的包的响应。在这种情况下，整个响应包必须不被发送，协议结束。服务器必须向所有客户端软件包发送响应包。

Processing of packages can consume unpredictable amount of time. Therefore the OMA DM Protocol does not specify any timeouts between packages.<br/>
处理包可能消耗不可预测的时间量。因此，OMA DM协议不指定包之间的任何超时。

If not enclosed by a Sequence or Atomic command, the client and server MAY freely choose the execution order of the management commands sent in the package. However, when execution order is required by the parent management command, commands MUST be executed in the order they were sent.<br/>
如果没有被序列或原子命令包围，客户端和服务器可以自由选择在包中发送的管理命令的执行顺序。 但是，当父管理命令需要特定执行顺序时，必须按照它们被发送的顺序执行命令。

Client MUST NOT send any commands other than Replace command containing DevInfo, Results and Alert to the server.<br/>
客户端必须不向服务器发送除包含DevInfo，Results和Alert的Replace命令以外的任何命令。

## 2.3.1 Session Abort 会话中止
### 2.3.1.1 Description 描述
Either the client or the server may decide to abort the session at any time. Reasons for session abort may be server shutdown, client power-down, user interaction on the client, etc. In this case it is best if the aborting party sends a SESSION ABORT Alert. It is RECOMMENDED that the message also includes Status and Results of all the management commands that the aborting party executed before the abort operation.<br/>
客户端或服务器可以决定在任何时候中止会话。会话中止的原因可以是服务器关闭，客户机关机，客户机上的用户交互等。在这种情况下，最好是中止方发送SESSION ABORT警报。推荐该消息还包括中止方在中止操作之前执行的所有管理命令的状态和结果。

If a recipient of a Session Abort sends a response to this message, the response is ignored.<br/>
如果会话中止的接收方向此消息发送响应，则忽略该响应。

Some cases of session aborts are not controllable, for example if the client goes out of coverage or its battery runs down. Servers and clients must be prepared for non-signalled session aborts as well. The requirements stated above are intended to reduce situations in which one party times out on a response from the other.<br/>
一些会话中止的情况是不可控的，例如，如果客户端超出覆盖范围或其电池耗尽。服务器和客户端也必须为非信号会话中止做好准备。上述要求旨在减少一方根据另一方的响应超时的情况。

Implementations are possible (e.g. OBEX) in which the request/response roles of the transport binding may be reversed, i.e. the SyncML Client is a transport-level server, and the SyncML Server is a transport-level client. In this case, the recommendation in Section 8.1.1 above may not apply.<br/>
实现是可能的（例如OBEX），其中传输绑定的请求/响应角色可以颠倒，即SyncML客户端是传输级服务器，并且SyncML服务器是传输级客户端。在这种情况下，上述第2.3.1节中的建议可能不适用。

### 2.3.1.2 Requirement 需求

Alert 1223 is used to signal an unexpected end to the device management session. The sender of the Session Abort alert MAY also include Status and Results of all the management commands that the aborting party executed before the abort operation. The sender MUST include a Final flag. A server receiving this alert SHOULD respond with a message that MUST contain status for the Alert and the SyncHdr and no new commands.<br/>
警报1223用于用信号通知设备管理会话的意外结束。会话中止警报的发送者还可以包括中止方在中止操作之前执行的所有管理命令的状态和结果。 发送方必须包括一个Final标志。 接收此警报的服务器推荐回复一条消息，该消息必须包含警报和SyncHdr的状态，并且不包含新的命令。

A client receiving Alert 1223 SHOULD NOT respond.<br/>
不推荐接收警报1223的客户端响应。

## 2.3.2 Package 0: Management Initiation Alert from server to client 包0：管理启动从服务器到客户端的警报
Many devices cannot continuously listen for connections from a management server. Other devices simply do not wish to “open a port” (i.e. accept connections) for security reasons. However, most devices can receive unsolicited messages, sometimes called “notifications”.<br/>
许多设备不能连续侦听来自管理服务器的连接。出于安全原因，其他设备仅仅不希望“打开端口”（即接受连接）。然而，大多数设备可以接收未经请求的消息，有时称为“通知”。

A management server can use this notification capability to cause the client to initiate a connection back to the management server. OMA DM Protocol specifies several Management Initiation notification bearers. Definition of bearers and notification content can be found from [DMNOTI] specification.<br/>
管理服务器可以使用该通知能力来使得客户端发起到管理服务器的连接。OMA DM协议指定了几个管理发起通知承载。承载和通知内容的定义可以从[DMNOTI]规范中找到。

[DMNOTI]:“OMA Device Management Notification Initiated Session, Version 1.2”. Open Mobile Alliance .
OMA-TS-DM_Notification-V1_2. URL:http://www.openmobilealliance.org

Note that an identical effect to receiving a Management Initiation notification can be caused in other ways. For example, the user interface (UI) of the device may allow the user to tell the client to initiate a management session. Alternatively, the management client might initiate a session as the result of a timer expiring. A fault of some type in the device could also cause the management client to initiate a session.<br/>
注意，可以以其他方式引起与接收管理发起通知相同的效果。例如，设备的用户界面（UI）可以允许用户告诉客户端发起管理会话。或者，管理客户端可以作为定时器到期的结果来发起会话。设备中某种类型的故障也可能导致管理客户端发起会话。

## 2.3.3 Package 1: Initialization from client to server 包1：从客户端到服务器的初始化
The setup phase is virtually identical to that described in the [SYNCPRO]. The purpose of the initialization package sent by the client is:<br/>
设置阶段实际上与[SYNCPRO]中描述的相同。 客户端发送的初始化包的目的是：

* To send the device information (like manufacturer, model etc) to a Device Management Server as specified [DMSTDOBJ]. Client MUST send device information in the first message of management session.<br/>
将设备信息（如制造商，型号等）发送到指定的设备管理服务器[DMSTDOBJ]。 客户端必须在管理会话的第一个消息中发送设备信息。
* To identify the client to the server according to the rules specified in Section 2.4.<br/>
根据第2.4节中指定的规则识别服务器的客户端。
* To inform the server whether the management session was initiated by the server (by sending a trigger in Package 0) or by the client (like end user selecting a menu item).<br/>
通知服务器管理会话是否由服务器启动（通过在包0中发送触发器）或由客户端（如终端用户选择菜单项）。
* To inform the server of any optional Client generated alert, for example Generic Alert or Client Event [REPPRO].<br/>
通知服务器任何可选的客户端生成警报，例如通用警报或客户端事件[REPPRO]。

[SYNCPRO]:“SyncML Data Sync Protocol, version 1.2”. Open Mobile Alliance . OMA-TS-DS_Protocol-V1_2. URL:http://www.openmobilealliance.org

[DMSTDOBJ]:“OMA Device Management Standardized Objects, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_StdObj-V1_2. URL:http://www.openmobilealliance.org

[REPPRO]:“SyncML Representation Protocol, version 1.2”. Open Mobile Alliance . OMA-TS-SyncML_RepPro-V1_2. URL:http://www.openmobilealliance.org
