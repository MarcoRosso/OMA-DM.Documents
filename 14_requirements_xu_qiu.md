# 1.4 Requirements 需求
## 1.4.1 High Level Functional Requirements 高级功能需求
### 1.4.1.1 Security 安全
#### 1.4.1.1 General security requirements 一般安全需求
1. The authentication procedure MUST be strong enough to ensure that is not be possible for a third party to masquerade as a Device management server by spoofing its identity. <br/>
认证过程必须足够强，以确保第三方不可能通过欺骗其身份来伪装为设备管理服务器。
2. The client and sever MUST be capable of detecting replay attacks.<br/>
客户端和服务器必须能够检测重放攻击。 
3. Architecture supports traversal of corporate firewalls and Network translation Devices (Use Case 1.3.1.2)<br/>
架构支持公司防火墙和网络翻译设备的遍历（用例1.3.1.2）
4. If end user confirmation is indicated by the Device Management Server, the Device will prompt for user confirmation before incorporation of configuration data. (Use Case 1.3.1.5)<br/>
如果设备管理服务器指示最终用户确认，则在合并配置数据之前，设备将提示用户确认。(用例1.3.1.5）
5. Except for establishing the initial trust relationship (bootstrap) over the air, if end user confirmation is not indicated by the Device Management Server, the Device MUST NOT ask for user confirmation before incorporation of configuration data. (Use Case 1.3.1.5)<br/>
除了通过空中下载建立初始信任关系（引导）之外，如果设备管理服务器未指示最终用户确认，则设备必须不在并入配置数据之前请求用户确认。（用例1.3.1.5）
6. The non-repudiation of the session MUST be ensured. (Use Case 1.3.4.1) <br/>
必须确保会话的不可否认性。（用例1.3.4.1)



#### 1.4.1.2 Authentication 鉴定
Before any Device management operations can be carried out on the Device, it must conform to the following:<br/>
在设备上执行任何设备管理操作之前，必须符合以下要求：
1. The client MUST successfully authenticate the Device Management server (Use Case 1.3.2.1).<br/>
客户端必须成功验证设备管理服务器（用例1.3.2.1）。
2. If the Device management operation is related to personal information then the user MUST successfully authenticate himself to the Device management server (Use Case 1.3.2.1).<br/>
如果设备管理操作与个人信息相关，则用户必须成功地向设备管理服务器认证自己（用例1.3.2.1）。
3. The Device Management Server May also authenticate the Device (Use Case 1.3.1.1., 1.3.1.3, 1.3.4.1)<br/>
设备管理服务器也可以验证设备（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
4. Whenever there is communication between Device Management Servers the Device Management Servers MUST mutually authenticate (Use Case 1.3.1.2).<br/>
每当设备管理服务器之间有通信时，设备管理服务器必须相互认证（用例1.3.1.2）。
5. With local wireless interfaces, discovery is controlled between the PC Agent and Device. Secure association and authentication MUST be supported. The first connection requires a secure association be created between the Device and PC. (Use Case 1.3.1.5)<br/>
当使用本地无线接口时，设备发现被控制在PC代理和设备之间。必须支持安全关联和认证。第一个连接需要在设备和PC之间创建安全关联。（用例1.3.1.5）

#### 1.4.1.3 Authorisation 授权
Before the Device Management server can carry out any Device management operations on the Device, it must conform to the following:<br/>
在设备管理服务器可以在设备上执行任何设备管理操作之前，它必须符合以下条件：
1. The Device Management server MUST be authorised to carry out any Device management operations on the Device (Use Case 1.3.2.1).<br/>
设备管理服务器必须被授权在设备上执行任何设备管理操作（用例1.3.2.1）。
2. With local wireless interfaces, discovery is controlled between the PC Agent and Device. Secure association and authorisation MUST be supported. The first connection requires a secure association be created between the Device and PC. (Use Case 1.3.1.5)<br/>
当使用本地无线接口时，设备发现被控制在PC代理和设备之间。必须支持安全关联和授权。第一个连接需要在设备和PC之间创建安全关联。（用例1.3.1.5）


#### 1.4.1.4 Integrity protection 完整性保护
1. All data communication between the Device Management Server and a Device MUST be integrity protected. (Use Case 1.3.1.1, 5.1.3, 5.4.1)<br/>
设备管理服务器和设备之间的所有数据通信必须是完整性保护的。（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
2. All data communication between Device Management Server MUST be integrity protected. (Use Case 1.3.1.2)<br/>
设备管理服务器之间的所有数据通信必须完整性保护。（用例1.3.1.2）
3. The Data Link between the Software Originator (or agent) and the Device Management Server MUST maintain data integrity. (Use Case 1.3.5.1)<br/>
软件发起方（或代理）和设备管理服务器之间的数据链路必须保持数据完整。（用例1.3.5.1）
4. The inventory SHALL be secure from alteration when sent by the appropriate integrity protection. (Use Case 1.3.3.1) <br/>
当通过适当的完整性保护发送时，目录必须是安全的。（用例1.3.5.1）
5. The downloaded software SHALL be secure from alteration by the appropriate integrity protection. (Use Case 5.3.1)<br/>
下载的软件应必须不受适当的完整性保护的影响。（用例1.3.3.1）

#### 1.4.1.5 Confidentiality protection 机密性保护

1. All data communication between the Device Management Server and a Device, that is personal to the user or confidential to the owner of the information (e.g. some network operator settings) MUST be confidentiality protected. (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
设备管理服务器和设备之间的所有数据通信（对于用户来说是个人的或对信息所有者来说是机密的）（例如某些网络运营商设置）必须是机密性保护的。（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
2. All data communication between Device Management Servers MUST be confidentiality protected. (Use Case 1.3.1.2)<br/>
设备管理服务器之间的所有数据通信必须被机密性保护。（用例1.3.1.2）
3. The Data Link between the Software Originator (or agent) and the Device Management Server MAY maintain data confidentiality. (Use Case 1.3.5.1)<br/>
软件发起者（或代理）和设备管理服务器之间的数据链路可以维护数据保密。（用例1.3.5.1）
4. The Data Link between the Device Management Server and the Device MAY maintain data confidentiality, where appropriate. (Use Case 1.3.5.1)<br/>
设备管理服务器和设备之间的数据链路可以在适当情况下保持数据机密性。（用例1.3.5.1）

#### 1.4.1.6 Smart card security 智能卡安全

1. Provisioning data on smart card SHALL be protected against unauthorized modification. (UC 1.3.1.3) <br/>
智能卡上的配置数据必须防止未经授权的修改。（用例 1.3.1.3）
2. It SHALL NOT be possible for the Smart Card to reveal any secret keys it holds (UC 1.3.1.3)<br/>
智能卡必须不显示其所拥有的任何密钥（用例 1.3.1.3）


### 1.4.1.2 Recording 纪录
1. The Device Management System SHALL provide sufficient information so that queries from the Device Management Server, reports from Devices, data downloads, and acknowledgements MAY be billed and tracked accordingly. (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
设备管理系统必须提供足够的信息，以便接受来自设备管理服务器的查询，来自设备的报告，数据下载和确认可以被相应地纪录和跟踪。（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
2. If a management authority causes delegation to occur among several Device Management Servers, the Management Authority MAY request from each DMS, and each DMS SHALL provide, reports of the operations performed in a device for tracking purposes (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
如果管理权限导致在多个设备管理服务器之间发生授权，则管理权限可以从每个DMS请求并且每个DMS应当提供在设备中执行的用于跟踪目的的操作的报告（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
3. The session MUST be identified as customer-care-related. (Use Case 1.3.4.1)<br/>
会话必须被标识为与客户服务相关。（用例1.3.4.1）
4. The session MUST be uniquely identified. (Use Case 1.3.4.1)<br/>
会话必须被唯一标识。（用例1.3.4.1）
5. If transactions are logged, server MUST log transactions with success indicator. (Use Case 1.3.4.1)<br/>
如果记录事务，则服务器必须使用成功指示器记录事务。（用例1.3.4.1）


### 1.4.1.3 Administration and Configuration 管理和配置

1. The DMS SHALL provide a standardized mechanism for publishing session/message transactions, such as confirmation requests and results, etc.(Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
DMS必须提供用于发布会话/消息事务的标准化机制，例如确认请求和结果等。（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
2. Confirmation request messages SHALL be uniquely identified and contain at least the subscriber id, data or data summary, and date/time.
(Use Case 1.3.4.1)<br/>
确认请求消息必须唯一标识，并至少包含订户id，数据或数据摘要和日期/时间。（用例1.3.4.1）
3. Confirmation result messages SHALL be uniquely identified and correlated to the request.(Use Case 1.3.4.1)<br/>
确认结果消息必须唯一标识并与请求相关联。（用例1.3.4.1）
4. Management Authority MAY be delegated by a primary Management Authority (one that has domain over a given set of Management Objects) to a secondary Management Authority. (Use Case 1.3.1.1)<br/>
管理机构可以由主管理机构（具有指定管理对象集合的域）委托给次级管理机构。（用例1.3.1.1）
5. The first connection MUST involve a secure association be created between the Device and PC. (Use Case 1.3.1.5)<br/>
第一个连接必须涉及在设备和PC之间创建安全关联。（用例1.3.1.5）
6. The DMS shall send a notification of the update/upgrade to the appropriate management authority. (Use Case 1.3.3.1)<br/>
DMS必须向适当的管理机构发送更新/升级的通知。（用例1.3.3.1）


### 1.4.1.4 Usability 可用性
1. If user confirmation is indicated by smart card data, the Device SHALL ask for user confirmation before incorporation of provisioning data (stored on smart card).<br/>
如果智能卡数据指示用户确认，则在合并配置数据（存储在智能卡上）之前，设备必须要求用户确认。
2. If user confirmation is not indicated by smart card data, the Device MUST NOT ask for user confirmation before incorporation of provisioning data (stored on smart card). (用例 1.3.1.3)<br/>
如果智能卡数据未指示用户确认，则设备必须不在合并供应数据（存储在智能卡上）之前请求用户确认。（用例 1.3.1.3）
3. If indicated by smart card data, the Device SHALL establish the connection to Device Management Server autonomously. (UC 1.3.1.3)<br/>
如果数据由智能卡提供，设备必须自动建立与设备管理服务器的连接。（用例 1.3.1.3）
4. If user confirmation is indicated by the Device Management Server, the Device SHALL ask for user confirmation before incorporation of configuration data (transferred by Device Management Server).<br/>
如果设备管理服务器指示用户确认，则在合并配置数据（由设备管理服务器传送）之前，设备必须要求用户确认。
5. Except for establishing the initial trust relationship configuration (bootstrap) over the air, if user confirmation is not indicated by the Device Management Server, the Device MUST NOT ask for user confirmation before incorporation of configuration data (transferred by Device Management Server). (用例 1.3.1.3, 1.3.1.4, 1.3.2.1)<br/>
除了通过空中下载建立初始信任关系配置（引导）之外，如果设备管理服务器未指示用户确认，则在并入配置数据（由设备管理服务器传送）之前，设备必须不要求用户确认。 （用例 1.3.1.3, 1.3.1.4, 1.3.2.1）
6. The Device SHALL be capable for being contacted by the Device Management Server, if the Device is switched on and has radio coverage by its subscribed network operator and is not busy by a voice link. (用例 1.3.2.1)<br/>
如果设备通电并且具有由其订阅的网络运营商的无线电覆盖并且不被语音链路占用，则设备必须能够被设备管理服务器联系。（用例 1.3.2.1）
7. The Device MAY be capable for being contacted by the Device Management Server, if the Device is busy by a voice link. (UC 1.3.2.1)<br/>
如果设备通过语音链路正忙，则设备可以能够被设备管理服务器联系。（用例 1.3.2.1）
8. User is not prompted if there is no work to be done (Use Case 1.3.1.5)<br/>
如果没有工作要做，则不提示用户（用例1.3.1.5）
9. Management Authority MAY clarify implications of subsequent actions (query, etc.) to the User. (Use Case 1.3.4.1)<br/>
管理机构可以澄清后续行动（查询等）对用户的影响。（用例1.3.4.1）
10. User voice calls MUST NOT be terminated upon reception of the query. (Use Case 1.3.4.1)<br/>
用户语音呼叫必须不在接收到查询时终止。（用例1.3.4.1）
11. User voice calls MUST NOT be terminated upon reception of the authorization request. (Use Case 1.3.4.1)<br/>
用户语音呼叫必须不在收到授权请求时终止。（用例1.3.4.1）
12. Authorization MUST be clear esp. regarding privacy issues and warranty. (Use Case 1.3.4.1)<br/>
由于隐私和保修问题，授权必须清除。（用例1.3.4.1）
13. User MAY be informed that the process is over. (Use Case 1.3.4.1)<br/>
用户可被告知过程已结束。（用例1.3.4.1）
14. The user SHALL be asked for confirmation to proceed before any software is updated. (Use Case 1.3.3.1)<br/>
在更新任何软件之前，必须要求用户确认以继续操作。（用例1.3.3.1）
15. The user SHALL be informed that the update/upgrade has been completed. (Use Case 1.3.3.1)<br/>
必须通知用户更新/升级已完成。（用例1.3.3.1）
16. The Device MUST NOT send an inventory list of applications installed in the Device without either this optional feature being added by the user or the Device asks for permission from the user when needed.<br/>
设备必须不发送安装在设备中的应用程序的清单列表，或者用户可添加此可选功能，或者设备在需要时向用户请求许可。

### 1.4.1.5 Interoperability 互操作性

1. The DMS MAY be interfaced with a Customer Care application. (Use Case 1.3.4.1) <br/>
DMS可以与客户服务应用程序接口。（用例1.3.4.1）
2. Errors MAY be reported to a Customer Care application. (Use Case 1.3.4.1)<br/>
错误可以报告给客户服务中心应用程序。（用例1.3.4.1）


### 1.4.1.6 Privacy 隐私
Requirements covered in other sections. <br/>
需求已在其它部分描述。

## 1.4.2 Overall Systems Requirements 整体系统要求
1. The Device Management infrastructure MAY be based on a distributed architecture, wherein functional elements of the system (e.g., the Device Management Server) MAY consist of one or more coordinated, but physically separate entities. (Use Case 1.3.1.1)<br/>
设备管理基础设施可以基于分布式架构，其中系统的功能元件（例如，设备管理服务器）可以由一个或多个协调但物理上分离的实体组成。（用例1.3.1.1）
2. The overall system SHALL support a distributed system architecture (Use Case 1.3.1.2)<br/>
整个系统必须支持分布式系统架构（用例1.3.1.2）
3. Device Discovery by the Device Management Server MUST be clearly defined (e.g. SMS, push.). (Use Case 1.3.4.1)<br/>
必须清楚地定义设备管理服务器的设备发现（例如，SMS，推送）。（用例1.3.4.1）
4. The Device Management System SHALL make provision for different Management Authorities (e.g. Enterprise, Network Operator) to manage different data sets or applications in a single device. Each Management Authority can control data sets and applications owned by that Management Authority.<br/>
设备管理系统必须为不同的管理机构（例如企业，网络运营商）提供管理，以在单个设备中管理不同的数据集或应用程序。每个管理机构可以控制该管理机构拥有的数据集和应用程序。

## 1.4.3 Systems Elements 系统组件
### 1.4.3.1 Device 设备
1. The Device SHALL be capable of discovering the presence of nearby, active Device Management system elements if those elements are using compatible local bearers. (Use Case 1.3.1.1)<br/>
如果这些元件使用兼容的本地承载，则设备必须能够发现附近的，活动的设备管理系统元件的存在。（用例1.3.1.1）
2. The Device SHALL be able to communicate all of its relevant properties (e.g., manufacturer, model, firmware, etc.) to the Device Management Server on demand. (Use Case 1.3.1.1,  1.3.1.3, 1.3.4.1)<br/>
设备应能够根据需要将所有相关属性（例如，制造商，型号，固件等）传送到设备管理服务器。（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
3. The Device SHALL be able to communicate its capabilities and configuration (e.g., WAP/MMS settings, installed software applications, etc.) to the Device Management Server on demand. (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
设备必须能够按需向设备管理服务器传达其能力和配置（例如，WAP/MMS设置，安装的软件应用等）。（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
4. The Device SHALL be capable of autonomously (i.e., without User interaction) accepting and storing downloaded Management Objects (e.g., parameters, software, etc.) after the one time initial trust relationship configuration (bootstrap) is performed. (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
在执行一次初始信任关系配置（引导）之后，设备必须能够自主地（即，没有用户交互）接受和存储下载的管理对象（例如，参数，软件等）。（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
5. Obsolete/outdated configuration data transferred/stored by any other Management Authority MUST NOT prevent the incorporation of the current data (UC 1.3.1.4).<br/>
由任何其他管理机构传输/存储的过时/过期的配置数据必须不阻止并入当前数据（用例  1.3.1.4）
6. The data tree for containing Device management objects on the Device SHALL be capable of being modified (i.e., nodes or data fields added or deleted), read from, and/or written to. (Use Case 1.3.1.1, 1.3.1.3, and 1.3.4.1)<br/>
用于包含设备上的设备管理对象的数据树必须能够被修改（即，添加或删除节点或数据字段），读取和/或写入。 （用例1.3.1.1, 1.3.1.3和1.3.4.1）
7. The Device SHALL be capable of receiving and displaying a command from the DM Server to request User confirmation for a management action. (Use Case 1.3.4.1)<br/>
设备必须能够接收和显示来自DM服务器的命令，以请求用户确认管理动作。（用例1.3.4.1）
8. The Device SHALL be capable of accepting User input regarding confirmation of a proposed management action, and sending the result of that confirmation to the DM Server. (Use Case 1.3.4.1)<br/>设备必须能够接受关于提出的管理动作的用户确认输入，并且将该确认的结果发送到DM服务器。（用例1.3.4.1）
9. The Device SHALL be able to acknowledge the receipt and installation of data downloaded from the Device Management Server. (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
设备必须能够确认从设备管理服务器接收下载数据并安装。（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
10. The Device SHALL be capable of detecting the presence of provisioning data on an installed, activated Smart Card. (Use Case 1.3.1.3)<br/>
设备必须能够检测安装的激活智能卡上是否存在配置数据。（用例1.3.1.3）
11. The Device SHALL be capable of autonomously establishing a data link with the Device Management Server, using connectivity information stored on the Smart Card. (Use Case 1.3.1.3)<br/>
设备必须能够使用存储在智能卡上的连接信息自主地与设备管理服务器建立数据链路。 （用例1.3.1.3）
12. The Device SHALL be capable of participating in a mutual authentication with the Device Management Server, using authentication credentials (e.g., a challenge response) stored on or derived from the Smart Card. (Use Case 1.3.1.3, 1.3.4.1)<br/>
设备必须能够使用存储在智能卡上或从智能卡导出的认证证书（例如，质询响应）参与与设备管理服务器的相互认证。（用例1.3.1.3, 1.3.4.1）
13. Device SHALL retrieve and incorporate relevant configuration data stored on the smart card into the Device's DM structure. (UC 1.3.1.3)<br/>
设备必须检索并将存储在智能卡上的相关配置数据合并到设备的DM结构中。(用例 1.3.1.3)
14. Each Device MUST support standardized dynamic IP allocation when the Device is first connected to the network. If an IP address cannot be allocated from the network, then the Device MUST use automatic IP addressing (Auto-IP) to obtain an address. (Use Case 1.3.1.5)<br/>
当设备首次连接到网络时，每个设备必须支持标准化的动态IP分配。如果无法从网络分配IP地址，则设备必须使用自动IP寻址（自动IP）来获取地址。（用例1.3.1.5）
15. The Device SHOULD announce itself on the network to all control points it detects. The act of announcement does not imply the Device will receive rights, since assignment of rights is an expression of the user's decision. When the Device is added to the network, the discovery protocol allows that Device to advertise its services to control points on the network. The fundamental exchange in both cases is a discovery message containing a few, essential specifics about the Device e.g., its type, identifier, and a pointer to more detailed information. (Use Case 1.3.1.5)<br/>
推荐设备在网络上向自己检测到的所有控制点发布自己的消息。公告行为并不意味着设备将接收权限，因为权限的分配是用户决定的表达。当设备添加到网络时，发现协议允许该设备向网络上的控制点通告其服务。在这两种情况下的基本交换信息包含的是关于设备的几个基本细节的发现消息，例如其类型，标识符和指向更详细信息的指针。（用例1.3.1.5）
16. The Device MUST support the assignment of a friendly name in relation to a network unique name(Use Case 1.3.1.5)<br/>
设备必须支持关于网络唯一名称的友好名称的分配。（用例1.3.1.5）
17. The mapping from friendly name to unique name MUST be the function of each user’s user interface in the case where the Device is shared. (Use Case 1.3.1.5)<br/>
从友好名称到唯一名称的映射必须是当设备已共享时每个用户的用户界面。 （用例1.3.1.5）
18. A method SHOULD be available by which a Device MAY automatically configure an interface with an IPv6 link-local address, IPv4 address in the 169.254/16 range that is valid for link-local communication on that interface, or both. On top of this there is a requirement to be able to define the link-local configuration to enable hosts that support multi-homing (more than one active interface and/or, more than one active address per interface, both IPv4 and IPv6 addresses, or a combination of these).This requirement is especially valuable in environments where no other configuration mechanism such as DHCP is available. (Use Case 1.3.1.5)<br/>
推荐使用一种方法，通过该方法设备可以自动配置具有IPv6链路的本地地址的接口，或在169.254/16范围内的IPv4的本地地址接口通信，或者同时配置两者。除此之外，需要能够定义链路本地配置以使得其能支持多归属的主机（多于一个活动接口和/或每个接口多于一个活动地址，IPv4和IPv6地址，或这些的组合）。在没有诸如DHCP的其他配置机制可用的环境中，该要求是特别有价值的。（用例1.3.1.5）
19. The Device SHOULD support IP based Device discovery based on the SSDP [http://www.upnp.org/download/draft_cai_ssdp_v1_03.txt]. The Device SHOULD support a 30 minute suggested timeout for when a Device is added or disappears from the network. (Use Case 1.3.1.5)<br/>
设备应该支持基于SSDP的基于IP的设备发现。当设备添加或从网络中消失时，推荐设备支持30分钟超时。（用例1.3.1.5）
20. If end user confirmation is indicated by the Device Management Server, the Device will prompt for user confirmation before incorporation of configuration data. (Use Case 1.3.1.5)<br/>
如果设备管理服务器指示最终用户确认，则在合并配置数据之前，设备将提示用户确认。（用例1.3.1.5）
21. PC Agent SHALL be capable of changing the DM tree on the Device and install the application (Use Case 1.3.1.5) 
PC代理应能够更改设备上的DM树并安装应用程序（用例 1.3.1.5）
22. The Device MAY support concurrent voice calls and data exchanges. (Use Case 1.3.4.1)<br/>
设备可以支持并发语音呼叫和数据交换。（用例1.3.4.1）
23. The Device MUST support at least one wireless data bearer. (Use Case 1.3.4.1)<br/>
设备必须支持至少一个无线数据承载。（用例1.3.4.1）
24. The Device MUST respond to query. (Use Case 1.3.4.1)<br/>
设备必须响应查询。（用例1.3.4.1）
26. The Device MUST verify integrity of data before execution. (Use Case 1.3.4.1)<br/>
设备必须在执行之前验证数据的完整性。（用例1.3.4.1）
27. The Device MUST report to Server errors that occur during the parameter or software download. (Use Case 1.3.4.1)<br/>
设备必须报告参数或软件下载期间发生的服务器错误。（用例1.3.4.1）
28. The Device MUST be capable of determining that the Server is authorized to provide the software and/or data. (Use Case
1.3.5.1)<br/>
设备必须能够确定服务器被授权提供软件和/或数据。（用例1.3.5.1）
29 The Device MUST be capable of exchanging security information with the Server. (Use Case 1.3.5.1) <br/>
设备必须能够与服务器交换安全信息。（用例1.3.5.1）
30. The Device MUST be capable of storing the software that is downloaded. (Use Case 1.3.5.1)<br/>
设备必须能够存储下载的软件。（用例1.3.5.1）
31. The Device MUST be able to independently verify the validity of the Software Originator of the Software and/or Data downloaded. (Use Case 1.3.5.1)<br/>
设备必须能够独立地验证软件和/或下载的数据的软件发起者的有效性。（用例1.3.5.1）
32. The Device MAY be able to verify, with the help of a Trusted Authority, the validity of the Software Originator of the Software and/or Data downloaded. (Use Case 1.3.5.1)<br/>
设备可以在受信任的机构的帮助下验证软件和/或下载的数据的软件发起者的有效性。（用例1.3.5.1）
33. The Device MUST be able to verify that the downloaded Software and/or Data is targeted to the Device. (Use Case 1.3.5.1) <br/>
设备必须能够验证下载的软件和/或数据是否针对设备。（用例1.3.5.1）
34. The Device SHALL send an inventory of its installed software to the Device Management Server. (Use Case 1.3.3.1)<br/>
设备必须将其安装的软件的清单发送到设备管理服务器。（用例1.3.3.1）
40. The Device SHALL receive the software update/upgrade. (Use Case 1.3.3.1)<br/>
设备必须接收软件更新/升级。（用例1.3.3.1）

#### 1.4.3.1.1 Interface to other Devices 与其它设备的接口
1. Data links between the Devices SHALL be over standardized, local and/or remote, wired and/or wireless bearers (e.g., Bluetooth, IR, USB, Ethernet, GPRS, etc.). (Use Case 1.3.1.1)<br/>
设备之间的数据链路必须通过标准化的，本地和/或远程的，有线和/或无线承载的（例如，蓝牙，IR，USB，以太网，GPRS等）。（用例1.3.1.1）
2. Protocols used SHALL be generally accepted and standardized (e.g. TCP/IP, http, https, Universal Plug and Play, etc) (Use Case 1.3.1.5)<br/>
使用的协议应该被普遍接受和标准化（例如TCP/IP, http, https，通用即插即用等）（用例1.3.1.5）

#### 1.4.3.1.2 Interface to Device Management Servers 设备管理服务器的接口
1. Data links between the Device Management Server and Devices SHALL be over standardized, local and/or remote, wired and/or wireless bearers (e.g., Bluetooth, IR, USB, Ethernet, GPRS, etc.). (Use Case 1.3.1.1,  1.3.1.3, 1.3.4.1)
设备管理服务器和设备之间的数据链路应当是通过标准化的，本地和/或远程，有线和/或无线承载（例如，蓝牙，IR，USB，以太网，GPRS等）。（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
2. Interface MUST support traversal of corporate firewalls and Network Address Translators (Use Case 1.3.1.2)<br/>
接口必须支持公司防火墙和网络地址转换器的穿越。（用例1.3.1.2）
3. Interface MUST be discoverable (Use Case 1.3.1.2)<br/>
接口必须是可发现的（用例1.3.1.2）
4. The Device Management Server MUST support secure connectivity via HTTPS. (Use Case 1.3.1.5)<br/>
设备管理服务器必须支持通过HTTPS的安全连接。（用例1.3.1.5）
5. Protocols used SHALL be generally accepted and standardized (e.g. TCP/IP, http, https, Universal Plug and Play, etc) (Use Case 1.3.1.5)<br/>
使用的协议应该被普遍接受和标准化（例如TCP/IP，http，https，通用即插即用等）（用例1.3.1.5）
7. The Device Management Server and the Device MUST be able to exchange their respective capabilities and select a set to be used for the download. (Use Case 1.3.5.1)
设备管理服务器和设备必须能够交换它们各自的能力并选择一组用于下载。（用例1.3.5.1）
8. The Device MUST be able to notify the server that it has accepted and successfully saved the downloaded software and/or data. (Use Case 1.3.5.1)
设备必须能够通知服务器它已经接受并成功保存了下载的软件和/或数据。（用例1.3.5.1）


### 1.4.3.2 Smart Card 智能卡
1. The Smart Card SHALL be capable of storing Management Objects (e.g., network address(es)). (Use Case 1.3.1.3)<br/>
智能卡必须能够存储管理对象（例如，网络地址）。（用例1.3.1.3）
2. The Smart Card SHALL be able to securely store authentication parameters, such keys, encryption mechanisms, etc. (Use Case 1.3.4.1)<br/>
智能卡必须能够安全地存储认证参数，例如密钥，加密机制等。（用例1.3.4.1）
3. The smart card MAY store data allowing the establishment of a secure connection to the Device Management Server (UC 1.3.1.4).<br/>
智能卡可以存储允许建立到设备管理服务器的安全连接的数据。（用例 1.3.1.4）
4. Device Management Server SHALL be capable of manipulating a Device’s Management object (Use Case 1.3.1.3)<br/>
设备管理服务器必须能够操纵设备的管理对象。（用例1.3.1.3）
5. The data tree for containing Device management objects on the Smart Card SHALL be capable of being modified (i.e., nodes or data fields added or deleted), read from, and/or written to. (Use Case 1.3.1.3)<br/>
用于存储智能卡上的设备管理对象的数据树必须能够被修改（即，添加或删除节点或数据字段），读取和/或写入。（用例1.3.1.3）
6. The Device Management Server SHALL be capable of manipulating a Management object resident on a Smart Card (Use Case 1.3.1.3)<br/>
设备管理服务器必须能够操作驻留在智能卡上的管理对象。（用例1.3.1.3）
7. Smart card SHALL provide mechanism that allows efficient detection of its DM structure. (UC 1.3.1.3)<br/>
智能卡必须提供允许有效检测其DM结构的机制。（用例 1.3.1.3）
8. If the Smart Card is present, the Smart Card MAY be used to ensure authenticity, integrity and non-repudiation of session between Device and DMS. (Use Case 1.3.4.1)<br/>
如果智能卡存在，智能卡可用于确保设备和DMS之间的会话的真实性，完整性和不可否认性。（用例1.3.4.1）
9. The Smart Card MAY be used to store data in a secure fashion. (Use Case 1.3.4.1)<br/>
智能卡可用于以安全的方式存储数据。（用例1.3.4.1）

#### 1.4.3.2.1 Interface to Device Management Servers 设备管理服务器的接口
1. The Device Management Server SHALL be able to establish a data link with a Smart Card installed in a Device. (Use Case 1.3.1.3)<br/>
设备管理服务器应能够与安装在设备中的智能卡建立数据链路。（用例1.3.1.3）

### 1.4.3.3 PC Agent PC代理
1. The PC agent SHALL to be able to support discovery of Devices so that it can identify those that should receive access rights to Devices in the local security domain. The PC MUST be able to authenticate and authorize further Device interaction. The PC is responsible for granting access rights to Devices under its control via the user's decision. (Use Case 1.3.1.5)<br/>
PC代理必须能够支持发现设备，以便它能够识别出应该接收对本地安全域中的设备的访问权限的那些设备。PC必须能够认证和授权进一步的设备交互。PC负责通过用户的决定授予对其控制下的设备的访问权限。（用例1.3.1.5）
2. The mapping from friendly name to network unique name SHALL be the function of each user’s user interface in the case where the Device is shared. (Use Case 1.3.1.5)<br/>
在设备共享的情况下，从友好名称到网络唯一名称的映射必须是每个用户的用户界面的功能。（用例1.3.1.5）
3. The PC agent SHALL be capable of launching the browser with an appropriate URL. (Use Case 1.3.1.5)<br/>
PC代理应能够使用适当的URL启动浏览器。（用例1.3.1.5）


#### 1.4.3.3.1 Interface to Devices 设备接口
1. Any interested PC Agent SHALL be capable of listening to the standard multicast address for notifications that new Devices are available. (Use Case 1.3.1.5)<br/>
任何感兴趣的PC代理必须能够监听用于新设备可用的通知的标准多播地址。（用例1.3.1.5）
2. Protocols used SHALL be generally accepted and standardized (e.g. TCP/IP, http, https, Universal Plug and Play, etc) (Use Case 1.3.1.5)<br/>
使用的协议应该被普遍接受和标准化（例如TCP / IP，http，https，通用即插即用等）（用例1.3.1.5）
3. Data links to Devices SHALL be over standardized, local and/or remote, wired and/or wireless bearers (e.g., Bluetooth, IR, USB, Ethernet, GPRS, etc.). (Use Case 1.3.1.5)<br/>
到设备的数据链路应通过标准化的，本地和/或远程的，有线和/或无线承载（例如，蓝牙，IR，USB，以太网，GPRS等）。（用例1.3.1.5）

### 1.4.3.3 Overall Device Management Server 整体设备管理服务器
1. The Device Management Server SHALL be capable of discovering the presence of nearby, active Device Management clients if those elements are using compatible local bearers. (Use Case 1.3.1.1)<br/>
如果这些元件使用兼容的本地承载，则设备管理服务器应该能够发现附近的活动设备管理客户端的存在。（用例1.3.1.1）
2. The Device Management Server SHALL support mutual authentication with the Device. (Use Case 1.3.1.1,  1.3.1.3,  1.3.4.1)<br/>
设备管理服务器必须支持与设备的相互身份验证。 （用例1.3.1.1, 1.3.1.3, 1.3.4.1）
3. The Device Management Server SHALL be capable of querying Devices for information about Device properties, configuration, and capabilities. (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
设备管理服务器必须能够查询设备以获取有关设备属性的信息，配置和功能。 （用例1.3.1.1, 1.3.1.3, 1.3.4.1）
4. The Device Management Server SHALL be capable of querying the Smart Card for information about Device properties, configuration, and capabilities. (Use Case 1.3.1.3)<br/>
设备管理服务器必须能够查询智能卡有关设备属性，配置和功能的信息。 （用例1.3.1.3）
5. The Device Management Server SHALL be capable of manipulating a Device’s Device Management Object. (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
设备管理服务器必须能够操纵设备的设备管理对象。（用例1.3.1.1, 1.3.1.3, 1.3.4.1）
6. The Device Management Server SHALL be capable of manipulating a Management Object resident on a Smart Card. (Use Case 1.3.1.3)<br/>
设备管理服务器必须能够操纵智能卡上驻留的管理对象。（用例1.3.1.3）
7. The Device Management Server SHALL be capable of capable of add/deleting/editing the fields of the Device’s Device Management Object. (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
设备管理服务器必须能够添加/删除/编辑设备的设备管理对象的字段。 （用例1.3.1.1, 1.3.1.3, 1.3.4.1）
8. The Device Management Server SHALL be capable of add/deleting/editing the values of the Management Object present on a Smart Card. (Use Case 1.3.1.3)<br/>
设备管理服务器必须能够添加/删除/编辑智能卡上存在的管理对象的值。（用例1.3.1.3）
9. The message from the Device acknowledging a device management operation SHALL contain an indication of success/failure of the operation. (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
来自设备确认的设备管理操作的消息必须包含操作成功/失败的指示。 （用例1.3.1.1, 1.3.1.3, 1.3.4.1）
10. The Message from the Device acknowledging a device management operation SHALL contain an indication of success/failure of the operation. (Use Case 1.3.1.3)<br/>
来自设备确认的设备管理操作的消息必须包含操作成功/失败的指示。 （用例1.3.1.3）
11. The DM Server SHALL be capable of sending a request for User confirmation to the Device, and accepting the response from the Device. (Use Case 1.3.4.1)<br/>
DM服务器必须能够向设备发送用户确认的请求，并且接受来自设备的响应。（用例1.3.4.1）
12. The DMS SHOULD be capable of receiving fault messages from a Device, and if supported the DMS SHALL provide a standardized mechanism for publishing the messages. (Use Case 1.3.4.1)<br/>
推荐DMS能够从设备接收故障消息，并且如果支持，DMS应当提供用于发布消息的标准化机制。（用例1.3.4.1）
13. The management server SHOULD be able to poll devices for faults. (Use Case 1.3.4.1)<br/>
推荐管理服务器能够轮询设备的故障。（用例1.3.4.1）
14. The Device Management Server SHALL be able to establish a secure data connection to the Device. (UC 1.3.1.3, 1.3.1.4, 1.3.2.1)<br/>
设备管理服务器必须能够建立到设备的安全数据连接。（用例 1.3.1.3, 1.3.1.4, 1.3.2.1）
15. The Device Management Server SHALL support group addressing of Devices in order to transfer the changed management objects for them. (UC 1.3.2.1)<br/>
设备管理服务器应必须支持设备的组寻址，以便为其传输更改的管理对象。（用例 1.3.2.1）
16. For the Device Management Server to be able to differentiate between the new and current configuration of a Device, Management Object data definitions SHALL specify canonical value representations and associated rules for unambiguous comparison. (UC 1.3.2.1)<br/>
为了使设备管理服务器能够区分设备的新配置和当前配置，管理对象数据定义必须指定规范值表示和相关规则以进行明确比较。（用例 1.3.2.1）
17. Management Object data definitions SHOULD be composed from a common set of basic data types rather than by specifying new data types.<br/>
推荐管理对象数据定义由一组通用的基本数据类型组成，而不是通过指定新的数据类型。
18. The Device Management Server SHOULD support at least one wireless data bearer. (Use Case 1.3.4.1)<br/>
推荐设备管理服务器支持至少一个无线数据承载。（用例1.3.4.1）
19. The Device Management transactions SHOULD be annotated with sufficient information to enable the Device Management Server to detect the lack of response of Device in a specified time interval. (Use Case 1.3.4.1)<br/>
推荐设备管理事务注明足够的信息来启用设备管理服务器在指定时间间隔内检测设备的响应不足。（用例1.3.4.1）
21. The Device Management Server MUST report errors in a standardized format. (Use Case 1.3.4.1)<br/>
设备管理服务器必须以标准格式报告错误。（用例1.3.4.1）
22. The Device Management Server MUST verify integrity of data prior to download to Device. (Use Case 1.3.4.1)<br/>
设备管理服务器必须在下载到设备之前验证数据的完整性。（用例1.3.4.1）
23. The Device Management Server MUST be able to verify that software and/or data is from an approved Software Originator or agent thereof. (Use Case 1.3.5.1)<br/>
设备管理服务器必须能够验证软件和/或数据来自已批准的软件发起方或其代理。（用例1.3.5.1）
24. The Device Management Server MUST be able to detect when a Device that needs a software and/or data update. (Use Case 1.3.5.1)<br/>
设备管理服务器必须能够检测何时设备需要软件和/或数据的更新。（用例1.3.5.1）
25. The Device Management Server MUST be capable of determining that the Device is authorized to receive the software and/or Data. (Use Case 1.3.5.1)<br/>
设备管理服务器必须能够确定设备被授权接收软件和/或数据。（用例1.3.5.1）
26. The Device Management Server MUST be capable of interrogating the Device as to its capabilities and to determine from this information if the Device is capable of receiving the software/data download using a mutually agreed upon method and format. (Use Case 1.3.5.1)<br/>
设备管理服务器必须能够向设备询问其能力，并且根据该信息确定设备是否能够使用相互同意的方法和格式来接收软件/数据下载。（用例1.3.5.1）
27. The Device Management Server MUST be capable of exchanging security credentials with the Device. (Use Case 1.3.5.1) <br/>
设备管理服务器必须能够与设备交换安全凭证。（用例1.3.5.1）
28. The Device Management Server MUST be capable of transmitting the software and/or data to the Device. (Use Case 1.3.5.1)<br/>
设备管理服务器必须能够向设备发送软件和/或数据。（用例1.3.5.1）
29. The Device Management Server SHOULD be able to verify, either independently or with the help of a Trusted Authority, the validity of the Software Originator of the Software and/or Data to be downloaded. (Use Case 1.3.5.1)<br/>
推荐设备管理服务器能够独立地或在可信授权机构的帮助下验证要下载的软件和/或数据的软件发起者的有效性。（用例1.3.5.1）
30. The Device Management Server SHOULD be able to verify that the downloaded Software and/or Data is targeted to a particular Device. (Use Case 1.3.5.1)<br/>
推荐设备管理服务器能够验证所下载的软件和/或数据是否针对特定设备。（用例1.3.5.1）
32. The Device Management Server SHALL be able to query a Device for an inventory of its installed software.<br/>
设备管理服务器必须能够向设备查询其安装的软件的清单。
33. The Device Management Server SHALL support group addressing of Devices in order to query multiple Devices for the purposes of a common update/upgrade to those Devices. (Use Case 1.3.3.1)<br/>
设备管理服务器必须支持设备的组寻址，以便查询多个设备以对这些设备进行常见更新/升级。（用例1.3.3.1）
34. The software inventory reported from the Device SHALL be in standardised format. (Use Case 1.3.3.1)<br/>
从设备报告的软件清单必须采用标准化格式。（用例1.3.3.1）

#### 1.4.3.4.1 Interface to Devices 设备接口
1. Data links between the Device Management Server and Devices SHALL be over standardized, local and/or remote, wired and/or wireless bearers (e.g., Bluetooth, IR, USB, Ethernet, GPRS, etc.). (Use Case 1.3.1.1, 1.3.1.3, 1.3.4.1)<br/>
设备管理服务器和设备之间的数据链路必须是通过标准化的，本地和/或远程的，有线和/或无线承载（例如，蓝牙，IR，USB，以太网，GPRS等）。 （用例1.3.1.1,1.3.1.3,1.3.4.1
2. Network/Device Management Server SHALL be capable to discover a new combination of Subscriber and Device attached in the Network (UC 1.3.1.4).<br/>
网络/设备管理服务器必须够发现网络中附加的订户和设备的新组合（用例 1.3.1.4）。
3. Interface supports traversal of corporate firewalls and Network Address Translators (Use Case 1.3.1.2) <br/>
接口支持公司防火墙和网络地址转换器的穿越（用例1.3.1.2）
4. The DMS MUST support secure connectivity via HTTPS. (Use Case 1.3.1.5)
DMS必须支持通过HTTPS的安全连接。（用例1.3.1.5）
5. Protocols used SHALL be generally accepted and standardized (e.g. TCP/IP, http, https, Universal Plug and Play, etc) (Use Case 1.3.1.5)<br/>
使用的协议必须被普遍接受和标准化（例如TCP / IP，http，https，通用即插即用等）（用例1.3.1.5）
7. The Device Management Server and the Device MUST be able to exchange their respective capabilities and select a set to be used for the download. (Use Case 1.3.5.1)<br/>
设备管理服务器和设备必须能够交换它们各自的能力并选择一组用于下载。（用例1.3.5.1）
9. The Device Management Server MUST be able to process the response from the Device indicating the success or failure of the download. (Use Case 1.3.5.1)<br/>
设备管理服务器必须能够处理来自设备的指示下载成功或失败的响应。（用例1.3.5.1）

#### 1.4.3.4.2 Interface to other Device Management Servers 与其他设备管理服务器的接口
1. Interface SHALL support traversal of corporate firewalls and Network Address Translators (Use Case 1.3.1.2)<br/>
接口必须支持公司防火墙和网络地址转换器的遍历（用例1.3.1.2）
2. Interface SHALL be discoverable (Use Case 1.3.1.2)<br/>
接口必须可以被发现（用例1.3.1.2）
3. The Device Management Server MUST support secure connectivity via HTTPS. (Use Case 1.3.1.5)<br/>
设备管理服务器必须支持通过HTTPS的安全连接。（用例1.3.1.5）
4. The Device Management Server SHALL expose a standard interface for obtaining Network parameters (Use Case 1.3.1.2)<br/>
设备管理服务器必须提供用于获取网络参数的标准接口（用例1.3.1.2）

#### 1.4.3.4.3 Interface to External 外部接口
1. Device Management Server SHALL provide an interface for receiving subscriber data remotely, which is needed to identify the Device or smart card of new subscriber. (UC 1.3.1.3)<br/>
设备管理服务器必须提供用于远程接收用户数据的接口，其需要识别新用户的设备或智能卡。（用例 1.3.1.3）
2. Device Management Server SHALL provide an interface that allows the user to trigger the transfer of configuration data (UC 1.3.1.4).<br/>
设备管理服务器必须提供一个允许用户触发配置数据传输的接口。（用例 1.3.1.4）
3. Device Management Server SHALL provide an interface that allows the Management Authority to initiate the transfer of (updated) configuration data. (UC 1.3.2.1)<br/>
设备管理服务器应提供一个接口，允许管理机构启动（更新的）配置数据的传输。（用例 1.3.2.1）

### 1.4.3.3 Network Interfaces 网络接口

Requirements covered in other sections.<br/>
需求已在其他部分描述。