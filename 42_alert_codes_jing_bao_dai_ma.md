# 4.2 Alert Codes 警报代码
Only the alert codes listed in this section are valid in OMA DM Protocol. <br/>
只有本节中列出的警报代码在OMA DM协议中有效。

OMA DM Protocol alert codes start at 1100.<br/>
OMA DM协议警报代码在1100开始。

| Alert Code Value <br/> 警报代码值 | Name<br/> 名称 | Description<br/> 描述 |
| -- | -- | -- |
|  | User interaction alert codes <br/> 用户交互警报代码 |  |
| 1100 | DISPLAY | The Alert is sent by the server and the client should display the message to provide information to the user.<br/> 警报由服务器发送，客户端应显示消息以向用户提供信息。 |
| 1101 | CONFIRM OR REJECT | This Alert is sent by the server and the client should display the message sent by the server and ask for confirmation. If the user doesn't confirm the operation, reject status MUST be sent back.<br/> 此警报由服务器发送，客户端应显示服务器发送的消息并要求确认。 如果用户不确认操作，拒绝状态必须发回。 |
| 1102 | TEXT INPUT | The terminal displays the message sent inside the Alert then allows the user to type in a text string. This text string is then sent back to the server in a Status message.<br/>终端显示在警报内发送的消息，然后允许用户键入文本字符串。然后，此文本字符串将在状态消息中发送回服务器。 |
| 1103 | SINGLE CHOICE | The user is presented a set of choices from which he or she is allowed to select only one. <br/>向用户呈现一组选择，从这些选择中,他或她被允许仅选择一个。 |
| 1104 | MULTIPLE CHOICE | The user is presented a set of choices from which he or she is allowed to select one or more. <br/>向用户呈现一组选择，从这些选择中, 他或她被允许选择一个或多个。 |
| 1105 - 1199 |  |  Reserved for future SyncML usage. <br/>保留用于将来的SyncML使用。|
|  | Device management session alert codes <br/> 设备管理会话警报码 |  |
| 1200 | SERVER-INITIATED MGMT | Specifies a server-initiated device management session. <br/> 指定服务器启动的设备管理会话。 |
| 1201 | CLIENT-INITIATED MGMT | Specifies a client-initiated device management session. <br/> 指定客户端发起的设备管理会话。 |
| 1202 – 1220   |  |  Reserved for future SyncML usage. <br/>保留用于将来的SyncML使用。|
|  | Special device management alert codes <br/> 特殊设备管理警报代码 |  |
| 1222 | NEXT MESSAGE | Specifies a request for the next message in the package. See [DMPRO]. <br/> 指定包中下一封消息的请求。参见[DMPRO]。 |
| 1223 | SESSION ABORT | Informs the recipient that the sender wishes to abort the device management session. See [DMPRO]. <br/> 通知接收者发送者希望中止设备管理会话。参见[DMPRO]。 |
| 1224 | CLIENT EVENT | Informs the server that an event has occurred on the client. Event data MUST be contained in Data element of an Item element. <br/> 通知服务器客户端上已发生事件。事件数据必须包含在Item元素的Data元素中。 |
| 1225 | NO END OF DATA | End of Data for chunked object not received. <br/> 未收到分块对象的数据结束标志。 |
| 1226 | GENERIC ALERT | Generic client generated alert with or without a reference to a Management Object. <br/> 带或不带引用管理对象的通用客户端生成警报。 |
| 1227 – 1299   |  |  Reserved for future SyncML usage. <br/>保留用于将来的SyncML使用。|

