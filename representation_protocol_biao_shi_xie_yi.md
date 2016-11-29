# Representation Protocol 表示协议
This document covers the Device Management usage of the SyncML Representation Protocol.<br/>
本文档介绍了SyncML表示协议的设备管理使用。

## OMA Device Management Usage OMA设备管理使用
There are two MIME content types for the OMA Device Management Message. The MIME content type of application/vnd.syncml.dm+xml identifies the clear-text XML representation for the DM Message. The MIME content type of application/vnd.syncml.dm+wbxml identifies the WBXML binary representation for the DM Message. Appendix C of this specification specifies the MIME content type registration for these two MIME media types.<br/>
OMA设备管理消息有两种MIME内容类型。应用程序的MIME内容类型/vnd.syncml.dm+xml标识DM消息的明文XML表示形式。应用程序的MIME内容类型/vnd.syncml.dm+wbxml标识DM消息的WBXML二进制表示。本规范的附录规定了这两种MIME媒体类型的MIME内容类型注册。

One of these two MIME content types MUST be used for identifying OMA Device Management Messages within transport and session level protocols that support MIME content types.<br/>
这两种MIME内容类型之一必须用于在支持MIME内容类型的传输和会话级协议中标识OMA设备管理消息。

All clients and servers MUST expect any 1.x version of WBXML, and all clients and servers MUST use any of the following versions of WBXML [WBXML1.1], [WBXML1.2], [WBXML1.3].<br/>
所有客户端和服务器必须支持任何1.x版本的WBXML，并且所有客户端和服务器必须使用以下任何版本的WBXML [WBXML1.1]，[WBXML1.2]，[WBXML1.3]。