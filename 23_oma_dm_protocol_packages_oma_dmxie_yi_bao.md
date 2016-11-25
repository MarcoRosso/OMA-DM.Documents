# 2.3 OMA DM Protocol packages OMA DM协议包
OMA DM Protocol consists of two parts: setup phase (authentication and device information exchange) and management phase. Management phase can be repeated as many times as the server wishes. Management sessions may start with Package 0 (the trigger). Trigger may be out-of-band depending on the environment and it is specified in DM Notification Initiated Session [DMNOTI].<br/>
OMA DM协议由两部分组成：建立阶段（认证和设备信息交换）和管理阶段。 管理阶段可以重复服务器所希望的次数。 管理会话可以从软件包0（触发器）开始。 根据环境，触发可以是带外的，并且它在DM通知发起的会话[DMNOTI]中指定。

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


The detailed requirements for the initialization package from the client to server (Package 1) are:<br/>
从客户端到服务器（包1）的初始化包的详细要求是：

1. The requirements for the elements within the SyncHdr element.
SyncHdr元素中元素的要求。
  * The value of the VerDTD element MUST be '1.2'.<br/>
  VerDTD元素的值必须为“1.2”。
  * The value of the VerProto element MUST be ‘DM/1.2’.<br/>
  VerProto元素的值必须为“DM/1.2”。
  * SessionID MUST be included to indicate the ID of the management session. If the client is responding to notification, with alert code SERVER-INITIATED MGMT (1200), then SessionID MUST be same as in notification. Otherwise, the client generates a SessionID which should be unique for that client. The same SessionID MUST be used throughout the whole session.<br/>
  必须包括SessionID以指示管理会话的ID。如果客户端正在响应通知，具有警报代码SERVER-INITIATED MGMT（1200），则会话ID必须与通知中相同。否则，客户端必须生成对于该客户端是唯一的SessionID。在整个会话中必须使用相同的SessionID。
 * MsgID MUST be used to unambiguously identify the message belonging to the management session from server to client.<br/>
MsgID必须用于明确标识从服务器到客户端的属于管理会话的消息。
 * The Target element MUST be used to identify the target server.<br/>
 Target元素必须用于标识目标服务器。
 * The Source element MUST be used to identify the source device.<br/>
 Source元素必须用于标识源设备。
 * The Cred element MAY be included in the authentication message from the Device Management client to Device Management server as specified in Section 9.<br/>
 Cred元素可以包含在从设备管理客户端到设备管理服务器的认证消息中，如第2.4节中所述。
 
2. Alert MUST be sent whether the client or the server initiated the management session in the SyncBody. The requirement for the Alert command follows:<br/>
无论客户端还是服务器发起SyncBody中的管理会话，都必须发送警报。 对警报命令的要求如下：
  * CmdID is REQUIRED. CmdID是必需的。
  * The Data element is used to carry the management session type which can be either SERVER-INITIATED MGMT (1200) or CLIENT-INITIATED MGMT (1201).<br/>
Data元素用于承载管理会话的可以是SERVER-INITIATED MGMT（1200）或CLIENT-INITIATED MGMT（1201）。

3. The device information MUST be sent using the Replace command in the SyncBody. The requirement for the Replace command follows:<br/>
必须使用SyncBody中的Replace命令发送设备信息。替换命令要求如下：
  * CmdID is REQUIRED. CmdID是必需的。
  * An Item element per node found from device information tree. Possible nodes in device information tree are specified in [DMSTDOBJ].<br/>
  从设备信息树中找到的每个节点的项目元素。设备信息树中的可能节点在[DMSTDOBJ]中指定。
  * The Source element in the Item element MUST have a value indicating URI of node.<br/>
  Item元素中的Source元素必须具有指示节点的URI的值。
  * The Data element is used to carry the device information data.<br/>
  Data元素用于携带设备信息数据。
  
4. Client MAY include client-generated alerts such as Client Event [REPPRO] or Generic Alert.<br/>
客户端可能包括客户端生成的警报，例如客户端事件[REPPRO]或通用警报。

The Final element MUST be used in the SyncBody for the message, which is the last in this package.<br/>
Final元素必须在消息的SyncBody中使用，该消息是此包中的最后一个。

## 2.3.4 Package 2: Initialization from server to client 包2：从服务器到客户端的初始化
The purpose of the initialization package sent by the server is to:<br/>
服务器发送的初始化包的目的是：

* Identify the server to the client according to the rules specified in Section 2.4.<br/>
根据第2.4节中指定的规则识别到客户端的服务器。
* Optionally, the server can send user interaction commands.<br/>
（可选）服务器可以发送用户交互命令。
* Optionally to send management data and commands.<br/>
可选择发送管理数据和命令。
* Send status of Client Initiated Alerts if any of these was received from the client<br/>
如果从客户端接收到任何警报消息，则发送客户端启动警报的状态

Package 2 MAY close the management session by containing only the `<Final>` element (any management command, user interaction command or client authentication challenge will continue the session). Alternately, the server may send the Session Abort Alert (1223) to force the close of the session in extreme situations.<br/>
包2可以通过仅包含`<Final>`元素（任何管理命令，用户交互命令或客户端认证挑战将继续会话）来关闭管理会话。 或者，服务器可以发送会话中止警报（1223）以在极端情况下强制关闭会话。

The detailed requirements for package 2 are:<br/>
包2的详细要求是：

1. The requirements for the elements within the SyncHdr element.<br/>
   SyncHdr元素中元素的要求。
   * The value of the VerDTD element MUST be '1.2'.<br/>
   VerDTD元素的值必须为“1.2”。
   * The value of the VerProto element MUST be ‘DM/1.2’ when complying with this specification.<br/>
   符合本规范时，VerProto元素的值必须为“DM/1.2”。
   * SessionID MUST be included to indicate the ID of the management session.<br/>
   必须包括SessionID以指示管理会话的ID。
   * MsgID MUST be used to unambiguously identify the message belonging to the management session from server to client.<br/>
   MsgID必须用于明确标识从服务器到客户端的属于管理会话的消息。
   * The Target element MUST be used to identify the target device.<br/>
   Target元素必须用于标识目标设备。
   * The Source element MUST be used to identify the source device.<br/>
   Source元素必须用于标识源设备。
   * Cred element MAY be included in the authentication message according to the rules described in Section 9. Server is always authenticated to the device but this authentication MAY be accomplished at the transport level.<br/>
   Cred元素可以根据第2.4节中描述的规则包括在认证消息中。服务器始终对设备进行认证，但此认证可以在传输层完成。
2. The Status MUST be returned in the SyncBody for the SyncHdr and Alerts sent by the client.<br/>
必须在SyncBody中为客户端发送的SyncHdr和Alerts返回状态。
3. Any management operation including user interaction in the SyncML document (e.g. Alert, Sequence, Replace) are placed into the SyncBody.<br/>
任何管理操作，包括SyncML文档中的用户交互（例如，Alert，Sequence，替换）在SyncBody中。
  * CmdID is REQUIRED.<br/> CmdID是必需的
  * Source MUST be used if URI is needed to further address the source dataset.<br/>
  如果需要URI来进一步寻址源数据集，则必须使用Source。
  * Target MUST be used if URI is needed to further address the target dataset.<br/>
  如果需要URI来进一步寻址目标数据集，必须使用Target。
  * The Data element inside Item is used to include the data itself unless the command does not require a Data element.<br/>
  Item中的Data元素用于包含数据本身，除非命令不需要Data元素。
  * The Meta element inside an operation or inside an Item MUST be used when the Type or Format are not the default values [META].<br/>
  当Type或Format不是默认值[META]时，必须使用操作中或Item内部的元元素。
4. The Final element MUST be used in the SyncBody for the message, which is the last in this package.<br/>
Final元素必须在消息的SyncBody中使用，这是此包中的最后一个。

## 2.3.5 Package 3: Client response sent to server 包3：客户端响应发送到服务器
The content of package 3 is:
包3的内容是：
* Results of management actions sent from server to client.<br/>
从服务器发送到客户端的管理操作的结果。
* Results of user interaction commands.<br/>
用户交互命令的结果。
* New optional Client generated alert, for example Generic Alert or Client Event [REPPRO] that was raised during the session.<br/>
新的可选的客户端生成的警报，例如在会话期间引发的通用警报或客户端事件[REPPRO]。

This package is sent by the client if Package 2 contained management commands that required a response from the client.<br/>
如果包2包含需要来自客户端的响应的管理命令，则该包由客户端发送。

The detailed requirements for package 3 are:<br/>
包3的详细要求是：
1. The requirements for the elements within the SyncHdr element.<br/>
SyncHdr元素中的元素的要求
   * The value of the VerDTD element MUST be '1.2'.<br/>
   VerDTD元素的值必须为“1.2”。
   * The value of the VerProto element MUST be ‘DM/1.2’.<br/>
   VerProto元素的值必须为“DM/1.2”。
   * SessionID MUST be included to indicate the ID of the management session.<br/>
   必须包括SessionID以指示管理会话的ID。
   * MsgID MUST be used to unambiguously identify the message belonging to the management session from server to client.<br/>
   MsgID必须用于明确标识从服务器到客户端的属于管理会话的消息。
   * The Target element MUST be used to identify the target device.<br/>
   Target元素必须用于标识目标设备。
   * The Source element MUST be used to identify the source device.<br/>
   Source元素必须用于标识源设备。
2. Status MUST be returned for the SyncHdr and Alert command sent by the device management server in the SyncBody.<br/>
必须为SyncBody中的设备管理服务器发送的SyncHdr和Alert命令返回Status。
3. Status MUST be returned in the SyncBody for management operations sent by the server in Package 2.<br/>
必须在SyncBody中返回Status，以便在包2中由服务器发送管理操作。
4. Results MUST be returned in the SyncBody for successful Get operations sent by the server in the previous package and the following requirements apply:<br/>
必须在SyncBody中返回结果，以便成功获取由上一个程序包中的服务器发送的Get操作，并满足以下要求：
   * Results MUST contain Meta element with Type and Format elements describing content of Data element, unless the Type and Format have the default values [META].<br/>
   Results须包含Meta元素，其中Type和Format元素描述Data元素的内容，除非Type和Format具有默认值[META]。
   * Items in Results MUST contain the Source element that specifies the source URI.<br/>
   结果中的项必须包含指定源URI的Source元素。
5. Client MAY send client generated alerts, for example Client Event [REPPRO] or Generic Alert.<br/>
   客户端可以发送客户端生成的警报，例如客户端事件[REPPRO]或通用警报。
   
The Final element MUST be used in the SyncBody for the message, which is the last in this package.<br/>
Final元素必须在消息的SyncBody中使用，该消息是此程序包中的最后一个。

## 2.3.6 Package 4: Further server management operations 包4：进一步的服务器管理操作
Package 4 is used to close the management session. If the server sends any operation in Package 4 that needs response from the client, the protocol restarts from Package 3 with a new protocol iteration. Server sends results of Client Initiated Alerts if any of these was received from the client in previous package. The detailed requirements for package 4 are:<br/>
包4用于关闭管理会话。如果服务器在包4中发送需要来自客户端的响应的任何操作，则协议以新的协议从包3重新开始重复。服务器发送客户端发起的警报的结果（如果这些警报中的任何一个是从先前包中的客户端接收的）。包4的详细要求是：

1. The requirements for the elements within the SyncHdr element. <br/>
 SyncHdr元素中的元素的要求。
  * The value of the VerDTD element MUST be '1.2'.<br/>
  VerDTD元素的值必须为“1.2”。
  * The value of the VerProto element MUST be ‘DM/1.2’.<br/>
  VerProto元素的值必须为“DM/1.2”。
  * SessionID MUST be included to indicate the ID of the management session.<br/>
  必须包括SessionID以指示管理会话的ID。
 * MsgID MUST be used to unambiguously identify the message belonging to the management session from server to client.<br/>
 MsgID必须用于明确标识从服务器到客户端的属于管理会话的消息。
 * The Target element MUST be used to identify the target device.<br/>
 Target元素必须用于标识目标设备
 * The Source element MUST be used to identify the source device.<br/>
 Source元素必须用于标识源设备。
2. Status MUST be returned for the SyncHdr sent by the device management server in the SyncBody and if any Alerts were sent by the client then the server MUST send Status for these Alerts.<br/>
必须为SyncBody中的设备管理服务器发送的SyncHdr返回Status，并且如果客户端发送了任何警报，则服务器必须为这些警报发送状态。

3. Any management operation including user interaction in the SyncML document (e.g. Alert, Sequence, Replace) placed into the SyncBody. <br/>
包括置于SyncBody中的SyncML文档（例如，Alert, Sequence, Replace）中的用户交互的任何管理操作。
  * CmdID is REQUIRED.<br/>
CmdID是必需的。
  * Source MUST be used if URI is needed to further address the source dataset.<br/>
 如果需要URI来进一步寻址源数据集，则必须使用Source。
  * Target MUST be used if URI is needed to further address the target dataset.<br/>
 如果需要URI来进一步寻址目标数据集，必须使用Target。
  * The Data element inside Item is used to include the data itself unless the command does not require a Data element.<br/>
 Item中的Data元素用于包含数据本身，除非命令不需要Data元素。
  * The Meta element inside an operation or inside an Item MUST be used when the Type or Format are not the default values [META].<br/>
  当Type或Format不是默认值[META]时，必须使用操作中或Item内部的Meta元素。

The Final element MUST be used in the SyncBody for the message, which is the last in this package. Package 4 MAY close the management session by containing only the `<Final>` element (any management command or user interaction command will continue the session). Alternately, the server may send the Session Abort Alert (1223) to force the close of the session in extreme situations.<br/>
Final元素必须在消息的SyncBody中使用，该消息是此程序包中的最后一个。包4可以通过只包含`<Final>`元素（任何管理命令或用户交互命令将继续会话）关闭管理会话。或者，服务器可以发送会话中止警报（1223）以在极端情况下强制会话的关闭。

## 2.3.7 Generic Alert 通用警报
The protocol defines a Generic Alert message for Alerts generated by the client that MAY have a relation to a Management Object. In the case of a relation to a Management Object then the Source and LocURI MUST identify the address to that Management Object.<br/>
协议定义了由可能与管理对象有关系的客户端生成的警报的通用警报消息。在与管理对象的关系的情况下，Source和LocURI必须标识该管理对象的地址。

Anytime after the Client or Server Initiated Management Alert, the client MAY send a Generic Alert message to the server. The Generic Alert message SHALL only be sent from the client to the server. After the server has received the Generic Alert the server MUST respond with the status for how the server handles all Items.<br/>
在客户端或服务器启动管理警报之后的任何时间，客户端可以向服务器发送通用警报消息。通用警报消息必须只能从客户端发送到服务器。服务器接收到通用警报后，服务器必须响应服务器如何处理所有项目的状态。

The client MAY send multiple Alert messages of code “Generic Alert” or combine them together with multiple Items inside one or multiple Alert message of code “Generic Alert”. The Data in the Generic Alert message is not specified in the protocol, the protocol will specify how the client can inform the server what Type and Format it is. The server MUST support the Generic Alert Format but not all Types of the alert data. The Server MUST respond with status 415 “Unsupported media Type or Format” if the Type and Format are unsupported by the server. If the device does not support Large Object then the Alert message MUST NOT exceeds the message size.<br/>
客户端可以发送代码“通用警报”的多个警报消息，或者将它们与代码“通用警报”的一个或多个警报消息中的多个项目组合在一起。通用警报消息中的数据未在协议中指定，协议将指定客户端如何通知服务器其类型和格式。服务器必须支持通用警报格式，但不支持所有类型的警报数据。如果服务器不支持类型和格式，则服务器必须响应状态415 “Unsupported media Type or Format”。如果设备不支持大对象，则警报消息不得超过消息大小。

This specification only specifies what is required from the protocol perspective, some registered Generic Alerts MAY have additional requirements for different Types of Generic Alert Data. For example, one registered Type of Alert may define that a reference to a Management Object is mandatory and the Format must be of Type Integer and the Alert Data must be included inside the Data.<br/>
本规范仅指定从协议角度所需的内容，某些注册的通用警报可能对不同类型的通用警报数据有其他要求。例如，一种注册的警报类型可以定义对管理对象的引用是强制性的，并且格式必须是整数，并且警报数据必须包括在数据内部。


The optional parameter Mark MUST contain the importance level. If the parameter is omitted then the default importance level is assumed.<br/>
可选参数Mark必须包含重要性级别。如果省略参数，则采用默认重要性级别。

The server MUST respond with status 200 “OK” or 202 “Accepted for processing” if the server has received the Alert without any errors, in other case the server MUST use one of the following error status codes: 401, 407, 412, 415 and 500.<br/>
如果服务器已经接收到警报而没有任何错误，则服务器必须响应状态200“OK”或202 “Accepted for processing”，否则服务器必须使用以下错误状态代码之一：401, 407, 412, 415和500。