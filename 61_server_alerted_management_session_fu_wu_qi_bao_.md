# 6.1 Server Alerted Management Session 服务器提醒的管理会话

This notification message is intended to provide a possibility for the server to alert the client to perform a management session. When the server alerts the client, it can tell for example the protocol version and whether the server proposes the session to be a foreground or background event. It can also tell if the session is happening because server has some management actions to perform or if the user caused the start of the session. The server MUST also send a digest that is included to prevent any Denial of Service (DoS) attacks.<br/>
该通知消息旨在提供服务器提醒客户端执行管理会话的可能性。当服务器提醒客户端时，它可以告诉例如协议版本以及服务器是否建议会话是前台或后台事件。它还可以判断会话是否正在发生，因为服务器有一些管理操作要执行，或者用户是否导致会话启动。服务器还必须发送包含的摘要，以防止任何拒绝服务（DoS）攻击。

Figure describes the MSC how the server alerts management session.
图描述了MSC如何提醒管理会话。

![](6.1.jpeg)
The package flow presented above is one OMA Device Management session. This means that all messages have the same OMA DM Session ID.<br/>
上面给出的包流程是一个OMA设备管理会话。 这意味着所有消息具有相同的OMA DM会话ID。