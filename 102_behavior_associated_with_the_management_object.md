# 10.2  Behavior Associated with the Management Object 与管理对象相关的行为

The following diagram shows the various valid states of the mobile device as they are related to firmware updates. It is possible that the server may not see some of these states.<br/>
下图显示了移动设备与固件更新相关的各种有效状态。 服务器可能无法看到这些状态中的一些。

![](10.2.jpeg)
Typically, the starting state is ‘Idle/Start’ and the terminating states are one of:<br/>
通常，起始状态是“空闲/开始”，并且终止状态是以下之一：
*	Update Failed / Have Data 
    更新失败/有数据
*	Update Failed / No Data 
    更新失败/无数据
*	Update Successful / Have Data
    更新成功/有数据
*	Update Successful / No Data
    更新成功/无数据
*	Download Failed
	下载失败

## 10.2.1 ‘Exec’ Command "Exec"命令
The ‘Exec’ command MUST be supported. <br/>
必须支持'Exec'命令。

The server issues ‘Exec’ commands to initiate long running operations in the client, such as download and update. The result of the ‘Exec’ command, encoded as a ResultCode, is returned in a Generic Alert following completion of the operation. A correlator, if supplied with the ‘Exec’ command, is also returned in that Generic Alert.  The client MUST send a status 202 (asynchronous) for the ‘Exec’ operation if the command is accepted for later processing.<br/>
服务器发出“Exec”命令以在客户端中启动长时间运行的操作，例如下载和更新。在操作完成后，在通用报警中返回编码为ResultCode的“Exec”命令的结果。如果提供了'Exec'命令，相关器也会在该通用警报中返回。如果命令被接受用于以后的处理，客户端必须发送用于'Exec'操作的状态202（异步）。

Optionally a User Interaction Alert [DMPRO] can be used for soliciting user opt-in prior to the execution of the Exec command on the Download node. <br/>
可选地，用户交互警报[DMPRO]可以用于在下载节点上执行Exec命令之前请求用户选择加入。

In the case of a download of an update package employing the large-object download feature of the OMA-DM protocol [DMPRO], the ‘Replace’ command is used by the DM server to initiate the download, prior to the invocation of an ‘Exec’ command to invoke the update activity.<br/>
在下载采用OMA-DM协议[DMPRO]的大对象下载特征的更新包的情况下，DM服务器使用“替换”命令来启动下载，在调用“Exec'命令前来调用更新活动。

The State element in the management object is updated to indicate the state the client reached during the corresponding Exec initiated update or download activity (See Chapter 10.2.).<br/>
管理对象中的State元素被更新，以指示客户端在相应的Exec启动的更新或下载活动期间达到的状态（请参见第10.2章）。

### 10.2.1.1 ‘Exec’ Command "Exec"命令
The server issues an ‘Exec’ command targeting the x/Download node. The client initiates an alternate download operation from the URL identified in the x/Download/PkgURL value. When the download operation is complete, the client issues a Generic Alert indicating the result of the download operation.<br/>
服务器发出一个“Exec”命令，目标是x/Download节点。 客户端从x/Download/PkgURL值中标识的URL启动备用下载操作。当下载操作完成时，客户端发出指示下载操作的结果的通用警报。

#### 10.2.1.1.1 Example of ‘Exec’ Command for Alternate Download 备用下载的'Exec'命令示例
Pre-Condition: The following element needs to be set with an appropriate value:<br/>
前提条件：以下元素需要设置一个适当的值：

`x/Download/PkgURL` is set<br/>
`x/Download/PkgURL` 已被设置好

Example of ‘Exec’ command:
'Exec'命令示例：
```
<Exec>
	<CmdID>3</CmdID>
	<Item>
		<Target>
			<LocURI>x/Download</LocURI>
		</Target>
	</Item>
</Exec>

```
### 10.2.1.2 ‘Exec’ Command Semantics for Update 用于更新的'Exec'命令语义

The server issues an ‘Exec’ command targeting the x/Update node. The client applies the previously received update package. When the update operation is complete, the client issues a Generic Alert indicating the result of the update operation.<br/>
服务器发出一个“Exec”命令，目标是x/Update节点。客户端应用预先接收更新包。更新操作完成后，客户端将发出一个通用警报，指示更新操作的结果。

### 10.2.1.2.1 	Example of ‘Exec’ Command for Update 用于更新的'Exec'命令示例
Pre-Condition: 预先条件

The firmware update package must be available on the device.<br/>
固件更新包必须在设备上可用。

Example of ‘Exec’ command:<br/>
'Exec'命令示例：
```
<Exec>
	<CmdID>3</CmdID>
	<Item>
		<Target>
			<LocURI>x/Update</LocURI>
		</Target>
 	</Item>
</Exec>
```
### 10.2.1.3 ‘Exec’ Command Semantics for Download And Update 用于下载和更新的'Exec'命令语义
The server issues an ‘Exec’ command targeting the x/DownloadAndUpdate node. The client initiates an alternate download operation from the URL identified in the x/DownloadAndUpdate/PkgURL value. When the download operation is completed successfully, the client applies the received update package without further server intervention. When the update operation is complete, the client issues a Generic Alert indicating the result of the update operation. In the event that the download fails, the client issues a Generic Alert indicating the failure of the download operation.<br/>
服务器发出一个“Exec”命令，目标是x/DownloadAndUpdate节点。 客户端从x/ DownloadAndUpdate/PkgURL值中标识的URL启动备用下载操作。当下载操作成功完成时，客户端应用所接收的更新包而无需进一步的服务器干预。更新操作完成后，客户端将发出一个通用警报，指示更新操作的结果。在下载失败的情况下，客户端发出指示下载操作失败的通用警报。

The Update activity is launched at the next practical opportunity.<br/>
更新活动在下一个实际机会时启动。

#### 10.2.1.3.1 Example of ‘Exec’ Command for DownloadAndUpdate 用于下载和更新的'Exec'命令示例
Pre-Condition: The following element needs to be set with an appropriate value:<br/>
前提条件：以下元素需要设置一个适当的值：

`x/Download/PkgURL` is set<br/>
`x/Download/PkgURL` 已被设置好

Example of ‘Exec’ command:<br/>
'Exec'命令示例：
```
<Exec>
	<CmdID>3</CmdID>
	<Item>
		<Target>
			<LocURI>x/DownloadAndUpdate</LocURI>
		</Target>
 	</Item>
</Exec>

```
## 10.2.2 Use of Generic Alert for Notifications 将通用警报用于通知
At the end of the operation invoked by the Exec commands in section 10.2.1, the device MUST send a notification to the DM server via a Generic Alert [DMPRO] message.  The alert message includes the following data:<br/>
在6.1节中的Exec命令调用的操作结束时，设备务必通过通用警报[DMPRO]消息向DM服务器发送通知。警报消息包括以下数据：

*	An integer result code – Used to report status of the operation<br/>
整数结果代码 - 用于报告操作的状态


*	The URI of the Firmware Update Management Object – Used to identify the source<br/>
固件更新管理对象的URI - 用于标识源

*	An alert type – Used to identify the operation<br/>
警报类型 - 用于识别操作

*	Correlator – Used by the server and passed as part of the Exec command<br/>
相关器 - 由服务器使用并作为Exec命令的一部分传递

Alerts that are reporting an error or failure condition SHOULD report a severity other than Informational in the Mark field of the Meta information.<br/>
报告错误或失败条件的警报应在Meta信息的标记字段中报告除了信息之外的严重性。

Once the Generic Alert message is sent to the DM Server at the end of the operation, the device MUST NOT retry the operation invoked via the Exec command by the DM Server without further server intervention. <br/>
一旦在操作结束时将通用警报消息发送到DM服务器，设备必须不重试由DM服务器通过Exec命令调用的操作，而不需要进一步的服务器干预。

NOTE: If the server needs to retrieve additional information, such as State, then the server MAY query the device for those specific nodes.<br/>
注意：如果服务器需要检索附加信息（例如状态），则服务器可以向设备查询这些特定节点。

## 10.2.2.1	URI of Firmware Update Management Object 固件更新管理对象的URI
The URI of the Firmware Update Management Object MUST be sent as the source of the Generic Alert [DMPRO] message.  This allows the Management Server to identify the origin of the alert.<br/>
固件更新管理对象的URI必须作为通用警报[DMPRO]消息的源发送。这允许管理服务器识别警报的来源。

## 10.2.2.2	Firmware Update Alert Types 固件更新警报类型
One of the following alert types MUST be used in a Generic Alert [DMPRO] message originating from a Firmware Update Management Object. The alert types are used to identify the Exec operation that was performed on the device.<br/>
在来自固件更新管理对象的通用警报[DMPRO]消息中必须使用以下警报类型之一。警报类型用于标识在设备上执行的Exec操作。
* The alert type “org.openmobilealliance.dm.firmwareupdate.download” MUST be used in response to the completion of a Download operation.
* The alert type “org.openmobilealliance.dm.firmwareupdate.update” MUST be used in response to the completion of an Update operation
* The alert type “org.openmobilealliance.dm.firmwareupdate.downloadandupdate” MUST be used in response to the completion of a DownloadAndUpdate  operation

## 10.2.2.3	Correlator 相关器
If the server passes a correlator to the client in the Exec command of a Firmware Update Operation, the client MUST return the same value to the server in the correlator field of the Generic Alert [DMPRO] message.<br/>
如果服务器在固件更新操作的Exec命令中将相关器传递给客户端，则客户端必须在通用警报[DMPRO]消息的相关器字段中向服务器返回相同的值。

If the server does not pass a correlator to the client in the Exec command of a Firmware Update Operation, the client MUST NOT send a correlator to the server in the correlator field of the Generic Alert [DMPRO] message.<br/>
如果服务器在固件更新操作的Exec命令中未将相关器传递给客户端，则客户端不必在通用警报[DMPRO]消息的相关器字段中向服务器发送相关器。

## 10.2.2.4	Result Code 结果代码
The result code of the operation MUST be sent as an integer value in the Data element of the GenericAlert [DMPRO] message. The ResultCode MUST be one of the values defined below:<br/>
操作的结果代码必须作为一个整数值发送到通用报警[DMPRO]消息的Data元素中。结果代码必须是以下定义的值之一：

| Result Code 结果代码 | Meaning 含义 | Usage 用法 |
| -- | -- | -- |
| 200 | Successful<br/> 成功 | Successful – The Request has Succeeded.<br/> 成功 - 请求已成功 |
| 250 -299 | Successful – Vendor Specified<br/> 成功 - 指定供应商 | Successful Operation with Vendor Specified ResultCode.<br/> 使用供应商指定的结果代码成功操作。 |
| 400 | Management Client Error <br/>管理客户端错误 | Management Client error – based on User or Device behavior<br/> 管理客户端错误 - 基于用户或设备行为 |
| 401 | User Cancelled<br/> 用户已取消 | User chose not to accept the operation when prompted. 用户在提示时选择不接受操作 |
| 402 | Corrupted Firmware Update Package <br/> 损坏的固件更新软件包 | Corrupted firmware update package, did not store correctly.  Detected, for example, by mismatched CRCs between actual and expected.<br/>损坏的固件更新包，没有正确存储。例如，通过CRC检测发现实际和期望之间的不匹配。 |
| 403 | Firmware Update Package – Device Mismatch 固件更新软件包 - 设备不匹配 | Wrong Firmware Update Package delivered to device based on current device characteristics.<br/> 根据当前设备特性将错误的固件更新软件包传送到设备。 |
| 404 | Failed Firmware Update Package Validation <br/>固件更新软件包验证失败 | Failure to positively validate digital signature of firmware update package.<br/>未正确验证固件更新包的数字签名 |
| 405 | Firmware Update Package Not Acceptable <br/>固件更新程序包不可接受 | Firmware Update Package is Not Acceptable<br/>固件更新包不可接受 |
| 406 | Alternate Download  Authentication Failure<br/> 备用下载认证失败 | Authentication was Required but Authentication Failure was encountered when downloading Firmware Update Package.<br/>验证是必需的，但下载固件更新程序包时遇到了验证失败。 |
| 407 | Alternate Download  Request Time-Out<br/>备用下载请求超时 | Client has encountered a time-out when downloading Firmware Update Package<br/>客户端在下载固件更新包时遇到超时 |
| 408 | Not Implemented <br/> 未实现 | The device does not support the requested operation.<br/> 设备不支持请求的操作。|
| 409 | Undefined Error<br/> 未定义错误 | Indicates failure not defined by any other error code.<br/>表示未由任何其他错误代码定义的故障。 |
| 410 | Firmware Update Failed<br/>固件更新失败 | Firmware Update operation failed in device.<br/>设备中的固件更新操作失败 |
| 411 | Malformed or Bad URL<br/>格式错误或网址不正确 | The URL provided for alternate download is bad<br/>为备用下载提供的网址不正确 |
| 450-499 | Client Error – Vendor Specified<br/>客户端错误 - 指定的供应商 | Client Error encountered for Operation with Vendor Specified Result Code<br/>使用供应商指定的结果代码进行操作时遇到客户端错误 |
| 500 | Firmware Update Failed<br/>固件更新失败 | Firmware Update operation failed in device.<br/>设备中的固件更新操作失败 |
| 501 | Download fails due to device is out of memory<br/>由于设备内存不足，下载失败 | The download fails due insufficient memory in the device to save the firmware update package.<br/>下载失败，因为设备中的内存不足，无法保存固件更新包。 |
| 502 | Firmware update fails due to device out of memory<br/>固件更新由于设备内存不足而失败 | The update fails because there isn’t sufficient memory to update the device.<br/>更新失败，因为没有足够的内存来更新设备。 |
| 503 | Download fails due to network issues<br/>由于网络问题，下载失败 | The download fails due to network/transport level errors.<br/>由于网络/传输级别错误，下载失败。|
| 550 -599 | Alternate Download Server Error – Vendor Specified<br/>备用下载服务器错误 - 指定供应商 | Alternate Download Server Error encountered for Operation with Vendor Specified ResultCode.<br/>使用供应商指定的结果代码进行操作时遇到备用下载服务器错误。|