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

After the HMAC is computed by the receiver (if it was present), the supplied HMAC and the computed HMAC can be compared in order to establish the authenticity of the sender, and also the integrity of the message.<br/>
在接收方计算HMAC（如果它存在）之后，可以比较所提供的HMAC和所计算的HMAC，以便建立发送者的真实性以及消息的完整性。

If the HMAC was expected (e.g. if a challenge for it had been issued) and either it or the userid are not supplied in the correct transport header, then an authentication failure results (as if they had been supplied, and were incorrect).<br/>
如果HMAC是预期的（例如，如果已经发出了对其的质询），并且它或者用户ID没有在正确的传输头中提供，则导致认证失败（正如它们已经被提供但是是不正确的）。

If the value of the username or secret is changed during a session (e.g. when the AAuthName or AAuthSecret element in [DMSTDOBJ] is replaced), the new value of secret will only be used for subsequent sessions.<br/>
如果在会话期间改变了用户名或密匙的值（例如，当[DMSTDOBJ]中的AAuthName或AAuthSecret元素被替换时），密匙的新值将仅用于后续会话。

Once the HMAC technique is used, it MUST be used for all subsequent messages until the end of the OMA DM session. The Status code sent back for the SyncHdr MUST be 200 to indicate authenticated for this message. In addition, the NextNonce element MUST be sent and used for the next HMAC credential check. Failure to meet these requirements MUST result in a termination of the session.<br/>
一旦使用HMAC技术，它必须用于所有后续消息，直到OMA DM会话结束。为SyncHdr发送回的状态码必须为200，以指示对此消息进行身份验证。此外，NextNonce元素必须被发送并用于下一个HMAC凭证检查。不能满足这些要求的会话必须终止。

### 5.1.4.4 HMAC and nonce value HMAC和随机数值
A new nonce MUST be used for every message. The new nonce will be obtained via the NextNonce value in the previous message. In addition, since HMAC credentials MUST be verified for each message, the SyncHdr status code for an authenticated message MUST be 200.<br/>
必须为每个消息使用新的随机数。 新的随机数将通过上一个消息中的NextNonce值获得。 此外，由于必须为每个消息验证HMAC凭证，所以已验证消息的SyncHdr状态代码必须为200。

### 5.1.4.5 Use of transport protocols providing authentication and integrity 使用传输协议提供认证和完整性保证
Note that the static conformance requirements for the HMAC feature is independent of its use. Neither client nor Server need supply the HMAC, unless challenged for it. For example, if it is deemed that an already authenticated transport protocol connection has already been established, then the Device or the Device Management Server MAY choose not to authenticate. In this particular situation, neither Server nor client is expected to issue a challenge for it. According to the general techniques specified in [DMPRO], a DM client that supports mutual authentication at the transport layer MAY choose not to support OMA DM authentication mechanisms. In this particular case, the Server MAY still issue a HMAC challenge, but the session MUST end if the client does not respond with the requested authentication type. The use of transport layer protocols is specified further in Section 5.5.1.1. The provisioning of credentials/certificates for transport layer authentication however, is beyond the scope of OMA DM Security.<br/>
请注意，HMAC特性的静态一致性要求与其使用无关。客户端和服务器都不需要提供HMAC，除非对它有质询。例如，如果认为已经建立了已经认证的传输协议连接，则设备或设备管理服务器可以选择不进行认证。在这种特殊情况下，服务器和客户端都不会对其发出质询。根据[DMPRO]中规定的一般技术，在传输层支持相互认证的DM客户端可以选择不支持OMA DM认证机制。在这种特殊情况下，服务器可能仍然发出HMAC质询，但是如果客户端没有用请求的认证类型响应，会话必须结束。传输层协议的使用在5.1.5.1.1节中进一步说明。然而，为传输层认证配置凭证/证书超出了OMA DM安全性的范围。

## 5.1.5 Confidentiality 保密性
Confidentiality in OMA DM has two major aspects; the confidentiality of information being transferred over a transport protocol, and the confidentiality of information between Device Management Servers.<br/>
OMA DM中的保密性有两个主要方面：通过传输协议传输的信息的机密性以及设备管理服务器之间的信息的机密性。
### 5.1.5.1 Confidentiality of information during transport 传输期间信息的保密性
Currently there is no inbuilt ability for the OMA DM protocol itself to provide confidentiality of the data being transferred between the Device and the Device Management Server. However, there are a number of techniques that OMA DM is compatible with that do provide this ability:<br/>
目前，对于OMA DM协议本身没有内置的能力来提供在设备和设备管理服务器之间传送的数据的保密性。 然而，有许多技术，他们与OMA DM兼容，并提供这种能力：

#### 5.1.5.1.1 Transport protocols that support encryption 支持加密的传输协议
The use of a transport layer protocol that supports encryption is RECOMMENDED for use where the exposure of the data to third party could have significantly negative consequences. Note that it is possible to use transports, which give confidentiality, without also having authentication. In these cases, confidentiality may be at risk.<br/>
支持加密的传输层协议的使用被推荐用于将数据暴露给第三方可能具有显着负面后果的用途。注意，可以使用给予保密性的传输，而不具有认证。在这些情况下，保密性可能有风险。

When using OMA DM over HTTP:
当使用OMA DM在HTTP上时：


* The Device Management Server MUST support both TLS 1.0 [TLS] and SSL3.0 [SSL3.0]
设备管理服务器必须支持TLS 1.0 [TLS]和SSL3.0 [SSL3.0]

* The Device Management Server MUST use TLS 1.0 or SSL3.0
设备管理服务器务必使用TLS 1.0或SSL3.0

* The device management client MUST use TLS 1.0 or SSL3.0
设备管理客户端必须使用TLS 1.0或SSL3.0

* The device management client MUST identify that the Device Management Server is using TLS1.0 or SSL3.0
设备管理客户端必须标识设备管理服务器正在使用TLS1.0或SSL3.0

* A device management session SHALL NOT take place over SSL2.0 or less.
设备管理会话必须不在SSL2.0或更低版本上发生。

* The Device Management Server MUST support all of the following cipher suites, all of which provide authentication, confidentiality and integrity, when using a TLS1.0 session<br/>
设备管理服务器必须支持所有以下密码套件，所有这些套件在使用TLS1.0会话时都提供身份验证，机密性和完整性
  * TLS_RSA_WITH_AES_128_CBC_SHA-1
  * TLS_RSA_WITH_3DES_EDE_CBC_SHA
  * TLS_RSA_WITH_RC4_128_SHA
* The device management client MUST support at least one of the following cipher suites, all of which provide authentication, confidentiality and integrity, when using a TLS1.0 session<br/>
设备管理客户端必须支持以下密码套件中的至少一个，当使用TLS1.0会话时，它们都提供认证，机密性和完整性
  * TLS_RSA_WITH_AES_128_CBC_SHA-1
  * TLS_RSA_WITH_3DES_EDE_CBC_SHA
  * TLS_RSA_WITH_RC4_128_SHA
* The Device Management Server MUST support both of the following cipher suites, both of which provide authentication, confidentiality and integrity, when using an SSL3.0 session<br/>
当使用SSL3.0会话时，设备管理服务器必须支持以下两种密码套件，这两种套件都提供身份验证，机密性和完整性
  * SSL_RSA_WITH_RC4_128_SHA
  * SSL_RSA_WITH_3DES_EDE_CBC_SHA
* The device management client MUST support at least one of the following cipher suites, both of which provide authentication, confidentiality and integrity, when using an SSL3.0 session<br/>
当使用SSL3.0会话时，设备管理客户端必须支持以下密码套件中的至少一个，它们都提供认证，机密性和完整性
  * SSL_RSA_WITH_RC4_128_SHA
  * SSL_RSA_WITH_3DES_EDE_CBC_SHA
  
The Device Management Server MAY accept the usage of other cipher suites with at least 128 bit symmetric keys when using an SSL3.0 or TLS1.0 session.<br/>
当使用SSL3.0或TLS1.0会话时，设备管理服务器可以接受使用具有至少128位对称密钥的其他密码套件。

The Device Management Server MUST support the requirements relating to certificates and certificate processing in section 6.3 and 6.4 of the WAP TLS Profile and Tunneling, [WAP-219-TLS].<br/>
设备管理服务器必须支持WAP TLS配置文件和隧道[WAP-219-TLS]第6.3和6.4节中与证书和证书处理相关的要求。

If the device management client supports TLS1.0, it MUST support the requirements relating to certificates and certificate processing in section 6.3 and 6.4 of the WAP TLS Profile and Tunneling, [WAP-219-TLS].<br/>
如果设备管理客户端支持TLS1.0，它必须支持WAP TLS配置文件和隧道[WAP-219-TLS]第6.3节和第6.4节中与证书和证书处理相关的要求。

#### 5.1.5.1.2 Management object encryption 管理对象加密
OMA DM fully supports the use of encrypted management objects, which may remain encrypted within the Device Management tree, or be decrypted upon receipt by the Device or Device Management Server.<br/>
OMA DM完全支持使用加密的管理对象，其可以在设备管理树内保持加密，或者在设备或设备管理服务器接收时被解密。

Depending upon implementation, an object may be encrypted prior to transmission over a non encrypted transport layer, and remain encrypted in storage space within either the Device Management Server or the Device, or, it may be decrypted immediately after receipt, and stored internally in unencrypted format.<br/>
根据实现，对象可以在通过非加密传输层传输之前被加密，并且在设备管理服务器或设备内的存储空间中保持加密，或者它可以在接收之后立即解密，并且以未加密格式在内部存储。

No restrictions are placed upon the encryption technique used, since this is independent of the OMA DM protocol itself.<br/>
对所使用的加密技术没有限制，因为这独立于OMA DM协议本身。

### 5.1.5.2 Confidentiality of information between Device Management Servers 设备管理服务器之间的信息保密性
OMA DM offers the ability for a Device Management Server to make private any data that is stored under Device Management control from another Device Management Servers. This is facilitated by the use of an ACL (Access Control List) that allows the protection of any group, or any individual Device Management object.<br/>
OMA DM使设备管理服务器能够将存储在设备管理控制下的任何数据从另一个设备管理服务器进行私有化。这通过使用允许保护任何组或任何单独设备的管理对象的ACL（访问控制列表）来实现。

#### 5.1.5.2.1 The Access Control List 访问控制列表
The Access Control List allows a hierarchical assignment of Access Rights based upon Device Management Server Identifiers’s (Unique identifiers for the Device Management Servers [DMTND]). A detailed description of the ACL can be found in [DMTND].<br/>
访问控制列表允许基于设备管理服务器标识符（设备管理服务器[DMTND]的唯一标识符）的访问权限的分级分配。有关ACL的详细说明，请参见[DMTND]。

## 5.1.6 Notification Initiated Session 通知启动会话
OMA DM offers the ability for a Device Management Server to make a request to a Device to establish a Management Session. The security of this message depends upon a digest. The specification of this message can be found in [DMNOTI].<br/>
OMA DM提供了设备管理服务器向设备请求建立管理会话的能力。此消息的安全性取决于摘要。该消息的规范可以在[DMNOTI]中找到。

## 5.1.7 Security for Bootstrap Operation 初始化操作的安全性
Bootstrapping is a sensitive process that may involve communication between two parties without any previous relationship or knowledge about each other. In this context, security is very important. The receiver of a bootstrap message needs to know that the information originates from the correct source and that it has not been tampered with en-route. It is important that DM clients accept bootstrapping commands only from authorized DM or CP servers.<br/>
初始化是一种敏感的过程，它可能涉及两方之间的通信，而彼此之间没有任何先前的关系或知识。 在这方面，安全是非常重要的。初始化消息的接收器需要知道信息源自正确的源并且它没有被经过篡改。 重要的是，DM客户端只接受来自授权的DM或CP服务器的引导命令。

### 5.1.7.1 Bootstrap via CP 通过CP初始化
The CP bootstrap mechanism is defined in [PROVBOOT].
CP初始化机制在[PROVBOOT]中定义。

#### 5.1.7.1.1 Smartcard 智能卡
The CP Bootstrap mechanism from the smartcard is defined in [PROVSC].<br/>
来自智能卡的CP初始化机制在[PROVSC]中定义。

### 5.1.7.2 Bootstrap via DM 通过DM初始化
#### 5.1.7.2.1 HMAC Computation for Bootstrap 初始化的HMAC计算
The HMAC is calculated in the following way:<br/>
HMAC以下列方式计算：

First, the bootstrap document is encoded in the WBXML format [WBXML1.1], [WBXML1.2], [WBXML1.3]. The encoded document and the shared secret are then input as the data and key, respectively, for the HMAC calculation [RFC2104], based on the SHA-1 algorithm [SHA], as defined in the WTLS specification [WTLS]. The output of the HMAC (M = HMAC- SHA(K, A)) calculation is encoded as a string of hexadecimal digits where each pair of consecutive digits represent a byte. The hexadecimal encoded output from the HMAC calculation is then included in the security information.<br/>
首先，引导文档以WBXML格式[WBXML1.1]，[WBXML1.2]，[WBXML1.3]编码。 然后，基于如WTLS规范[WTLS]中定义的SHA-1算法[SHA]，将编码文档和共享秘密分别作为HMAC计算的数据和密钥[RFC2104]输入。 HMAC（M = HMAC-SHA（K，A））计算的输出被编码为十六进制数字串，其中每对连续数字代表一个字节。HMAC计算的十六进制编码的输出被包括在安全信息中。

The security method and HMAC are then passed as parameters to the content type in the format like this: <br/>
然后将安全方法和HMAC作为参数传递到内容类型，格式如下：

Content-Type: MIME type; SEC=type; MAC=digest

Where:其中

MIME type is application/vnd.syncml.dm+wbxml (cannot use XML for bootstrap)
SEC = “NETWORKID”, “USERPIN”, or “USERPIN_NETWORKID”. Other types MAY also be used. Digest is the computed HMAC value as stated above.<br/>
MIME类型是application/vnd.syncml.dm + wbxml（不能使用XML进行初始化）
SEC =“NETWORKID”，“USERPIN”或“USERPIN_NETWORKID” 也可以使用其他类型。摘要是如上所述的计算的HMAC值。

#### 5.1.7.2.2 Transports 传输
Since any transport MAY be used to send the Bootstrap message to the DM client, appropriate security for bootstrapping a Device securely MUST be employed. If the transport has this appropriate security, it MUST be employed, otherwise, transport neutral security MUST be employed.<br/>
由于可以使用任何传输来向DM客户端发送初始化消息，因此必须采用用于安全地初始化设备的适当安全性措施。如果传输具有这种适当的安全性，必须使用，否则，必须使用运输中性安全。

Transport specific security is documented in the transport binding documents [SYNCHTTP], [SYNCOBEX], [SYNCWSP].
传输特定安全性记录在传输绑定文档[SYNCHTTP]，[SYNCOBEX]，[SYNCWSP]中。

#### 5.1.7.2.3 Transport Neutral Security 传输中性安全
The following subsections show some methods of transport neutral security. While the Server and client MUST support NETWORKID and USERPIN, they are not limited to just those – other methods MAY be used as long as they employ a level of security appropriate for bootstrap. The combined security of the secret (e.g., randomness, difficulty of obtaining, etc.), the transport and the environment of use needs to be among the considerations when a bootstrapping service is being implemented.<br/>
以下小节显示了一些传输工具中性安全的方法。虽然服务器和客户端必须支持NETWORKID和USERPIN，但是它们不仅限于那些 - 其他方法可以使用，只要它们的使用适合于初始化的安全级别。 当实现初始化服务时，密匙（例如，随机性，获得难度等），传输和使用环境的组合安全性需要考虑在内。

##### 5.1.7.2.3.1 NETWORKID
This method relies on some kind of shared secret that the Device and the network provider both know before the bootstrap process starts. This could be things like IMSI (for GSM) or ESN (for CDMA). What the shared secret actually is depends on the network provider and the particular Device. One advantage with this method is that is can be used without user intervention.<br/>
该方法依赖于设备和网络提供商在初始化过程开始之前都知道的某种共享密匙。这可以是诸如IMSI（用于GSM）或ESN（用于CDMA）的东西。共享密匙实际上取决于网络提供商和特定设备。 该方法的一个优点是可以在没有用户干预的情况下使用。

The NETWORKID method requires:<br/>
NETWORKID方法需要：

A HMAC value to be calculated using this shared secret and the DM bootstrap message, to be sent along with the message. See section 5.1.7.2.1.<br/>
要使用此共享密钥和DM初始化消息计算的HMAC值与消息一起发送。见第5.1.7.2.1节。

The protocol used to send the bootstrap message must be capable of transporting both the HMAC value and the OMA DM bootstrap package.<br/>
用于发送初始化消息的协议必须能够传输HMAC值和OMA DM引导程序包。

The security type SHALL be specified as ”NETWORKID”.<br/>
安全类型必须指定为“NETWORKID”。

OMA DM compliant Devices and Servers MUST support the NETWORKID method.<br/>
符合OMA DM的设备和服务器必须支持NETWORKID方法。

##### 5.1.7.2.3.2 USERPIN
This method relies on a PIN that must be communicated to the user out-of-band, or agreed to before the bootstrap process starts.<br/>
此方法依赖于必须在带外与用户通信或在初始化过程开始之前同意的PIN。

The USERPIN method requires:<br/>
USERPIN方法需要：

A HMAC value to be calculated using this shared secret and the DM bootstrap message, to be sent along with the message. See section 5。1.7.2.1.
要使用此共享密钥和DM初始化消息计算的HMAC值并与消息一起发送。见第5.1.7.2.1节。

The protocol used to send the bootstrap message must be capable of transporting both the HMAC value and the OMA DM bootstrap package.<br/>
用于发送初始化消息的协议必须能够传输HMAC值和OMA DM引导程序包。

The security type SHALL be specified as ”USERPIN”.<br/>
安全类型必须指定为“USERPIN”。

OMA DM compliant Devices and Servers MUST support the USERPIN method.<br/>
符合OMA DM的设备和服务器必须支持USERPIN方法。
