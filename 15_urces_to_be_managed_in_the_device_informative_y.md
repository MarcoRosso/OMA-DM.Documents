# 1.5 urces to be managed in the Device (Informative) 要在设备中管理的信息（资料性）

This section provides an overview of the resources which are candidates for being managed using the Device Management mechanism. Categories of parameters and the parameters themselves that are listed in association with a resource are informative only – they are meant to provide guidance, and are not an exhaustive list of required parameters for particular capabilities, applications, or other Device characteristics.<br/>
本节概述了使用设备管理机制管理的资源。与资源相关联列出的参数类别和参数本身仅是信息性的 - 它们旨在提供指导，并且不是用于特定能力，应用或其他设备特性的所需参数的详尽列表。

There may be some special conditions or expectations around the presence, access, or manipulation of managed resources that should be taken into account when defining parameters and some of those conditions are noted here:<br/>
围绕被管理资源的存在，访问或操作可能有的一些特殊条件或期望，在定义参数时应该考虑这些条件或期望，并且在这里注意到这些条件中的一些：

Note that not all resources may be available at a given time depending on a number of factors, such as the presence of accessories or permissions associated with a resource. For example, in Devices with a smart card, some parts of the resources managed in the Device may be specific to a certain IMSI, for example the username & password associated with a bearer. These shall only be active if the specified IMSI is inserted in the Device.<br/>
注意，并非所有资源在给定时间都可用，这取决于多个因素，诸如与资源相关联的附件或许可的存在。例如，在具有智能卡的设备中，在设备中管理的资源的一部分可能特定于某个IMSI，例如与承载相关联的用户名和密码。只有在设备中插入指定的IMSI时，它们才会处于活动状态。

Time-sensitive resources shall be noted as such and their configurability specified such that it is possible to ascertain when such settings apply. For instance, some settings may have one or more time periods with distinct start and stop clock times. Other such settings may only be active for a period measured by cumulative use.<br/>
对时间敏感的资源应该这样注意，指定其可配置性，确定何时应用这些设置。例如，一些设置只应用于一个或多个不同的时间段，它们拥有不同的开始和停止时间。其他此类设置只能在通过累计使用时间来决定是否处于活动状态。

For operationally critical resources it shall be possible to locally or remotely revert the handset back to using a previously working value of the resources, should the new settings fail (e.g. software defined radio). Critical resources should be supported by adequate fault management on or off the Device as appropriate.<br/>
对于操作上关键的资源，如果新的设置失败（例如软件定义的无线电），则可以本地或远程地将手机恢复到使用该资源前的工作状态。关键资源的使用与否应通过适当的设备上的故障管理来支持。

Management data may be set originally by OMA bootstrap methods, then read and maintained via Device Management. Subsequent to booting, resources may be created, added, deleted, or modified in accordance with any implementation of Device Management or OA&M mechanisms.<br/>
管理数据可以由OMA引导方法最初设置，然后通过设备管理读取和维护。在引导之后，可以根据设备管理或OA＆M机制的任何实现来创建，添加，删除或修改资源。

## 1.5.1 Applications Requiring Managed Resources 需要管理资源的应用程序
Following is a non-exhaustive list of common mobile applications that are expected to be supported by managed resources. The list of applications may be appended and special requirements pertaining to their managed resources may be noted in this section. However, the categories of managed resources presented in a subsequent section are intended to be applicable to the Applications listed here as well as additional applications that are added. The addition or modification of managed resource parameters should reference back to specific applications or use cases as presented in this document. The current list of Applications are:<br/>
以下是预期受管资源支持的常见移动应用程序的非详尽列表。 该列表可以增加，并且其与管理资源有关的特殊要求在本节中可以注明。 但是，后续章节中提供的管理资源类别旨在适用于此处列出的应用程序以及添加的其他应用程序。 管理资源参数的添加或修改应参考本文档中介绍的特定应用程序或用例。 当前应用程序列表是：

* Multi-Media Messaging Service 多媒体消息
* E-mail 电子邮件
* Instant Messaging 即时消息
* Internet Browser 网络浏览器
* Device Synchronization 设备同步
* Device Management Agents 设备管理代理

## 1.5.2 Application and Service Resource Categories 应用程序和服务资源类别
The categories of Managed Resources required by some or all of these Applications are detailed in this section and are comprised of:<br/>
这些部分或全部应用程序所需的管理资源类别在本节中详细介绍，包括：

* Connectivity 连接
* Device Physical 物理设备
* Security 安全
* Performance 性能
* Billing 计费
* User Preferences & Customization 用户首选项和自定义
* Other 其它

In the following tables the Default Actor “Management Authority” is abbreviated MA. <br/>
在下面的表中，默认动作者“管理权限”缩写为MA。

Change Policy has generic settings as follows:<br/>
更改策略具有如下的通用设置：

Without Authorization, implying no or weak authentication. Usually applies to User or Subscriber modifiable resources – abbreviated W/O A<br/>
没有授权，意味着没有或较弱的身份验证。通常适用于用户或订户可修改的资源（缩写为W/O A）
  
With Authorization, implying data integrity required, authentication with cryptographic means. Usually associated with Network or Service Provider Management Authorities, Enterprise/IT Administrators, or other MA Delegates. – abbreviated W/A<br/>
使用授权，意味着需要数据完整性，使用加密方法进行身份验证。通常与网络或服务提供商管理机构，企业/IT管理员或其他MA代表相关联。-缩写为W/A
  
Unknown (which may mean it’s ambiguous) – abbreviated Unk<br/>
未知（这可能意味着它的模棱两可） -缩写Unk

![](r01.jpeg)
![](r02.jpeg)
### 1.5.2.1 Application Data Resources 应用数据资源
| Resource 资源 | Parameters 参数 | Default Actor 默认参与者| Change Policy (Easy, Hard, Unknown) 更改政策（简单，困难，未知） | Notes 备注|
| -- | -- | -- | -- | -- |
| Device Management settings<br/> 设备管理设置 | TBD | MA | W/A |  |
| Data Synchronization settings<br/> 数据同步设置 | Application Service Access Point<br/>应用程序服务访问点<br/>Server Name<br/>服务器名称<br/>Access Point Link<br/>接入点链路<br/>Proxy Information Link<br/>代理信息链接 | User, Subscriber 用户，订户 | W/O A |  |

### 1.5.2.2 Connectivity 连接性
The following resources are mainly based on the OMA client provisioning data.<br/>
以下资源主要基于OMA客户端配置数据。

| Resource 资源 | Parameters 参数 | Default Actor 默认参与者| Change Policy  更改政策| Notes 备注|
| -- | -- | -- | -- | -- |
| Supported packet bearer settings - The information model associated with GPRS bearer settings is described in the OMA client provisioning Network Access Point parameter, for the case where the bearer relates to GPRS.<br/> 支持的分组承载设置 - 在承载与GPRS相关的情况下，在OMA客户端配置网络接入点参数中描述与GPRS承载设置相关联的信息模型。| Packet Bearer (e.g. GPRS, SMS, ...)<br/>分 组承载（例如GPRS，SMS，...）| MA | W/A |The management authority may, for example, use this object to modify or add an APN definition in the Device.<br/> 管理权限可以使用此对象来修改或在设备中添加APN定义。|
| Circuit switched data settings - The information model associated with circuit switched data settings is described in the OMA client provisioning Network Access Point parameter, for the case where the bearer relates to circuit switched data.<br/>电路交换数据设置 - 在承载涉及电路交换数据的情况下，在OMA客户端配置网络接入点参数中描述与电路交换数据设置相关联的信息模型。 |  | MA | W/A |  |
| Proxy settings - The information model associated with this resource is described in the OMA client provisioning PXLOGICAL parameter.<br/>代理设置-与此资源关联的信息模型在OMA客户端配置PXLOGICAL参数中描述。 | WAP Gateway<br/>WAP网关 | MA | W/A |  |
| Application connectivity data - Application-specific protocol connectivity parameters are specified in Sec.1.5.2.1<br/>应用程序连接数据-特定于应用程序的协议连接参数在1.5.2.1节 | Application Service Access Point (address and port), Bearer, Server Name, Access Point Information Link, Proxy Information Link, URI Domain<br/>应用服务接入点（地址和端口），承载，服务器名称，接入点信息链路，代理信息链路，URI域 | MA | W/A | The Device may support fallback connectivity parameters in case the preferred connectivity profile fails. (See OMA- REQ-2002-0078, LS from MSIG).For any combination of: (a) application, (b) port number and (c) requested URI domain it shall be possible to specify the network access point (including bearer) and/or proxy to be used.Reference the information model in the OMA client provisioning APPLICATIONand ACCESS parameters.<br/>在优选连接性配置文件失败的情况下，设备可以支持回退连接参数。（参见OMA-REQ-2002-0078，来自MSIG的LS）。对于（a）应用，（b）端口号和（c）请求的URI域的任何组合，应当可以指定要使用的网络接入点（包括承载）和/或代理。在OMA客户端配置APPLICATION和ACCESS参数中引用信息模型。|

### 1.5.2.3 Device Physical 设备物理
| Resource 资源 | Parameters 参数 | Default Actor 默认参与者| Change Policy  更改政策| Notes 备注|
| -- | -- | -- | -- | -- |
| Device information - Device information gives a view on the parameters which identify and describe the Device.<br/> 设备信息 - 设备信息提供了识别和描述设备的参数视图。 | Device Make, Device Model, OS Version, Memory Configuration, Display Characteristics, IMEI, IMSI, Phone Number, Connectivity Supported (e.g. GPRS, BlueTooth, 802.11x, etc.), Current Connectivity <br/> 设备品牌，设备型号，操作系统版本，存储器配置，显示特性，IMEI，IMSI，电话号码，支持的连接（例如GPRS，蓝牙，802.11x等）| MA | Unknown | Reference existing Device information management object defined by SyncML.<br/> 引用由SyncML定义的现有设备信息管理对象。 |
| Time and Date - Needed to allow authorised parties to set the time and date on behalf of the customer.<br/>时间和日期 - 需要允许授权方代表客户设置时间和日期。 | Time Zone,Time,Time Format,Date,Date Format<br/>时区，时间，时间格式，日期，日期格式 | MA, User | W/A, W/O A? | Useful in those cases where network identification and time zone is not supported by the visited network.<br/>在受访网络不支持网络标识和时区的情况下很有用。 |
| Peripheral Profile - List of peripheral support and their current usage<br/>外设配置文件 - 外设支持列表及其当前使用情况 | Peripheral List, Usage <br/>  外设列表，用法 | MA, User | W/A, W/O A |  |

### 1.5.2.4 Security 安全
Security Resources listed here are assumed to be generic, Device-wide attributes, whereas it is presumed that any Device Management system will define security models for the manipulation of the actual managed objects representing the resources.<br/>
此处列出的安全资源假定为通用的设备范围属性，而假定任何设备管理系统将定义用于操纵代表资源的实际受管对象的安全模型。

| Resource 资源 | Parameters 参数 | Default Actor 默认参与者| Change Policy  更改政策| Notes 备注|
| -- | -- | -- | -- | -- |
| Certificate – A list of parameters that are required in order to provision the Device with security certificates: <br/> 证书 - 为设备配置安全证书所需的参数列表：| Base64 Encoded Certificate, Certificate hash (used as the ID to identify the cert), Private key (If it is a client cert, the private key of the cert need to be specified separately when being transmitted to the Device together with the certificate), Owner (define who logically own this certificate, operator, corp, end user, etc), Certificate category (specify whether this is a root cert, a cert for application execution, a personal cert, etc)<br/> Base64编码证书，证书哈希（用作ID来标识证书），私钥（如果是客户端证书，当与证书一起传输到设备时，需要单独指定证书的私钥），所有者（定义谁在逻辑上拥有此证书，运营商，公司，最终用户等），证书类别（指定这是根证书，应用程序执行的证书，个人证书等） | MA | W/A | -- |
| Keys - One or more keys as required by Device, Applications, or Management Authority in general <br/> 密钥 - 设备，应用程序或管理机构一般要求的一个或多个密钥 |  | MA | W/A | Separate keys per usage are possible.<br/> 可以单独使用每个密匙。 |
| Cryptographic Algorithms - Available cryptographic algorithms (and specification of how to access them)<br/>加密算法 - 可用的加密算法（以及如何访问它们的规范） | Crypto Algorithm List<br/>加密算法列表 | MA | W/A | |
| Trust Levels - Specification of the available trust level available and/or desired on the Device as a whole, useful for authentication choices <br/> 信任级别 - 在整个设备上可用和/或期望的可用信任级别的规范，对于认证选择是有用的 | Available Trust Levels, Current Trust Level<br/> 可用的信任级别，当前信任级别 | MA | W/A |  |
| Hardware Security Support - Identification of non-software security support, such as a built-in random number generator<br/>硬件安全支持 - 识别非软件安全支持，例如内置的随机数生成器 | Hardware Security List<br> 硬件安全列表| MA | W/A | Some question about how this may map to other Security parameters such as Trust Level (what does it enable?)<br/> 一些问题，如何将这映射到其他安全参数，如信任级别（它启用了什么？） |
| Authentication Profile - Authentication is used to verify the identity of the user or application. Base resource to be re-used by Applications, Services, or protocols. Multiple authentication mechanisms and associated parameters are anticipated.<br/> 认证配置文件 - 认证用于验证用户或应用程序的身份。要由应用程序，服务或协议重用的基本资源。预期多种认证机制和相关参数。| Authentication level (specify the authentication is for which layer: app layer, transport layer, etc),Authentication Protocol (specify the auth protocol, such as Kerberos v5, NTLM, RADIUS, EAP, HTTP BASIC Auth, etc Note: different layer could have different auth protocols.<br/>认证级别（指定认证是针对哪个层：应用层，传输层等），认证协议（指定认证协议，如Kerberos v5，NTLM，RADIUS，EAP，HTTP BASIC Auth等。 注意：不同层有不同认证协议。 | MA | W/A | -- |
| Policy - Policies around how the security features of the Device are used. For instance, what level of trust is required for certain transactions or for different connections.<br/> 策略 - 关于如何使用设备的安全功能的策略。 例如，某些事务或不同连接需要什么级别的信任。 |Trust Policy,Transaction Policy,Updates Policy, Connections Policy<br/>信任政策，事务策略，更新策略，连接策略| MA, User | W/A |  |
| Authorization and Access Control – covers access to other resources at various levels in Device Management from applications and services to the managed resources themselves<br/>授权和访问控制 - 涵盖设备管理的从应用程序和服务到被管理资源本身各个级别的其他资源的访问 | Managed Resource ACLs, White List, Black List<br/>托管资源ACL，白名单，黑名单 | MA | W/A | For particular applications there may be the need to allow (whitelist) or block (blacklist) connections explicitly, e.g. allowing only a predefined SMSC sender number for WAP Push.<br/>对于特定应用，可能需要明确地允许（白名单）或阻塞（黑名单）连接，例如， 仅允许用于WAP推送的预定义SMSC发送者号码。 |

### 1.5.2.5 Performance 性能
Performance measurements can take multiple forms. For example, they may be high or low-water marks, accumulators, discrete samples, etc.<br/>
性能测量可以采取多种形式。例如，它们可以是高或低水印，累积器，离散样品等。

| Resource 资源 | Parameters 参数 | Default Actor 默认参与者| Change Policy  更改政策| Notes 备注|
| -- | -- | -- | -- | -- |
| Alarm Log - Reports on recent Device alarms<br/>报警日志 - 报告最近的设备报警 | Log ID, Subscribers, Policy, Enabled Flag, Reports<br/>日志ID，订阅者，策略，启用标志，报告 | MA | W/A | Local policy may be defined to account for retention or storage limits.<br/>可以定义本地策略以考虑保留或存储限制。 |
| Fault Log - Reports on recent Device faults<br/>故障日志 - 报告最近的设备故障 | Log ID, Subscribers, Policy, Enabled Flag, Reports, Severity Counts, Metrics<br/>日志ID，订阅者，策略，启用标志，报告，严重性计数，指标 | MA | W/A | Local policy may be defined to account for retention or storage limits.<br/> 可以定义本地策略以考虑保留或存储限制。|
| Connectivity Bandwidth<br/>连接带宽 | Unit of Measure, Available,Preferred, Actual<br/>计量单位，可用，优先，实际 | MA | W/A |  |
| Traffic Load - Measurement(s) of network activity (bytes, packets, etc.)<br/>流量负载 - 网络活动的测量（字节，数据包等） |Unit of measure (bytes, packets, ...), Current Load, Historical Load, Dropped Packets<br/>计量单位（字节，数据包，...），当前负载，历史负载，丢弃的数据包 | MA | W/A |  |
| Application Load - Measurement indicating relative application usage of the Device<br/>应用程序负载 - 指示设备的相对应用程序使用量的测量 | Number of Apps, Processor Utilization<br/>应用程序数量，处理器利用率 | MA | W/A |  |
| Policy - One or more policies governing performance monitoring or acquisition<br/>策略 - 一个或多个管理性能监控或采集的策略 | Schedules, Sample Rates, Logging Policy<br/>时间表，采样率，记录策略 | MA | W/A |  |