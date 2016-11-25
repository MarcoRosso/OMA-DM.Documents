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
## 2.5.2.5 Progress notification (object download) 进度通知（对象下载）
Users SHOULD be able to track the progress of a longer management operation like a file or object download. OMA Device Management Protocol will not provide a separate mechanism for progress notification but it will entirely reuse the SyncML Size Meta-Information tag defined in SyncML Meta-Information DTD [META] and will make a recommendation for device manufacturers to use this tag for displaying progress notification.<br/>
推荐用户能够跟踪较长的管理操作（如文件或对象下载）的进度。OMA设备管理协议不会为进度通知提供单独的机制，但它将完全重用SyncML元信息DTD[META]中定义的SyncML大小元信息标签，并且将建议设备制造商使用此标签显示进度通知。

According to SyncML Meta-Information DTD, any Item can be tagged by Size meta-information that indicates the size of the object. When the device encounters a Size meta-information tag in a received Item, it MAY display a progress notification on the user interface if the device decides that the item with the given size will take a longer time to download. The progress notification bar is scaled according to the length information conveyed in the Size element. If the size information is not sent by the server, the client is not able to display a scaled progress bar so it is recommended that servers send this information if the object to be downloaded by the client is reasonably large.<br/>
根据SyncML元信息DTD，任何Item可以由指示对象的大小的Size元信息来标记。当设备在所接收的项目中遇到Size元信息标签时，如果设备确定具有给定大小的项目将花费较长时间下载，则其可以在用户界面上显示进度通知。进度通知栏根据Size元素中传达的长度信息进行缩放。如果服务器未发送大小信息，则客户端无法显示缩放的进度条，因此如果客户端要下载的对象相当大，建议服务器发送此信息。

Example of an antivirus data file download with Size Meta Information.
使用Size元信息下载防病毒数据文件的示例。
```
<Add>
  <CmdID>2</CmdID>
  <Meta>
  <Format xmlns="syncml:metinf">b64</Format> 
  <Type xmlns="syncml:metinf">
      application/antivirus-inc.virusdef </Type>
  </Meta>
  <Item>
    <Meta>
      <!-- Size of the data item to download --> 
      <Size xmlns='syncml:metinf'>37214</Size>
      </Meta>
      <Target><LocURI>./antivirus_data</LocURI></Target>
      <Data>
      <!-- Base64-coded antivirus file -->
      </Data>
  </Item>
</Add>
```
Progress indicator will be displayed during the execution of the Add command and it will be scaled so that the total length of data to be downloaded is supposed to be 37214 bytes.<br/>
在执行添加命令期间将显示进度指示器，并且它将被缩放，要下载的数据的总长度应为37214字节。
## 2.5.3 User interaction options 用户交互选项
Alert's MAY have optional User interaction parameters in the first Item. Optional parameters are represented as one text string inside the Data element. If the User interaction Alert does not have optional parameters, the first Item is empty. The optional parameter string conforms to the URL encoding format specified in [RFC2396].<br/>
提醒可以在第一个Item中有可选的用户交互参数。可选参数在Data元素中表示为一个文本字符串。 如果用户交互警报没有可选参数，则第一个项目为空。可选参数字符串符合[RFC2396]中指定的URL编码格式。

The following example uses two optional parameters:<br/>
以下示例使用两个可选参数：

 `MAXDT=30&DR=1`
 
 The client MUST skip without error message all the optional parameters that it is not able to process. <br/>
 客户端必须没有错误消息地跳过它不能处理所有可选参数。
 
 The following optional parameters are currently defined.<br/>
 以下可选参数当前已定义。
 
 ### 2.5.3.1 MINDT (Minimum Display Time) 最小显示时间
This parameter is a hint to the user agent of the minimum time that the user interaction should be displayed to the user. This can be important to guarantee that a notification message is readable.<br/>
此参数是向用户代理提示用户交互应显示给用户的最短时间的提示。这对于保证通知消息可读的是重要的。

MINDT parameter MUST have a value that can be evaluated as a positive, integer number. Value of MINDT is interpreted as notification display time to user in seconds.<br/>
MINDT参数必须有一个可以作为正整数计算的值。MINDT的值被解释为用户的通知显示时间的秒数。

Example: 范例：
```
<!-- Display this message for at least 10 seconds -->
<Item><Data>MINDT=10</Data></Item>
```
 ### 2.5.3.2 MAXDT (Maximum Display Time) 最大显示时间
 This parameter is a hint to the user agent for how long the client should wait for the user to execute the user interaction. If the user does not act within MAXDT time, the action is considered to be cancelled and a timeout status package or default response package is sent back to the server.<br/>
此参数提示用户代理客户端应等待用户执行用户交互的时间。如果用户在MAXDT时间内没有动作，则认为该操作被取消，并且超时状态包或默认响应包被发送回服务器。

MAXDT parameter MUST have a value that can be evaluated as a positive, integer number. Value of MAXDT is interpreted as seconds to wait for user action.<br/>
MAXDT参数必须有一个可以作为正整数计算的值。MAXDT的值被解释为等待用户操作的秒数。

Example: 范例：
```
<!-- Wait maximum 20 seconds for the user --> <Item>
<Data>MAXDT=20</Data></Item>
```
 ### 2.5.3.3 DR (Default Response) 默认响应
 DR optional parameter specifies the initial state of the user interaction control widget. Other than setting the initial state of the user interaction control widget, DR has no other influence on the user interaction control widget. Interpretation for different user interaction types is the following:<br/>
DR可选参数指定用户交互控件窗口小部件的初始状态。除了设置用户交互控件小部件的初始状态之外，DR对用户交互控件小部件没有其他影响。不同用户交互类型的解释如下：

* If the user interaction is Notification, this optional parameter is ignored.<br/>
如果用户交互是通知，则忽略此可选参数。
* If the user interaction is a confirmation, 0 means that the reject user interface element is highlighted by default, 1 means that the accept user interface element is highlighted by default. Highlighted user interface element means that the "default" user interaction (like pressing Enter button) will select the highlighted user interface element. If the client user interface has no notion of highlighted user interface element, this parameter MAY be ignored.<br/>
如果用户交互是确认，0表示拒绝用户界面元素默认突出显示，1表示默认情况下突出显示接受用户界面元素。突出显示的用户界面元素意味着“默认”用户交互（如按Enter按钮）将选择突出显示的用户界面元素。如果客户端用户界面没有突出显示的用户界面元素的概念，则可以忽略此参数。

* If the user interaction is user input, DR value specifies the original text in the text input user interface element. This text MUST conform to the optional parameter syntax rules.<br/>
如果用户交互是用户输入，DR值指定文本输入用户界面元素中的原始文本。此文本必须符合可选参数语法规则。
* If the user interaction is single-choice, the DR value is the originally highlighted choice item; e.g. value between 1 and the number of items in the selection list.<br/>
如果用户交互是单选项，则DR值是原始突出显示的选项项目；例如值介于1和选择列表中的项目数之间。
* If the user interaction is a multi-choice, the DR value is a minus sign-separated list of originally highlighted values (for example: 2-3).<br/>
* 如果用户交互是多选项，则DR值是以原始高亮显示的值的减号分隔列表（例如：2-3）。
例子：

Examples: 范例：
```
<!-- Accept by default in a Confirmation action --> 
<Item><Data>DR=1</Data></Item>

```
```
<!-- Default user entry of "John Doe" in an user input action --> 
<Item><Data>DR=John+Doe</Data></Item>
```
```
<!-- Default selection of item 3 in a single-choice action --> 
<Item><Data>DR=3</Data></Item>
```
```
<!-- Default selection of item 2 and 3 in a multi-choice action -->
<Item><Data>DR=2-3</Data></Item>
```
 ### 2.5.3.4 MAXLEN (Maximum length of user input)  最大用户输入长度
MAXLEN value is evaluated to a positive integer and determines the maximum number of characters that can be typed into the text input user interaction widget. The optional parameter MUST be ignored in all other kind of user interaction widget. If the specified maximum length of input string exceeds the capability of the client, the client MAY ignore the parameter.<br/>
MAXLEN值为正整数，其代表可以输入到文本输入用户交互窗口小部件的最大字符数。必须在所有其他类型的用户交互窗口小部件中忽略可选参数。如果指定的输入字符串的最大长度超过客户端的能力，则客户端可以忽略该参数。

Examples: 范例：
```
<!-- Maximum string length is 30 --> 
<Item><Data>MAXLEN=30</Data></Item>
```
 ### 2.5.3.5 IT (Input Type) 输入类型
IT specifies what kind of characters are allowed in the text input user interaction widget. Based on this information a client with limited keyboard MAY display user interaction elements that allow easy input of characters not present on the keyboard. The optional parameter MUST be ignored in user interaction widgets other than text input. Allowed values:<br/>
IT指定在文本输入用户交互窗口小部件中允许使用什么样的字符。基于该信息，具有有限键盘的客户端可以显示允许输入不存在于键盘上的字符的用户交互元件。在用户交互窗口小部件中，除了文本输入之外，必须忽略可选参数。允许值：

IT=A - Alphanumeric input, client SHOULD allow input of all alphanumeric characters. This is the default behaviour.<br/> 
IT = A - 字母数字输入，客户端应允许输入所有字母数字字符。这是默认行为。 

IT=N - Numeric input, client SHOULD allow input of all numeric characters, decimal point and sign character.<br/>
IT = N - 数字输入，客户端应允许输入所有数字字符，小数点和符号字符。

IT=D - Date input, client SHOULD allow input of all numeric characters. User input is delivered to server in following text string format "DDMMYYYY", where;<br/>
IT = D - 日期输入，客户端应该允许输入所有数字字符。用户输入以以下文本字符串格式“DDMMYYYY”传递到服务器，其中;
  * DD is day with possible leading zero.<br/>
  DD是第一位可能为零的日期。
  * MM is month with possible leading zero.<br/>
  MM是第一位可能为零的月份。
  * YYYY is year presented with four digits.<br/>
  YYYY年份提供四位数字。
  
IT=T - Time input, client SHOULD allow input of all numeric characters. User input is delivered to server in following text string format "hhmmss", where;<br/>
IT = T - 时间输入，客户端应允许输入所有数字字符。用户输入以下面的文本字符串格式“hhmmss”传递到服务器，其中;

* hh is hours with possible leading zero.<br/>
hh是第一位可能为零的小时。
* mm is minutes with possible leading zero.<br/>
mm是第一位可能为零的分钟。
* ss is seconds with possible leading zero.<br/>
ss是第一位可能为零的秒数。

IT=P - Phone number input, client SHOULD allow input of all numeric characters, "+", "p", "w" and "s". "+" MUST be first if present in phone number.<br/>
IT = P - 电话号码输入，客户端应允许输入所有数字字符，“+”，“p”，“w”和“s”。 “+”必须是第一，如果存在于电话号码。

IT=I - IP address input, client SHOULD allow input of all numeric characters. User input is delivered to server in following text string format "xxx.yyy.zzz.www"<br/>
IT = I - IP地址输入，客户端应允许输入所有数字字符。用户输入以以下文本字符串格式“xxx.yyy.zzz.www”传送到服务器

Examples: 范例：
```
<!-- Numeric text input -->
<Item><Data>IT=N</Data></Item>
```
Status message delivered to server as response<br/>
Status消息作为响应传递到服务器
```
<Status>
  <MsgRef>1</MsgRef>
  <CmdRef>2</CmdRef>
  <Cmd>Alert</Cmd>
  <Data>200</Data> <!-- Successful, entered a number --> 
  <Item>
     <Data>-1.23</Data>
  </Item>
</Status>
```
 ### 2.5.3.6 ET (Echo Type) 回声类型
ET specifies how text input user interaction widget echoes the characters that the user types in. The optional parameter MUST be ignored in user interaction widgets other than text input. Allowed values:<br/>
ET指定文本输入用户交互窗口小部件如何回显用户键入的字符。可选参数必须在用户交互窗口小部件而不是文本输入中被忽略。 允许值：

ET=T - Text input. The client SHOULD allow the user to see the character the user typed into the text input user interaction widget. This is the default behaviour.<br/>
ET = T - 文本输入。客户端应该允许用户看到用户键入到文本输入用户交互小部件中的字符。 这是默认行为。

ET=P - Password input. The client SHOULD hide the character the user typed into the text input user interaction widget. One way of doing it MAY be writing an asterisk instead of the character itself.<br/>
ET = P - 密码输入。客户端应该隐藏用户键入到文本输入用户交互窗口小部件中的字符。一种方法是写一个星号而不是字符本身。

Examples: 范例：
```
<!-- Numeric text input -->
<Item><Data>ET=T</Data></Item>
```

