# 10.3 Client Initiated Firmware Update 客户端启动的固件更新
## 10.3.1 General 总体
Firmware Upgrade is in its nature device dependent. This feature is therefore an optional feature for client devices and for servers. This section only defines the format of the client initiated message and not in which circumstances the client device will send it. This message is an information message to the server so that the server should investigate if an update is needed. The device can send two different Firmware Update requests dependent on if it is originated from the Device or a User. The client SHOULD NOT expect any specific Firmware Update action from the server. If the Alert Type is “User Initiated”, then the server MAY send User Interaction Commands in the same session to inform the user how the server will handle the firmware update request. The Server MAY investigate if update is needed in the same session, but MAY also inform the user that the server will investigate this later on.<br/>
固件升级的性质取决于设备。因此，此功能是客户端设备和服务器的可选功能。本节仅定义客户端发起的消息的格式，而不是客户端设备将在哪种情况下发送它。此消息是到服务器的信息消息，以便服务器应调查是否需要更新。取决于设备是源自设备还是用户，设备可以发送两个不同的固件更新请求。客户端不应期望服务器的任何特定固件更新操作。如果警报类型是“用户启动”，则服务器可以在同一会话中发送用户交互命令以通知用户服务器将如何处理固件更新请求。服务器可以调查是否需要在同一会话中更新，但也可以通知用户服务器将调查此后。

The Generic Alert format is used for this notification. The Server MAY respond with specific Status Codes as follows:<br/>
通用警报格式用于此通知。服务器可以使用特定的状态代码进行响应，如下所示:

 If the update package is available and the Server will command update operations in the same session, the Server MAY respond with status 200 “OK”. If the update package is not available or the Server will not command update operations in the same session, the Server SHOULD respond with status 202 “Accepted for processing”. <br/>
如果更新包可用并且服务器将在同一会话中命令更新操作，则服务器可以用状态200“OK”进行响应。如果更新包不可用或服务器不会在同一会话中命令更新操作，则服务器应响应状态202“Accepted for processing”。 

The following client requirements MUST be supported if Client Initiated Firmware Update is implemented:<br/>
如果实施客户端启动的固件更新，则必须支持以下客户端要求：

## 10.3.1.1 Generic Alert 通用警报
The message MUST follow the Generic Alert format. <br/>
该消息必须遵循通用警报格式。

## 10.3.1.2 Alert Type 警报类型
The message MUST use the alert type: “org.openmobilealliance.dm.firmwareupdate.devicerequest” for device initiated firmware update and alert type: “org.openmobilealliance.dm.firmwareupdate.userrequest” for user initiated firmware update.<br/>
该消息必须使用警报类型：“org.openmobilealliance.dm.firmwareupdate.devicerequest”用于设备启动的固件更新和警报类型：“org.openmobilealliance.dm.firmwareupdate.userrequest”用于用户启动的固件更新。

## 10.3.1.3 URI
The URI in the alert, if specified, MUST point to the dynamic node (e.g., the `<x>`) representing a single firmware update management object in the tree. When present, the server investigates the availability of updates for the firmware indicated by the management object. It is further suggested when not present, the server investigates the availability of all relevant firmware updates for the terminal originating the alert. The server MAY query the contents of the management object specified by a URI. The server SHOULD initiate a firmware update if any relevant updates are discovered. <br/>
如果指定，则警报中的URI必须指向表示树中的单个固件更新管理对象的动态节点（例如，`<x>`）。当存在时，服务器调查由管理对象指示的固件的更新的可用性。进一步建议，当不存在时，服务器调查发起警报的终端的所有相关的固件更新的可用性。服务器可以查询由URI指定的管理对象的内容。如果发现任何相关更新，则服务器应启动固件更新。

## 10.3.1.4 Data
The Data element MUST be included. A client vendor MAY use the data field to supply implementation specific data. In case there is no implementation specific data the value needs to be left empty.<br/>
必须包括数据元素。客户端供应商可以使用数据字段来提供实现特定的数据。如果没有实现特定的数据，该值需要保留为空。

