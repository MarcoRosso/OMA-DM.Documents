# 2.4 Authentication 认证
OMA DM Protocol uses the authentication framework specified in this chapter, with extensions defined in OMA Device Management Security [DMSEC]. This section specifies the rules for how the OMA-DM Protocol-level and the transport- level authentication are used.<br/>
OMA DM协议使用本章中指定的认证框架，其扩展在OMA设备管理安全[DMSEC]中定义。本节规定了如何使用OMA-DM协议层和传输层认证的规则。

Server and client can both challenge each other if no credentials were given in the original request or the credentials were considered too weak. If the server sent no credentials or invalid credentials in Package #2, no challenge and no commands (only Status to SyncHdr and DevInfo), the client MUST NOT challenge the server by sending back only a Status for the SyncHdr with a challenge. If the server challenged the client in Pkg 2, the client MUST revert to pkg 1 and MUST resend the Alert and DevInfo along with the credentials requested by the server.<br/>
如果在原始请求中没有提供凭据，或者认为凭据太弱，服务器和客户端都可以互相质疑。如果服务器在程序包＃2中没有发送凭证或发送无效的凭证，没有挑战和命令（只有状态到SyncHdr和DevInfo），客户端必须不通过发送回带有挑战的SyncHdr的状态来质疑服务器。如果服务器在Pkg2中质疑客户端，客户端必须恢复到pkg1，并且必须重新发送Alert和DevInfo以及服务器请求的凭据。

The preferred authentication type of the server may be indicated to the client using the `<X>/AAuthPref` parameter in DM Account management object [DMSTDOBJ].<br/>
可以使用DM帐户管理对象[DMSTDOBJ]中的`<X>/AAuthPref`参数向客户端指示服务器的优选认证类型。

Generation and maintenance of client and server credentials are out of scope of the OMA DM Protocol specification. In this chapter, the authentication procedures are defined for the basic and MD5 digest access authentication.<br/>
客户端和服务器凭据的生成和维护超出了OMA DM协议规范的范围。在本章中，为基本的和MD5摘要访问认证定义了认证过程。

## 2.4.1 Authentication Challenge 认证挑战
If the response code to a request (message or command) is 401 (‘Unauthorized’) or 407 (‘Authentication required’), the request requires authentication. In this case, the Status command to the request MUST include a Chal element (See [DMREPPRO]). The Chal contains a challenge applicable to the requested resource. The orignator MAY repeat the request with a suitable Cred element (See [DMREPPRO]). If the request already included the Cred element, then the 401 response indicates that authorization has been refused for those credentials.<br/>
如果对请求（消息或命令）的响应代码是401（'Unauthorized'）或407（'Authentication required'），则该请求需要验证。在这种情况下，请求的Status命令必须包含一个Chal元素（参见[DMREPPRO]）。 Chal包含适用于所请求资源的挑战。指令器可以使用合适的Cred元素重复请求（参见[DMREPPRO]）。如果请求已经包括Cred元素，则401响应指示已经为那些凭证拒绝了授权。

Both the client and the server can challenge for authentication.<br/>
客户端和服务器都可以质疑身份验证。

If the 401 response (i.e., Status) contains the same challenge as the prior response, and the user agent has already attempted authentication at least once, then the user SHOULD be presented the entity that was given in the response, since that entity might include relevant diagnostic information.<br/>
如果401响应（即，状态）包含与先前响应相同的挑战，并且用户代理已经尝试了至少一次认证，则推荐向用户呈现在响应中给出的实体，因为该实体可以包括相关诊断信息。

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

