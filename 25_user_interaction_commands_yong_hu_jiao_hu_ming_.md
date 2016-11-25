# 2.5 User interaction commands 用户交互命令
## 2.5.1 Introduction 介绍
The OMA Device Management Protocol specifies following user interaction types for example to notify and obtain confirmation from the user regarding the management operation. These interaction types are the following:<br/>
OMA设备管理协议指定以下用户交互类型，例如通知并获得来自用户关于管理操作的确认。这些交互类型如下：

* User displayable notification associated with a certain action.<br/>
与某个操作相关联的用户可显示通知。
* Confirmation from the user to execute a certain management operation.<br/>
确认用户执行特定的管理操作。
* Prompt user to provide input for upcoming management operation.<br/>
提示用户为即将到来的管理操作提供输入。
* Prompt user to select item or items among items.<br/>
提示用户选择项目之间的项目或单个项目。
* Display progress notification for a certain action.<br/>
显示某个操作的进度通知。

## 2.5.2 User interaction alert codes 用户交互提醒代码
These Alert's can be sent only from the server to the client. Clients MUST report 406: “Optional Feature Not Supported”, if client does not support User Interaction Alerts. If sent by the client, they are ignored by the server. Multiple user interaction Alert's can be present in Package 2, in this case the client executes them by arbitrary order (unless Sequence is used) and sends back the results in multiple Status packages in Package 3. If the protocol continues after Package 4, Package 4 can also contain user interaction Alert's.<br/>
这些提醒只能从服务器发送到客户端。如果客户端不支持用户交互提醒，客户端必须报告406：“Optional Feature Not Supported”。如果由客户端发送，它们将被服务器忽略。多个用户交互提醒可以出现在包2中，在这种情况下客户端以任意顺序执行它们（除非使用Sequence），并且在包3中的多个Status包中发送结果。如果协议在包4继续，包4也可以包含用户交互提醒。

When a user interaction is executed, server is notified about the outcome of the interaction in a Status message. The user interaction-specific Status responses are described in [DMREPPRO].<br/>
当执行用户交互时，交互的结果由Status消息通知服务器。用户交互特定的Status响应在[DMREPPRO]中描述。

All user interaction Alert's contain two or more Item elements. Client MUST preserve the order of these Item elements. Client MUST also process these Item elements in the same order as they are in the message.<br/>
所有用户交互提醒包含两个或多个Item元素。客户端必须保持这些Item元素的顺序。客户端还必须以与消息中相同的顺序处理这些Item元素。

User interactions, except display, SHOULD have user option to cancel operation. If the user decides to cancel the operation, then management message processing is stopped. Status codes for executed commands are reported normally and status code (215) Not executed is returned to all commands which are not processed.After processing the user response the server might decide to continue protocol with some other management operation.<br/>
除显示外，推荐用户交互具有用于取消操作的用户选项。如果用户决定取消操作，则停止管理消息处理。正常报告已执行命令的状态代码，状态代码（215）Not executed将返回到未处理的所有命令。处理用户响应后，服务器可能决定使用某些其他管理操作继续协议。

If the UI allows the user to cancel(for any of the UI Alerts),then the status(214) Operation cancelled should be returned for the Alert.<br/>
如果UI允许用户取消（对于任何UI提醒），则应当针对提醒返回状态（214）Operation cancelled的操作。

## 2.5.2.1 Display 显示
The SyncML DISPLAY Alert is slightly changed in OMA DM Protocol. The Alert has two Items.<br/>
SyncML DISPLAY提醒在OMA DM协议中略有更改。警报有两个项目。
* The first Item contains optional parameters as specified in Section 2.5.3.<br/>
第一个Item包含第2.5.3节中指定的可选参数。
* The second Item has exactly one Data element containing the text to be displayed to the user.<br/>
第二个Item正好有一个Data元素，其中包含要显示给用户的文本。

Example: 范例
```
<Alert>
  <CmdID>2</CmdID>
  <Data>1100</Data> 
  <Item><Data>MINDT=10</Data></Item>
  <Item>
      <Data>Management in progress</Data>
  </Item>
</Alert>
```
## 2.5.2.2 Confirmation 确认
Confirmation is a binary decision: the user either approves or rejects the option. A new Alert code is introduced for this purpose, the CONFIRM_OR_REJECT. When the client receives this Alert, it displays the Alert text then enables the user to select "Yes" or "No". If the answer is "Yes", the status code 200: “Yes” is returned and the processing of the package continues without change in processing. If the answer is "No", the status code 304: “No” is returned and the processing of the package ceases. If the UI allows the user to cancel, status 214: “Operation cancelled” should be returned for the Alert.<br/>
确认是一个二元决策：用户允许或拒绝该选项。为此目的引入了一个新的提醒代码CONFIRM_OR_REJECT。当客户端接收到此提醒时，它显示提醒文本，然后使用户选择“是”或“否”。如果答案为“是”，则返回状态代码200：“Yes”，并且包没有改变地继续处理。如果答案为“否”，则返回状态代码304：“No”，并且包的处理停止。如果UI允许用户取消，则应当针对提醒返回状态214：“Operation cancelled”。

If user answers "No", then package processing will change according to placement of confirmation Alert in package as follows.<br/>
如果用户回答“否”，则包处理将根据包中的确认提醒的位置而改变，如下。

* If confirmation Alert is inside Atomic, then Atomic fails and all executed commands have to be rolled back.<br/>
如果确认提醒在Atomic中，则Atomic将失败，并且必须回滚所有已执行的命令。

* If confirmation Alert is inside Sequence, then commands in Sequence after confirmation Alert are bypassed.<br/>
如果确认提醒在Sequence中，则确认提醒后Sequence中的命令被绕过。

* If confirmation Alert is not inside Atomic or Sequence i.e. it is directly in SyncBody, then user response has no effect to package processing. In this way server can query user opinion before sending actual management commands to client device.<br/>
如果确认警报不在Atomic或Sequence内，即它直接位于SyncBody中，则用户响应对包处理没有影响。通过这种方式，服务器可以在向客户端设备发送实际管理命令之前询问用户意见。

Statuscode(215) Not Executed will be sent back for the commands whose execution was bypassed as result of user interaction.<br/>
状态代码（215）Not Executed 将返回用户交互后跳过执行的指令。

The Alert contains two Items.<br/>
警报包含两个Item。
* The first Item contains the optional parameters as specified in Section 10.3.<br/>
第一个Item包含第2.5.3节中指定的可选参数。
*  The second Item has exactly one Data element containing the text to be displayed to the user.<br/>
第二个项目正好有一个Data元素，其中包含要显示给用户的文本。