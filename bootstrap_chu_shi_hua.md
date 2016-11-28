# Bootstrap 初始化
Other OMA DM specifications define how a management session is established and maintained. However, in order for a device to be able to initiate a management session it must be provisioned with OMA DM settings.<br/>
其他OMA DM规范定义了如何建立和维护管理会话。 但是，为了使设备能够发起管理会话，必须使用OMA DM设置进行设置。

Bootstrap is a process of provisioning the DM client to a state where it is able to initiate a management session to a new DM server. Bootstrap can move a device from an un-provisioned, empty state, to a state where it is able to initiate a management session to a DM server. DM clients that have already been bootstrapped can be further bootstrapped to enable the device to initiate a management session to new DM servers.<br/>
引导是将DM客户端配置到能够向新的DM服务器发起管理会话的状态的过程。初始化可以将设备从未设置的空状态引导到其能够发起到DM服务器的管理会话的状态。已经被初始化的DM客户端可以被进一步引导以使得设备能够发起到新的DM服务器的管理会话。

##Definitions 定义
See the DM Tree and Description [DMTND] document for definitions of terms related to the management tree.<br/>有
关与管理树相关的术语的定义，请参阅DM树和说明[DMTND]文档。

2G UICC: UICC activated in a 2G mode that has physical characteristics of UICC [TS102.221] but logical characteristics of SIM [151.011].<br/>
2G UIUC: UICC在具有UICC的物理特性[TS102.221]但是SIM的逻辑特性[151.011]的2G模式中激活。

3G UICC: UICC activated in a 3G mode that has physical and logical characteristics of the UICC [TS102.221].<br/>
3G UICC: UICC在具有UICC[TS102.221]的物理和逻辑特性的3G模式中激活。

ADM:Access condition to an EF which is under the control of the authority which creates this file.<br/>
ADM: 对创建此文件的权限控制下的EF的访问条件。

Application:The implementation of a well-defined and related set of functions that perform useful work on behalf of the user. It may consist of software and or hardware elements and associated user interfaces.<br/>
应用：一个定义良好的相关函数集的实现，代表用户执行有用的工作。它可以包括软件和/或硬件元件和相关联的用户接口。

Application Identifier: A data element that identifies an application in a smartcard. An application identifier may contain a registered application provider number in which case it is a unique identification for the application. If it contains no application provider number, then this identification may be ambiguous.<br/>
应用程序标识符：标识智能卡中的应用程序的数据元素。应用标识符可以包含注册的应用提供商号码，在这种情况下，它是应用的唯一标识。如果它不包含应用程序提供者号码，则该标识可能是不明确的。<br/>

Authentication: Authentication is the process of ascertaining the validity of either the Device or the Device Management Server’s identity.<br/>
认证：认证是确定设备或设备管理服务器的身份的有效性的过程。

Binary Files: Binary Files are equivalent to transparent files as described in [TS102.221].<br/>
二进制文件：二进制文件等同于[TS102.221]中所述的透明文件。

Bootstrap: The process of provisioning the DM client to a state where it is able to initiate a management session to a new DM server.<br/>
初始化：将DM客户端配置为能够向新的DM服务器发起管理会话的状态的过程。

Card Issuer: The organization or entity that owns and provides a smartcard product.<br/>
卡发行商：拥有并提供智能卡产品的组织或实体。

Cardholder：The person or entity presenting a smartcard for uses.<br/>
持卡人：提供智能卡以供使用的个人或实体。

Cardholder Verification:Also called the PIN. Typically a 4 to 8 digit number entered by the cardholder to verify that the cardholder is authorized to use the card.<br/> 
持卡人验证: 也称为PIN。通常由持卡人输入的4到8位数字号码来验证持卡人是否有权使用卡。

Command: A message sent by the ME to the smartcard that initiates an action and solicits a response from the smartcard.<br/>
命令：ME发送到智能卡的消息，该消息发起动作并请求来自智能卡的响应。

Content: Content means data delivered inside of OMA DM messages `<Data>`-elements.<br/>
内容：内容指着在OMA DM消息`<Data>`元素内传递的数据。


Data Object Directory Files: Contain directories of data objects (not keys or certificates) ([PKCS#15], section 6.7) known to the PKCS#15 application.<br/>
数据对象目录文件：包含PKCS＃15应用程序已知的数据对象（不是密钥或证书）的目录（[PKCS＃15]，第3.2.7节）。

Dedicated File: A file containing access conditions and, optionally, Elementary Files (EFs) or other Dedicated Files.<br/>
专用文件: 包含访问条件和可选的基本文件（EF）或其他专用文件的文件。

Device: The Device is, or is to become managed by one or more remote entities (Device Management Servers). A device may have many characteristics, and many parameters may be made available for reading, writing, deleting and modifying by a Device Management Server.<br/>
设备：设备是或将由一个或多个远程实体（设备管理服务器）管理。 设备可以具有许多特性，并且许多参数可以被设备管理服务器用于读取，写入，删除和修改。

Device Management Server: The Device Management Server is an entity that is responsible for maintaining one or more Devices, in whole or in part. Its role is to facilitate the easy maintenance of a Device.<br/>
设备管理服务器：设备管理服务器是负责整体或部分地维护一个或多个设备的实体。它的作用是方便设备的轻松维护。

Elementary File: A set of data units or records that share the same identifier. It cannot be a parent of another file.<br/>
基本文件：共享相同标识符的一组数据单元或记录。它不能是另一个文件的父级。

File Identifier: A 2-byte binary value used to address a file on a smartcard.<br/>
文件标识符：用于对智能卡上的文件进行寻址的2字节二进制值。

Management Session: A continuous connection between the Device and the Device Management Server established for the purpose of carrying out one or more device management operations.<br/>
管理会话：在设备和设备管理服务器之间建立用于执行一个或多个设备管理操作的连续连接。

Object Directory File: The mandatory Object Directory File ([PKCS#15], section 3.2.2) consists of pointers to other EFs, each one containing a directory over PKCS#15 objects of a particular class (here and below, a “directory” means a list of objects).<br/>
对象目录文件：强制的对象目录文件（[PKCS＃15]，第3.2.2节）包含指向其他EF的指针，每个指针包含一个特定类的PKCS＃15对象的目录（这里和以下内容，“目录”都指对象的列表）。

Path: Concatenation of file identifiers without delimitation. The Path type is defined in [ISO7816-4] sub-clause 5.1.2. If the path starts with the MF identifier (0x3F00), it is an absolute path; otherwise it is a relative path. A relative path must start with the identifier of the current DF (or with the identifier '0x3FFF').<br/>
路径：不带分隔符的文件标识符的连接。路径类型在[ISO7816-4]子句5.1.2中定义。如果路径以MF标识符（0x3F00）开头，则它是绝对路径; 否则为相对路径。相对路径必须以当前DF的标识符（或标识符“0x3FFF”）开头。

Record: A string of bytes within an EF handled as a single entity.<br/>
纪录：EF中的字节串作为单个实体的处理。

Smartcard: A device with an embedded microprocessor chip. A smartcard is used for storing data and performing typically security related (cryptographic) operations. A smartcard may be the SIM, the UICC, the R-UIM or a smartcard used in a secondary smartcard reader of a device.<br/>
智能卡：具有嵌入式微处理器芯片的器件。智能卡用于存储数据和典型地执行与安全相关的（加密）操作。智能卡可以是SIM，UICC，R-UIM或在设备的智能卡读取器中使用的智能卡。

UICC: A physically secure device, an IC card (or smartcard), that can be inserted and removed from the device. It may contain one or more applications [TS102.221].<br/>
UICC：物理安全设备，IC卡（或智能卡），可以插入设备或从设备中移除。它可以包含一个或多个应用程序[TS102.221]。

##Abbreviaitons 缩写
2G Second generation network i.e. GSM 第二代通信网络如GSM

3G Third generation network i.e. UMTS 第三代通信网络如UMTS

ADF Application Dedicated File 应用程序专用文件

AID Application Identifier 应用程序标识符

ALW Always. Access condition indicating a given function is always accessible. 总是。指示给定功能的访问条件为始终可访问。

CHV Cardholder Verification 持卡人验证

DF Dedicated File 专用文件

DIR Directory File 目录文件

DM Device Management 设备管理

DODF Data Object Directory Files 数据对象目录文件

EF Elementary File 基本文件

FCP File Control Parameter 文件控制参数

IC Integrated Circuit 集成电路

ID Identifier 标识符

MAC Message Authentication Code 消息验证码

ME Mobile Equipment 移动设备

MF Master File 主文件

ODF Object Directory File 对象目录文件

OID Object Identifier 对象标识符

OMA Open Mobile Alliance 开放移动联盟

PIN Personal Identification Number 个人身份识别码

SIM GSM Subscriber Identity Module GSM用户识别模块 

WAP Wireless Application Protocol 无线应用协议



