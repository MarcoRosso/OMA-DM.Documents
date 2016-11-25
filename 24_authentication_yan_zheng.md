# 2.4 Authentication 认证
OMA DM Protocol uses the authentication framework specified in this chapter, with extensions defined in OMA Device Management Security [DMSEC]. This section specifies the rules for how the OMA-DM Protocol-level and the transport- level authentication are used.<br/>
OMA DM协议使用本章中指定的认证框架，其扩展在OMA设备管理安全[DMSEC]中定义。本节规定了如何使用OMA-DM协议层和传输层认证的规则。

Server and client can both challenge each other if no credentials were given in the original request or the credentials were considered too weak. If the server sent no credentials or invalid credentials in Package #2, no challenge and no commands (only Status to SyncHdr and DevInfo), the client MUST NOT challenge the server by sending back only a Status for the SyncHdr with a challenge. If the server challenged the client in Pkg 2, the client MUST revert to pkg 1 and MUST resend the Alert and DevInfo along with the credentials requested by the server.<br/>
如果在原始请求中没有提供凭据，或者认为凭据太弱，服务器和客户端都可以互相质疑。如果服务器在程序包＃2中没有发送凭证或发送无效的凭证，没有挑战和命令（只有状态到SyncHdr和DevInfo），客户端必须不通过发送回带有挑战的SyncHdr的状态来质疑服务器。如果服务器在Pkg2中质疑客户端，客户端必须恢复到pkg1，并且必须重新发送Alert和DevInfo以及服务器请求的凭据。

The preferred authentication type of the server may be indicated to the client using the `<X>/AAuthPref` parameter in DM Account management object [DMSTDOBJ].<br/>
可以使用DM帐户管理对象[DMSTDOBJ]中的`<X>/AAuthPref`参数向客户端指示服务器的优选认证类型。

Generation and maintenance of client and server credentials are out of scope of the OMA DM Protocol specification. In this chapter, the authentication procedures are defined for the basic and MD5 digest access authentication.<br/>
客户端和服务器凭据的生成和维护超出了OMA DM协议规范的范围。在本章中，为基本的和MD5摘要访问认证定义了认证过程。

## 2.4.1 Authentication Challenge 认证质询
If the response code to a request (message or command) is 401 (‘Unauthorized’) or 407 (‘Authentication required’), the request requires authentication. In this case, the Status command to the request MUST include a Chal element (See [DMREPPRO]). The Chal contains a challenge applicable to the requested resource. The orignator MAY repeat the request with a suitable Cred element (See [DMREPPRO]). If the request already included the Cred element, then the 401 response indicates that authorization has been refused for those credentials.<br/>
如果对请求（消息或命令）的响应代码是401（'Unauthorized'）或407（'Authentication required'），则该请求需要验证。在这种情况下，请求的Status命令必须包含一个Chal元素（参见[DMREPPRO]）。 Chal包含适用于所请求资源的质询。指令器可以使用合适的Cred元素重复请求（参见[DMREPPRO]）。如果请求已经包括Cred元素，则401响应指示已经为那些凭证拒绝了授权。

Both the client and the server can challenge for authentication.<br/>
客户端和服务器都可以质疑身份验证。

If the 401 response (i.e., Status) contains the same challenge as the prior response, and the user agent has already attempted authentication at least once, then the user SHOULD be presented the entity that was given in the response, since that entity might include relevant diagnostic information.<br/>
如果401响应（即，状态）包含与先前响应相同的质询，并且用户代理已经尝试了至少一次认证，则推荐向用户呈现在响应中给出的实体，因为该实体可以包括相关诊断信息。

If the response code to a request is 212 (‘Authentication accepted’), no further authentication is needed for the remainder of the DM session. In the case of the MD5 digest access authentication, the Chal element can however be returned. Then, the next nonce in Chal MUST used for the digest when the next DM session is started.<br/>
如果对请求的响应代码是212（‘Authentication accepted’），则对于DM会话的剩余部分不需要进一步的认证。在MD5摘要访问认证的情况下，可以返回Chal元素。然后，当下一个DM会话开始时，Chal中的下一个nonce必须用于摘要。

If a request includes security credentials and the response code to the request is 200, the same credentials MUST be sent within the next request. If the Chal element is included and the MD5 digest access authentication is mandated, a new digest is created by using the next nonce. In the case of the MD5 digest access authentication, the Chal element can however be returned. The next nonce in Chal MUST be used when the next request is sent.<br/>
如果请求包括安全凭证，并且对请求的响应代码为200，则必须在下一个请求中发送相同的凭证。如果包括Chal元素并且强制执行MD5摘要访问认证，则通过使用下一个nonce来创建新的摘要。在MD5摘要访问认证的情况下，可以返回Chal元素。当发送下一个请求时，务必使用Chal中的下一个nonce。

Once authentication has occurred, the authentication type for a security layer MUST be kept same for the whole session.<br/>
一旦认证发生，安全层的认证类型务必与整个会话保持相同。

In case of authentication failure (either the userid and/or password was wrong or authentication was mandated) requirements are:<br/>
在身份验证失败（用户名和/或密码错误或强制授权）的情况下，要求是：

  * The response message indicating the authentication failure on application layer (see chapter 2.4.3) contains only Status commands (i.e. Replace, Get etc. commands MUST NOT be specified in the response). A Status command MUST be provided for every command received in the request.
指示应用层上认证失败的响应消息（见第2.4.3章）仅包含状态命令（即，不应在响应中指定Replace，Get等命令）。必须为请求中接收的每个命令提供Status命令。

  * In case the session is continued, the next message containing the proper credentials MUST contain a Status for the SyncHdr, MUST have the same SessionID as the previous messages and the message MUST be sent to the RespURI, if it was specified in the response indicating the authentication failure.<br/>
在会话继续的情况下，包含适当证书的下一个消息必须包含SyncHdr的状态，必须具有与先前消息相同的SessionID，并且消息必须发送到RespURI，如果它在响应中指定认证失败。

## 2.4.2 Authorization 授权
The Cred element MUST be included in requests (message or command), which are sent after receiving the 401 or 407 responses if the request is repeated. In addition, it can be sent in the first request from a device if the authentication is mandated through pre-configuration. The content of the Cred element is specified in [DMREPPRO]. The authentication type is dependent on the challenge (See the previous chapter) or the pre-configuration.<br/>
Cred元素必须包括在请求（消息或命令）中，如果请求被重复，它们在接收401或407响应之后发送。此外，如果通过预配置强制认证，则可以在来自设备的第一请求中发送它。 Cred元素的内容在[DMREPPRO]中指定。 认证类型取决于质询（参见前一章）或预配置。

## 2.4.3 Application Layer Authentication 应用层认证
The authentication on the application layer is accomplished by using the Cred element in SyncHdr and the Status command associated with SyncHdr. Within the Status command, the challenge for the authentication is carried as defined earlier. The authentication can happen both directions, i.e., the client can authenticate itself to the server and the server can authenticate itself to the client.<br/>
应用层上的认证通过使用SyncHdr中的Cred元素和与SyncHdr相关联的Status命令来实现。在状态命令中，如先前定义的那样进行认证的质询。认证可以在两个方向发生，即，客户端可以向服务器认证自身，并且服务器可以向客户端认证自身。

## 2.4.4 Authentication Examples 验证示例
### 2.4.4.1 Basic authentication with a challenge 使用质询进行基本身份验证
At this example, the client tries to initiate with the server without any credentials (Pkg #1). The server challenges the client (Pkg #2) for the application layer authentication. The client MUST send Pkg #1 again with the credentials. The server accepts the credentials and the session is authenticated (Pkg #2). In the example, commands in SyncBody are not shown although in practice, they would be there.<br/>
在此示例中，客户端尝试使用服务器启动而不使用任何凭据（Pkg＃1）。服务器向客户端（Pkg＃2）询问应用程序层认证。客户端必须再次使用凭证发送Pkg＃1。服务器接受凭据，并且会话已通过身份验证（Pkg＃2）。在该示例中，SyncBody中的命令不显示，虽然在实践中，他们将存在。

Pkg #1 from Client:  客户端发送的包1:
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
    <VerDTD>1.2</VerDTD>
    <VerProto>DM/1.2</VerProto>
    <SessionID>1</SessionID>
    <MsgID>1</MsgID> 
      <Target><LocURI>http://www.syncml.org/mgmt-server</LocURI></Target> 
      <Source><LocURI>IMEI:493005100592800</LocURI></Source>
  </SyncHdr>
  <SyncBody>
     ...
  </SyncBody>
</SyncML>
```
Pkg #2 from Server:  服务器发送的包2:
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
    <VerDTD>1.2</VerDTD>
    <VerProto>DM/1.2</VerProto>
    <SessionID>1</SessionID>
    <MsgID>1</MsgID> <Target><LocURI>IMEI:493005100592800</LocURI></Target> 
    <Source><LocURI>http://www.syncml.org/mgmt-server</LocURI></Source>
  </SyncHdr>
  <SyncBody>
     <Status>
     <CmdID>1</CmdID>
     <MsgRef>1</MsgRef>
     <CmdRef>0</CmdRef>
     <Cmd>SyncHdr</Cmd> 
     <TargetRef>http://www.syncml.org/mgmt-server</TargetRef> 
     <SourceRef>IMEI:493005100592800</SourceRef>
     <Chal>
       <Meta>
          <Type xmlns=’syncml:metinf’>syncml:auth-basic</Type>
          <Format xmlns=’syncml:metinf’>b64</Format> </Meta>
     </Chal>
     <Data>407</Data> <!-- Credentials missing --> </Status>
     ...
  </SyncBody>
</SyncML>
```
Pkg #1 (with credentials) from Client:  客户端发送的包1（有凭据）:
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
    <VerDTD>1.2</VerDTD>
    <VerProto>DM/1.2</VerProto>
    <SessionID>1</SessionID>
    <MsgID>2</MsgID> 
    <Target><LocURI>http://www.syncml.org/mgmt-server</LocURI></Target> 
    <Source><LocURI>IMEI:493005100592800</LocURI></Source>
    <Cred>
      <Meta>
      <Type xmlns=’syncml:metinf’>syncml:auth-basic</Type> 
      <Format xmlns='syncml:metinf'>b64</Format>
      </Meta>
      <Data>QnJ1Y2UyOk9oQmVoYXZl</Data>
      <!-- base64 formatting of “userid:password” --> 
    </Cred>
  </SyncHdr>
  <SyncBody>
     ...
  </SyncBody>
</SyncML>
```
Pkg #2 from Server:  服务器发送的包2:
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
    <VerDTD>1.2</VerDTD>
    <VerProto>DM/1.2</VerProto>
    <SessionID>1</SessionID>
    <MsgID>2</MsgID> 
    <Target><LocURI>IMEI:493005100592800</LocURI></Target> <Source>
    <LocURI>http://www.syncml.org/mgmt-server</LocURI></Source>
  </SyncHdr>
  <SyncBody>
     <Status>
     <CmdID>1</CmdID> 
     <MsgRef>2</MsgRef><CmdRef>0</CmdRef><Cmd>SyncHdr</Cmd> 
     <TargetRef>http://www.syncml.org/mgmt-server</TargetRef> 
     <SourceRef>IMEI:493005100592800</SourceRef>
     <Data>212</Data> <!-- Authenticated for session -->
      </Status>
     ...
  </SyncBody>
</SyncML>

```
### 2.4.4.2 MD5 digest access authentication with a challenge MD5摘要访问认证与质询
At this example, assume (as in 9.4.1 above) the client tries to initiate with the server without any credentials (Pkg #1 is omitted here for brevity). The server challenges the client as above (Pkg #2 is also omitted from this example) for the application layer authentication. The authentication type is now syncml:auth-md5 (MD5 digest access authentication). The client MUST resend Pkg #1 this time with the MD5 credentials (as shown below in Pkg #1). The server accepts the credentials and the session is authenticated (Pkg#2 below). Also, the server sends the next nonce to the client, which the client MUST use when the next DM session is started. In the example, commands in SyncBody are not shown although in practice, they would be there.<br/>
在这个示例中，假设（如在上面2.4.4.2中）客户端尝试使用没有任何凭证的服务器发起连接（为了简洁，这里省略Pkg＃1）。服务器通过如上所述的方式向客户端发起应用层认证的质询，（Pkg＃2也从本示例中省略）。认证类型现在为syncml：auth-md5（MD5摘要访问认证）。客户端必须使用MD5凭据重新发送Pkg＃1（如下面的Pkg＃1所示）。服务器接受凭据，并且会话通过身份验证（下面的Pkg＃2）。此外，服务器向客户端发送下一个nonce，客户端必须在下一个DM会话开始时使用它。 在示例中，SyncBody中的命令不显示，虽然在实践中，他们会存在。

Pkg #1 from Client:  客户端发送的包1:
```
<SyncML xmlns='SYNCML:SYNCML1.2'>
  <SyncHdr>
    <VerDTD>1.2</VerDTD>
    <VerProto>DM/1.2</VerProto>
    <SessionID>1</SessionID>
    <MsgID>2</MsgID> 
    <Target><LocURI>http://www.syncml.org/mgmt-server</LocURI></Target> 
    <Source>
      <LocURI>IMEI:493005100592800</LocURI> 
      <LocName>Bruce2</LocName> <!-- userid --> 
    </Source>
    <Cred>
     <Meta>
       <Type xmlns=’syncml:metinf’>syncml:auth-md5</Type>
       <Format xmlns=’syncml :metinf’>b64</Format>
     </Meta>
    <Data>Zz6EivR3yeaaENcRN6lpAQ==</Data>
    <!-- Base64 coded MD5 for user “Bruce2”, password “OhBehave”, nonce “Nonce” -->
    </Cred>
  </SyncHdr>
  <SyncBody>
     ...
  </SyncBody>
</SyncML>
```
Pkg #2 from Server:  服务器发送的包2: