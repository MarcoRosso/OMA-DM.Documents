# 6.2 Structure of General Notification Initiated Session Alert 一般通知启动会话提醒的结构

General Package#0 is the default format used for the Notification Initiated Session Trigger Message. This default format can be used if this document does not describe a special format for initialization purposes.<br/>
通用包＃0是用于通知发起的会话触发消息的默认格式。如果本文档没有为初始化目的描述特殊格式，则可以使用此默认格式。

The following figure describes the format of the General Package #0.<br/>
下图描述了通用包＃0的格式。

![](6.2.jpeg)
The MIME type for the General Notification Initiated Session Alert message is application/vnd.syncml.notification and the Content-Type code for that is 0x44. Byte order for General Notification Initiated Session Alert message is Big Endian (Network order).<br/>
通用通知发起的会话警报消息的MIME类型为application/vnd.syncml.notification，而Content-Type代码为0x44。 一般通知发起的警报消息的会话的字节顺序是大端序（网络顺序）。

## 6.2.1 Syntax for the Initiation Notification 启动通知的语法
The following ABNF [RFC2234] defines the syntax for the message. The order and the size of the fields MUST be same as specified in the following syntax of the Trigger Message.<br/>
以下ABNF [RFC2234]定义消息的语法。字段的顺序和大小必须与触发消息的以下语法中指定的相同。
```
<trigger-message> ::= <digest><trigger>
<digest> ::= 128*BIT                               ; ‘MD5 Digest value’
<trigger> ::= <trigger-hdr><trigger-body>
<trigger-hdr> ::= <version><ui-mode><initiator><future-use> 
                  <sessionid><length-identifier><server-identifier>
<version> ::= 10*BIT                               ; ‘Device Management Version’
<ui-mode> ::= <not-specified> / <background> /     ;‘Background/Informative/
               <informative> / <user-interaction>  ; User Interaction session’
<not-specified> ::= “00”                           ; ‘2*bit value “0”’
<background> ::= “01”                              ; ‘2*bit value “1”’
<informative> ::= “10”                             ; ‘2*bit value “2”'
<user-interaction> ::= “11”                        ; ‘2*bit value “3”’
<initiator> ::= <client> / <server>                ; ‘Server/User initiated’
<client> ::= “0”                                   ; ‘1*bit value “0”’ 
<server> ::= “1”                                   ; ‘1*bit value “1”’
<future-use> ::= 27*BIT                            ; ‘Reserved for future DM use’
<sessionid> ::= 16*BIT                             ; ‘Session identifier’
<length-identifier> ::= 8*BIT                      ; ‘Server Identifier length’
<server-identifier> ::= <length-identifier>*CHAR   ; ‘Server Identifier’

<trigger-body> ::= [<vendor-specific>]
<vendor-specific> ::= n*BIT                        ; ‘Optional vendor specific info’
```  

## 6.2.2 Description of the fields 字段说明
### 6.2.2.1 Trigger Message 触发消息

The `<trigger-message>` field specifies the message causing the client to connect to the server.<br/>
<trigger-message>字段指定使客户端连接到服务器的消息。

### 6.2.2.2 Digest 摘要
The `<digest>` field specifies the MD5 Digest authentication. The Digest is computed as Digest = H(B64(H(server- identifier:password)):nonce:B64(H(trigger))). Length of MD5 Digest is 128 bits.<br/>
`<digest>`字段指定MD5摘要认证。Digest计算为Digest = H(B64(H(server- identifier:password)):nonce:B64(H(trigger)))。MD5摘要的长度为128位。

### 6.2.2.3 Trigger 触发
The `<trigger>` field is container for the trigger-hdr and trigger-body fields.<br/>
`<trigger>`字段是trigger-hdr和trigger-body字段的容器。

### 6.2.2.4 Header of the Trigger Message 触发消息的标题
The `<trigger-hdr>` field specifies the header of the Trigger Message.
`<trigger-hdr>`字段指定触发消息的标题。

### 6.2.2.5 Body of the Trigger Message 触发消息的主体
The `<trigger-body>` field specifies the body of the Trigger Message.
`<trigger-body>`字段指定触发消息的主体。

### 6.2.2.6 Version Information 版本信息
The `<version>` field specifies the version of the OMA Device Management Notification message sent by the OMA DM server. This value is specified by using the 10 bits in the Trigger Message. The supported version is counted as `<notification message version> = DEC (version)/10`, i.e. first the bit value is transferred to the numeric and then divided by ten. Therefore the biggest possible version is ‘102.3’ and the version ‘1.0’ is specified as ‘0000001010’.<br/>

`<version>`字段指定由OMA DM服务器发送的OMA设备管理通知消息的版本。 该值通过使用触发消息中的10位来指定。 支持的版本计数为`<notification message version> = DEC（version）/10`，即首先将位值传输到数字，然后除以十。因此，最大可能的版本是“102.3”，版本“1.0”被指定为“0000001010”。

Notification messages conforming to this version of the specification MUST have <version> field 10-bit binary value ‘0000001011’.<br/>
符合此版本规范的通知消息必须具有`<version>`字段10位二进制值“0000001011”。

### 6.2.2.7 User Interaction Mode 用户交互模式
The `<ui-mode>` field specifies the server recommendations whether the server wants the management session to be executed in background or show a notification to the user. A client SHOULD follow this recommendation.<br/>
`<ui-mode>`字段指定服务器建议，即服务器是否希望在后台执行管理会话，或向用户显示通知。客户端应该遵循此建议。

The values the User Interaction mode can have:<br/>
用户交互模式可以具有的值：

* Not specified – The `<not-specified>` field in `<user-interaction>` field specifies that the server doesn’t have a recommendation to this element. This value is specified by using the 2 bits and the bit value for not specified action is “00”.<br/>
未指定 - `<user-interaction>`字段中的`<not-specified>`字段指定服务器没有对此元素的建议。该值由2位指定，未指定动作的位值为“00”。

* Background management action – The `<background>` field specifies that the server recommends the management action SHOULD be done as a background event. This value is specified by using the 2 bits and the bit value for background action is “01”.<br/>
后台管理操作 - `<background>`字段指定服务器建议管理操作应作为后台事件完成。该值由2位指定，背景操作的位值为“01”。

* Informative management action – The `<informative>` field specifies that the server recommends the client to display an informative notification or maybe emitting a beep sound announcing the beginning of the provisioning session to the device user. This value is specified by using the 2 bits and the bit value for informative notification is “10”.<br/>
信息性管理行动 - `<informative>`字段指定服务器建议客户端显示信息性通知，或者可能向设备用户发出通知配置会话开始的嘟嘟声。该值由2位指定，信息通知的位值为“10”。

* User Interaction before the management action – The `<user-interaction>` field specifies that the server recommends the client to prompt the device user for acceptance of the offered management session before the management session takes place. This value is specified by using the 2 bits and the bit value for user displayable notification is “11”.<br/>
管理操作之前的用户交互 - `<user-interaction>`字段指定服务器建议客户端在管理会话发生之前提示设备用户接受所提供的管理会话。该值由2位指定，用户可显示通知的位值为“11”。

### 6.2.2.8 Initiator of the Management Action 管理行动的发起人
The `<initiator>` field specifies how the server has interpreted the initiation of the management action, either because the end user requested it or because the server has management actions to perform. A client SHOULD follow this recommendation.<br/>
`<initiator>`字段指定服务器如何解释管理操作的启动，因为最终用户请求它或者因为服务器有管理操作要执行。客户端应该遵循此建议。

The values the Initiator of the Management action can have:<br/>
管理行动发起人可以具有的价值：

* Client (End User) Initiated management action – The `<client>` field specifies that the end user caused the device management session to start. This value is specified by using 1 bit and the bit value for end user initiated management session is “0”.
客户端（最终用户）启动的管理操作 - `<client>`字段指定最终用户启动设备管理会话。该值由1位指定，最终用户发起的管理会话的位值为“0”。

* Server Initiated management action – The `<server>` field specifies that the server (operator, enterprise) caused the device management session to start. This value is specified by using 1 bit and the bit value for Server initiated management session is “1”.<br/>
服务器启动的管理操作 - `<server>`字段指定服务器（操作员，企业）导致设备管理会话启动。此值使用1位指定，服务器启动的管理会话的位值为“1”。

The `<client>` and `<server>` values do not convey any information related to “sync type” (for more information about Sync Types see the SyncML Synchronization protocol document [SYNCPRO] for details of Sync Types).<br/>
<client>和<server>值不传达任何与“同步类型”相关的信息（有关同步类型的更多信息，请参阅SyncML同步协议文档[SYNCPRO]了解同步类型的详细信息）。

### 6.2.2.9 Future Use of the Device Management 设备管理的未来使用
The `<future-use>` field is reserved for the future fields for OMA Device Management. The reserved space is 27 bits long and the bit value for bits not yet in use MUST be “0”.<br/>
`<future-use`>字段保留用于OMA设备管理的未来使用。保留空间为27位长，未使用位的位值必须为“0”。

### 6.2.2.10 Session Identifier 会话标识符
The <sessionid> field specifies the identifier of the OMA DM session associated with the DM Message. This value is specified by using the 16 bits in the Trigger Message. The Session ID MUST be different between different management session Trigger Messages and the Client MUST use this Session ID when it connects to the OMA DM Server. If the server triggers the same management session several times, it is RECOMMENDED that the same Session ID be used. If client receives the same Session ID several times it is enough for a client to initiate only one management session.<br/>
`<sessionid>`字段指定与DM消息相关联的OMA DM会话的标识符。该值通过使用触发消息中的16位来指定。不同的管理会话触发消息的会话ID必须不同，并且客户端在连接到OMA DM服务器时必须使用该会话ID。如果服务器多次触发相同的管理会话，则建议使用相同的会话ID。如果客户端多次接收到相同的会话ID，则客户端只启动一个管理会话就足够了。

When preparing the OMA DM Message for connection to the DM server, the binary session ID value from the trigger message, in the unsigned hexadecimal range of 1 through FFFF, SHALL be mapped to a string of hexadecimal digits (chosen from the numeric digits “0”-“9” and the upper-case letters “A”-“F”) of between one and four characters in length, inclusive, and placed in the SessionID element of the OMA DM message. Leading zeros MUST NOT be included.<br/>
当准备用于连接到DM服务器的OMA DM消息时，触发消息中的二进制会话ID值（在无符号十六进制范围1到FFFF中）应映射到一串十六进制数字（从数字“0“-”9“和大写字母”A“-”F“），该数字长度在一个和四个字符之间，并放置在OMA DM消息的SessionID元素中。前导零必须不包括在内。

### 6.2.2.11 Length of the Identifier 标识符的长度
The `<length-identifier>` field specifies the length of the Server Identifier of the management server. The value of the Length Identifier is counted as Length of the server-identifier = DEC (length-identifier).<br/>
`<length-identifier>`字段指定管理服务器的服务器标识符的长度。长度标识符的值被计数为server-identifier=DEC（length-identifier）的长度。

### 6.2.2.12 Server Identifier 服务器标识符
The `<server-identifier>` field specifies the Server Identifier of the management server. Length of `<server-identifier>` is specified in the `<length-identifier>` field.
`<server-identifier>`字段指定管理服务器的服务器标识符。 在`<length-identifier>`字段中指定`<server-identifier>`的长度。

### 6.2.2.13 Vendor Specific Information 供应商特定信息
可选的`<vendor specific>`字段用于指定供应商特定信息。该字段跟在`<server-identifier>`字段之后，触发消息大小的其余部分可以用供应商特定信息打包。

