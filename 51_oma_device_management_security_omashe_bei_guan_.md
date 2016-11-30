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
