# 2.4 Authentication 认证
OMA DM Protocol uses the authentication framework specified in this chapter, with extensions defined in OMA Device Management Security [DMSEC]. This section specifies the rules for how the OMA-DM Protocol-level and the transport- level authentication are used.<br/>
OMA DM协议使用本章中指定的认证框架，其扩展在OMA设备管理安全[DMSEC]中定义。本节规定了如何使用OMA-DM协议层和传输层认证的规则。

Server and client can both challenge each other if no credentials were given in the original request or the credentials were considered too weak. If the server sent no credentials or invalid credentials in Package #2, no challenge and no commands (only Status to SyncHdr and DevInfo), the client MUST NOT challenge the server by sending back only a Status for the SyncHdr with a challenge. If the server challenged the client in Pkg 2, the client MUST revert to pkg 1 and MUST resend the Alert and DevInfo along with the credentials requested by the server.<br/>
如果在原始请求中没有提供凭据，或者认为凭据太弱，服务器和客户端都可以互相质疑。如果服务器在程序包＃2中没有发送凭证或发送无效的凭证，没有挑战和命令（只有状态到SyncHdr和DevInfo），客户端必须不通过发送回带有挑战的SyncHdr的状态来质疑服务器。如果服务器在Pkg2中质疑客户端，客户端必须恢复到pkg1，并且必须重新发送Alert和DevInfo以及服务器请求的凭据。

The preferred authentication type of the server may be indicated to the client using the `<X>/AAuthPref` parameter in DM Account management object [DMSTDOBJ].<br/>
可以使用DM帐户管理对象[DMSTDOBJ]中的`<X>/AAuthPref`参数向客户端指示服务器的优选认证类型。

Generation and maintenance of client and server credentials are out of scope of the OMA DM Protocol specification. In this chapter, the authentication procedures are defined for the basic and MD5 digest access authentication.<br/>
客户端和服务器凭据的生成和维护超出了OMA DM协议规范的范围。在本章中，为基本的和MD5摘要访问认证定义了认证过程。
