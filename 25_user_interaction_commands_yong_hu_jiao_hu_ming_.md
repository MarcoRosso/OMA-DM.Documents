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
如果确认提醒不在Atomic或Sequence内，即它直接位于SyncBody中，则用户响应对包处理没有影响。通过这种方式，服务器可以在向客户端设备发送实际管理命令之前询问用户意见。

Statuscode(215) Not Executed will be sent back for the commands whose execution was bypassed as result of user interaction.<br/>
状态代码（215）Not Executed 将返回用户交互后跳过执行的指令。

The Alert contains two Items.<br/>
提醒包含两个Item。
* The first Item contains the optional parameters as specified in Section 10.3.<br/>
第一个Item包含第2.5.3节中指定的可选参数。
*  The second Item has exactly one Data element containing the text to be displayed to the user.<br/>
第二个Item正好有一个Data元素，其中包含要显示给用户的文本。

Example: 范例
```
<Alert>
  <CmdID>2</CmdID>
  <Data>1101</Data>
  <Item></Item> <!-- no optional parameters -->
  <Item>
    <Data>Do you want to add the CNN access point?</Data> 
  </Item>
</Alert>
```
Result if user responds "No": 如果用户响应“否”的结果：
```
<Status>
  <CmdID>2</CmdID>
  <MsgRef>1</MsgRef>
  <CmdRef>2</CmdRef>
  <Cmd>Alert</Cmd>
  <Data>304</Data> <!-- Not modified -->
</Status>
```
If the result in the above example had been that the user chose Yes, the status would have been (200).<br/>
如果上述示例中的结果是用户选择“是”，则状态将为（200）。

## 2.5.2.3 User input 用户输入
When this Alert is sent, the client displays the text then allows the user to type in a text string. This text string is then sent back to the server in a Status message.<br/>
发送此提醒时，客户端显示文本，然后允许用户键入文本字符串。然后，此文本字符串将在状态消息中发送回服务器。

The server instructs the client to execute this user interaction by sending a TEXT INPUT Alert. The Alert contains at least two Items.<br/>
服务器通过发送TEXT INPUT提醒指示客户端执行此用户交互。提醒至少包含两个Item。

* The first Item contains optional parameters as specified in Section 2.5.3.<br/>
第一个Item包含第2.5.3节中指定的可选参数
* The second Item has exactly one Data element containing the text to be displayed to the user.<br/>
第二个Item正好有一个Data元素，其中包含要显示给用户的文本。

Example: 范例
```
<Alert>
  <CmdID>2</CmdID>
  <Data>1102</Data>
  <Item></Item>
  <Item>
    <Data>Type in the name of the service you would like to configure</Data>
  </Item>
</Alert>
```
The user is presented with the text and an input box to type in the message. The following Status message is sent back in the next message from client to server:<br/>
向用户显示文本和输入框以输入消息。以下状态消息在客户端到服务器的下一个消息中发回：
```
<Status>
  <MsgRef>1</MsgRef>
  <CmdRef>2</CmdRef>
  <Cmd>Alert</Cmd>
  <Data>200</Data> <!-- Successful, user typed in a text -->
  <Item>
     <Data>CNN</Data> <!-- User input -->
  </Item>
</Status>
```
## 2.5.2.4 User choice 用户输入
When this Alert is sent, the user is presented with a set of possible choices. The Alert body MUST contain the following Items.<br/>
当发送此提醒时，向用户呈现一组可能的选择。提醒主体必须包含以下项目。
* The first Item contains optional parameters as specified in Section 2.5.3.<br/>
第一个Item包含第2.5.3节中指定的可选参数
* The second Item has exactly one Data element containing the title of the selection as plain text.<br/>
第二个Item只有一个Data元素，其中包含作为纯文本的选择标题。
* From third Item onwards the Item contains exactly one Data element that describes one possible choice as plain text. These Items are referenced by a number starting from 1. Items MUST be numbered in the order they were sent. Items SHOULD be presented to the user in the order they were sent.<br/>
从第三个Item开始，项目正好包含一个纯文本描述做为一个可能的选择的Data元素。这些Item由从1开始的数字引用。Item必须按照它们发送的顺序编号。推荐将Item按照发送的顺序呈现给用户。

The user selection is returned in Status message. The selected item is returned in an Item. The Data element of this Item contains the reference number of item. A variation of this Alert allows the user to select multiple items. In this case selected items are sent back in multiple Items in the same way as one selected item.<br/>
用户的选择在Status消息中返回。所选项目在Item中返回。此Item的Data元素包含项的引用号。此提醒的变体允许用户选择多个项目。在这种情况下，所选项目以与一个所选项目相同的方式在多个Item中返回。

One possible implementation could be a list and each Data member of the Alert could be displayed as a row in the list. The user could select a list item then he or she would push the "Ok" button and the ID of the selected list item is sent back in a Status message.<br/>
一个可能的实现可以是列表，并且提醒的每个Data成员可以在列表中显示为一行。用户可以选择列表项目，然后他或她将点击“确定”按钮，并且在状态消息中发回所选择的列表项目的ID。

Example for a single-choice Alert: 单选提醒示例：
```
<Alert>
  <CmdID>2</CmdID>
  <Data>1103</Data> 
  <Item><Data>MINDT=10</Data></Item>
  <Item>
    <Data>Select service to configure</Data> 
  </Item>
  <Item>
     <Data>CNN</Data>
  </Item>
  <Item>
     <Data>Mobilbank</Data>
  </Item>
  <Item>
     <Data>Game Channel</Data>
  </Item>
</Alert>
```
Response to this Alert returns the selected item. <br/>
对此提醒的响应将返回所选项目。
```
<Status>
  <MsgRef>1</MsgRef>
  <CmdRef>2</CmdRef>
  <Cmd>Alert</Cmd>
  <Data>200</Data> <!-- Successful, user selected an item -->
  <Item>
    <Data>2</Data> <!-- User selected MobilBank -->
  </Item>
</Status>
```
Example to multiple-choice Alert<br/>
多选项提醒的示例
```
<Alert>
  <CmdID>2</CmdID>
  <Data>1104</Data>
  <Item></Item>
  <Item><Data>Select service to configure</Data></Item> 
  <Item>
     <Data>CNN</Data>
  </Item>
  <Item>
     <Data>Mobilbank</Data>
  </Item>
  <Item>
    <Data>Game Channel</Data>
  </Item>
</Alert>
```
Response to this Alert returns the selected item. The number of the selected items can be returned in arbitrary order by the client.<br/>
对此提醒的响应将返回所选项目。所选项目的数量可以由客户端以任意顺序返回。
```
<Status>
  <MsgRef>1</MsgRef>
  <CmdRef>2</CmdRef>
  <Cmd>Alert</Cmd>
  <Data>200</Data> <!-- Successful, user selected an item --> 
  <Item>
     <Data>3</Data>
  </Item>
  <Item>
    <Data>2</Data> <!-- User selected Mobilbank and Game Channel -->
  </Item>
</Status>
```