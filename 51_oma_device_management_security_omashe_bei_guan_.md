# 5.1 OMA Device Management Security OMA设备管理安全
## 5.1.1 Credentials 凭证
Four examples of suitable credentials exchanged between Devices and Device Management servers are shown in the following list.<br/>
在设备和设备管理服务器之间交换的合适凭证的四个示例如以下列表所示。

1. A username (AAUTHNAME in [DMSTDOBJ]) that uniquely identifies the Device Management Server [DMTND] to a Device), a password (AAUTHSECRET in [DMSTDOBJ]) – to be coupled with the username, and a nonce (AAUTHDATA in [DMSTDOBJ]) – to prevent replay attacks where hashing algorithms are used with static data.<br/>
唯一标识设备的设备管理服务器[DMTND]的用户名（[DMSTDOBJ]中的AAUTHNAME），要与用户名相关联的密码（[DMSTDOBJ]中的AAUTHSECRET），以及随机数（AAUTHDATA， [DMSTDOBJ]） - 以防止重用攻击，其中散列算法与静态数据一起使用。

2. A username (AAUTHNAME in [DMSTDOBJ]) that identifies the Device to the Device Management Server), a password (AAUTHSECRET in [DMSTDOBJ]) – to be coupled with username, and a nonce (AAUTHDATA in [DMSTDOBJ]) – to prevent replay attacks where hashing algorithms are used with static data.<br/>
用于标识设备到设备管理服务器的用户名（[DMSTDOBJ]中的AAUTHNAME），要与用户名相关联的密码（[DMSTDOBJ]中的AAUTHSECRET）和随机数（[DMSTDOBJ]中的AAUTHDATA）一起使用防止重复攻击，其中散列算法与静态数据一起使用。

3. A certificate, as specified in [WAP-219-TLS]<br/>
[WAP-219-TLS]中规定的证书。

4. A network, transport or server specific mechanism, for example WAP.<br/>
网络，传输或服务器特定机制，例如WAP。

For the purpose of Server to Device authentication, if a username, password and nonce are used, the Server MUST use a different password for each client it serves, in order that a client (which possesses a shared secret based on this password) cannot pose effectively as this Server in a interaction with another client.<br/>
为了服务器到设备认证的目的，如果使用用户名，密码和随机数，则服务器务必对它所服务的每个客户端使用不同的密码，以便客户端（拥有基于该密码的共享密钥）不能有效地建立作为此服务器与另一客户端的交互。

## 5.1.2 Initial Provisioning of Credentials 凭证的初始设置
The initial provisioning of the credentials for a Server, so that the Device may be capable of authenticating a specific Device Management Server, is documented in [DMBOOT]. However, other techniques outside of these specifications are not excluded.<br/>
[DMBOOT]中记录了服务器的凭证的初始配置，以便设备能够验证特定设备管理服务器。然而，不排除这些规格之外的其他技术。

Essentially, any suitable technique will deliver at least the bare minimum of information required to establish the DM session. This, of course, includes the Server credential and the Device credential.<br/>
基本上，任何合适的技术将至少递送建立DM会话所需的最少的信息。这当然包括服务器凭据和设备凭证。

## 5.1.3 Authentication 认证

Both OMA DM Protocol [DMPRO] client and Server MUST be authenticated to each other. Authentication can be performed at different layers. OMA DM servers MUST support both client and Server authentication at the transport layer. OMA DM Servers MUST request client authentication at the transport layer when transport layer security is requested by the OMA DM client during session establishment. Some clients may not support transport-layer client authentication. Servers MUST authenticate such clients at the application layer. If the transport layer does not have a sufficiently strong authentication feature, OMA DM Protocol layer authentication MUST be used.<br/>
OMA DM协议的[DMPRO]客户端和服务器必须彼此认证。认证可以在不同的层执行。OMA DM服务器必须在传输层支持客户端和服务器认证。当会话建立期间OMA DM客户端请求传输层安全时，OMA DM服务器必须在传输层请求客户端认证。某些客户端可能不支持传输层客户端认证。服务器必须在应用层验证这样的客户端。如果传输层不具有足够强的认证特征，则必须使用OMA DM协议层认证。

Either the client or the Server MAY send credentials to each other or challenge the other to send them.<br/>
客户端或服务器可能会向彼此发送凭据或质疑另一方发送凭据。

OMA DM clients that do not support client authentication at the transport layer MUST support OMA DM syncml:auth-md5 type authentication. OMA DM clients that support mutual authentication at the transport layer MAY support OMA DM authentication mechanisms such as the syncml:auth-md5 type.The DM Server MAY still issue a MD5 challenge when transport layer mutual authentication has already been completed but the session MUST be terminated if the client does not respond with the requested authentication type. The provisioning of credentials/certificates for transport layer authentication is beyond the scope of OMA DM Security.<br/>
在传输层不支持客户端认证的OMA DM客户端必须支持OMA DM syncml：auth-md5类型认证。支持传输层相互认证的OMA DM客户端可以支持OMA DM认证机制，例如syncml：auth-md5类型。当传输层相互认证已经完成但是如果客户端没有使用请求的认证类型进行响应，则会话必须终止。传输层认证的凭据/证书的配置超出了OMA DM安全性的范围。

It is assumed that OMA DM Protocol will often be used on top of a transport protocol that offers session layer authentication so that authentication credentials are exchanged only at the beginning of the session (like in TLS or WTLS). If the transport layer is not able to provide session authentication, however, each request and response MUST be authenticated.
假设OMA DM协议将经常在提供会话层认证的传输协议之上使用，则认证证书交换仅在会话开始时（例如在TLS或WTLS中）进行。然而，如果传输层不能提供会话认证，则必须认证每个请求和响应。

## 5.1.3.1 MD-5 authentication in OMA DM OMA DM中的MD-5认证
MD-5 authentication [RFC1321] works by supplying primitive userid:password in the Cred element of the SyncHdr as shown below.<br/>
MD-5认证[RFC1321]通过在SyncHdr的Cred元素中提供原始userid：password来工作，如下所示。
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
    <VerDTD>1.2</VerDTD>
    <VerProto>DM/1.2</VerProto>
    <SessionID>1</SessionID>
    <MsgID>1</MsgID>
    <Target> 
        <LocURI>http://www.syncml.org/mgmt-server</LocURI>
    </Target>
    <Source>
        <LocURI>IMEI:493005100592800</LocURI>
        <LocName>Bruce1</LocName> <!-— userid --> 
    </Source>
    <Cred>
    <Meta>
      <Type xmlns="syncml:metinf">syncml:auth-md5</Type> 
      <Format xmlns=”syncml:metinf”>b64</Format>
    </Meta>
    <Data>18EA3F......</Data>
          <!-- base64 formatting of MD-5 Digest -->
    </Cred>
    <Meta>
        <MaxMsgSize xmlns="syncml:metinf">5000</MaxMsgSize>
    </Meta>
  </SyncHdr>
         <!—- regular body information here -->
  <SyncBody>
  </SyncBody>
</SyncML>
```
## 5.1.3.2 Computation of the MD-5 Digest 计算MD-5摘要
The digest supplied in the Cred element is computed as follows: 
在Cred元素中提供的摘要计算如下：

Let H = the MD5 Hashing function.<br/>
令H = MD5哈希函数。

Let Digest = the output of the MD5 Hashing function. <br/>
令Digest = MD5哈希函数的输出。

Let B64 = the base64 encoding function.<br/>
令B64 = base64编码函数。

Digest = H(B64(H(username:password)):nonce)

This computation allows the authenticator to authenticate without having knowledge of the password. The password is neither sent as part of the Cred element, nor is it required to be known explicitly by the authenticator, since the authenticator need only store a pre-computed hash of the username:password string.
此计算允许认证者在不知道密码的情况下进行认证。 码既不作为Cred元素的一部分发送，也不需要由认证者明确地知道，因为认证者仅需要存储username：password字符串的预先计算的散列。

## 5.1.3.3 Password and nonce usage 密码和随机数使用

Both password and nonce are RECOMMENDED to be at least 128 bits (16 random octets) in length.<br/>
密码和随机数都推荐为至少128位（16个随机字节）长度。

The nonce value MUST be issued in a challenge from either the Device or the Device Management Server. In the case of the credentials being sent prior to a challenge being issued, then the last nonce used shall be reused. The authenticator must be aware that the issuer of the credentials may be using a stale nonce (that is to say, a nonce that is invalid due to some previous communications failure or a loss of data). Because of this, if authentication fails, one more challenge, along with the supply of a new nonce, MUST be made.<br/>
必须在来自设备或设备管理服务器的质询中发出随机数。 在证书在发出质询之前发送的情况下，所使用的最后一个随机数将被重用。认证者必须知道凭证的发行者可能使用过时的随机数（也就是说，由于某些先前的通信故障或数据丢失）。因此，如果认证失败，必须进行另一个质询以及提供新的随机数。

A new nonce SHOULD be used for each new session. The sequence of nonce values (as seen across sessions) SHOULD be difficult to predict.<br/>
推荐为每个新会话使用新的随机数。推荐使随机数值序列（如会话中看到的）很难预测。

## 5.1.3.4 Challenges from non-authenticated agents 来自未认证代理的质询
In some scenarios, it might be necessary for client and Server to accept challenges from agents that have not yet been successfully authenticated. For example, consider the case in which both client and Server have outdated nonces, and MD5 or HMAC authentication is used. If they both discard the Chal element, they will not have a chance to update their nonce and they will never be able to authenticate each other. To avoid this situation it is RECOMMENDED that client and Server use the latest received nonce to build the content of the Cred element, even when the nonce is received from a non- authenticated agent. It is also RECOMMENDED that client and Server do not over-write the stored copy of the next nonce with one received from a non-authenticated agent, as that would allow malicious agents to replace good nonces with bad ones.<br/>
在某些情况下，客户端和服务器可能需要接受来自尚未成功验证的代理的挑战。 例如，考虑客户端和服务器都具有过时的随机数，并且使用MD5或HMAC认证的情况。 如果他们都抛弃Chal元素，他们将没有机会更新其随机数，他们将永远不能够彼此认证。为了避免这种情况，建议客户端和服务器使用最新接收的随机数来构建Cred元素的内容，即使当从非认证代理接收到随机数时。还建议客户端和服务器不用从未认证代理接收的一个随机数的覆盖下一个随机数的存储副本，因为这将允许恶意代理用坏的随机数代替好的随机数。

## 5.1.4 Integrity 完整性
Integrity of OMA DM messages is achieved using a HMAC-MD5 [RFC2104].<br/>
OMA DM消息的完整性使用HMAC-MD5[RFC2104]来实现。

This is a Hashed Message Authentication Code that MUST be used on every message transferred between the Device and the Device Management Server (if requested to do so by either entity). The use of integrity checking is OPTIONAL.
这是一个散列消息认证码，必须用于在设备和设备管理服务器之间传输的每个消息（如果任一实体请求这样做）。使用完整性检查是可选的。

### 5.1.4.1 How integrity checking is requested 如何请求完整性检查
Integrity checking is requested in the same way and at the same time as authentication challenges in [DMPRO]. A challenge issued for syncml:auth-MAC will use the same Meta data for Type, Format, and NextNonce as syncml:auth- md5. A new authentication type, syncml:auth-MAC, may be requested by either the client or the Device Management Server (or simply supplied prior to a challenge ever being issued). When used, this authentication type MUST be specified in the transport header and MUST NOT be specified using the Cred element.<br/>
完整性检查在[DMPRO]中以与身份验证相同的方式和相同的时间进行请求。 对syncml发出的质询：auth-MAC将对Type，Format和NextNonce使用与syncml：auth-md5相同的Meta数据。 新的认证类型syncml：auth-MAC可以由客户端或设备管理服务器请求（或者在发出质询之前简单地提供）。 使用时，必须在传输头中指定此认证类型，且必须不使用Cred元素指定。

Note that the recipient of a challenge MUST respond with the requested authentication type, else the session MUST be terminated. For example, a challenge requesting the HMAC engenders a reply with valid Basic Authentication credentials, the session will be terminated despite the validity of the authentication credentials that were actually supplied.<br/>
注意，质询的接收者必须用所请求的认证类型来响应，否则会话必须终止。例如，请求HMAC收到有效的基本认证凭证的答复的质询，尽管实际提供的认证凭证有效，会话仍将被终止。

### 5.1.4.2 How the HMAC is computed 如何计算HMAC
The HMAC is computed as described below, and uses MD-5 as its hashing function. The HMAC relies upon the use of a shared secret (or key), which in this application is itself a hash (denoted below as H(username:password)).<br/>
HMAC的计算如下所述，并且使用MD-5作为其散列函数。HMAC依赖于共享秘密（或密钥）的使用，在本应用中，共享秘密本身是哈希（以下表示为H(username:password)）。

The HMAC value MUST be computed by encoding in base64 the result of the digest algorithm applied as follows:<br/>
HMAC值必须通过在base64中编码，通过如下摘要算法来计算：

H(B64(H(username:password)):nonce:B64(H(message body)))<br/>

where H(X) is the result of the selected digest algorithm (MD-5) applied to octet stream X, and B64(Y) is the base64 encoding of the octet stream Y.<br/>
其中H（X）是应用于八位字节流X的所选择的摘要算法（MD-5）的结果，并且B64（Y）是八位字节流Y的base64编码。

### 5.1.4.3 How the HMAC is specified in the OMA DM message 如何在OMA DM消息中指定HMAC
The HMAC itself MUST be transported along with the original OMA DM message. This is achieved by inserting the HMAC into a transport header called x-syncml-hmac. This technique works identically on HTTP, WAP, and OBEX. The HMAC is calculated initially by the sender using the entire message body, either in binary form (WBXML) or text form (XML). The receiver applies the same technique to the incoming message.<br/>
HMAC本身必须与原始OMA DM消息一起传送。这是通过将HMAC插入到称为x-syncml-hmac的传输头中实现的。此技术在HTTP，WAP和OBEX上的工作原理相同。HMAC最初由发送方使用整个消息体（二进制形式（WBXML）或文本形式（XML））来计算。 接收方对输入消息应用相同的技术。

The header x-syncml-hmac contains multiple parameters, including the HMAC itself, the user or Server identifier, and an optional indication of which HMAC algorithm is in use (the only one currently defined is MD-5).<br/>
报头x-syncml-hmac包含多个参数，包括HMAC本身，用户或服务器标识符，以及使用哪个HMAC算法的可选指示（仅有一个当前定义的是MD-5）。

The value of the x-syncml-hmac header is defined as a comma separated list of attribute-values pairs. The rule "#rule" and the terms "token" and "quoted-string" are used in accordance to their definition in the HTTP 1.1 specifications [RFC2616].<br/>
x-syncml-hmac头的值定义为以逗号分隔的属性值对列表。 规则“#rule”和术语“token”和“quoted-string”根据它们在HTTP 1.1规范[RFC2616]中的定义使用。

Here is the formal definition:<br/>
这里是正式的定义：
`syncml-hmac = #syncml-hmac-param`<br/>

where:其中

`syncml-hmac-param = (algorithm | username | mac)`

The following parameters are defined:
定义以下参数：
```
algorithm = "algorithm" "=" ("MD5" | token)
username = "username" "=" username-value
mac = "mac" "=" mac-value
```
where:其中
```
username-value = quoted-string
mac-value = base64-string
```
The parameter algorithm can be omitted, in that case MD5 is assumed. The parameter username MUST be specified. The parameter mac MUST be specified.<br/>
可以省略参数algorithm，在这种情况下假定为MD5。必须指定参数username。必须指定参数mac。

Note that a base64-string is any concatenation of the characters belonging to the base64 Alphabet,as defined in [RFC1521].
注意，base64字符串是属于base64 Alphabet的字符的任何级联，如[RFC1521]中定义。

Example:范例
```
x-syncml-hmac: algorithm=MD5, username="Robert Jordan",
mac=NTI2OTJhMDAwNjYxODkwYmQ3NWUxN2RhN2ZmYmJlMzk
```
The username-value is the identical string from the LocName of the Source element of the SyncHdr, and represents the identity of the sender of the message. The presence of the username in the message header allows the calculation and validation of the HMAC to be independent of the parsing of the message itself.<br/>
username-value是来自SyncHdr的Source元素的LocName的相同字符串，并且表示消息的发送者的标识。在消息报头中存在的用户名允许HMAC的计算和验证独立于消息本身的解析。

Upon receiving a message, the steps are:<br/>
收到消息后，步骤如下：
1. Check for the HMAC in the message header; extract it and the username.<br/>
检查消息头中的HMAC; 提取它和用户名。
2. Using the username, look up the secret key from storage. This key is itself a hash, which incorporates the username and password, as described earlier.<br/>
使用用户名，从存储中查找密钥。 这个密钥本身是一个哈希，它包含用户名和密码，如前所述。
3. Either parse the message;<br/>
解析消息
4. Or, validate the digest.<br/>
或者，验证摘要

In either sequence of steps, the digest is calculated based on the entire message body, which is either a binary XML document (WBXML) or a text XML document.<br/>
在任一一步骤序列中，基于整个消息体来计算摘要，消息体是二进制XML文档（WBXML）或文本XML文档。
