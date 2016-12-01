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
### 6.2.2.1 Trigger Message

The `<trigger-message>` field specifies the message causing the client to connect to the server.<br/>
<trigger-message>字段指定使客户端连接到服务器的消息。

### 6.2.2.2 Digest
The `<digest>` field specifies the MD5 Digest authentication. The Digest is computed as Digest = H(B64(H(server- identifier:password)):nonce:B64(H(trigger))). Length of MD5 Digest is 128 bits.<br/>
`<digest>`字段指定MD5摘要认证。Digest计算为Digest = H(B64(H(server- identifier:password)):nonce:B64(H(trigger)))。MD5摘要的长度为128位。