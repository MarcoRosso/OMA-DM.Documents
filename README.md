# OMA Device Management

Approved Version 1.2.1 - 17 Jun 2008

版本1.2.1 2008年6月17日

文档包含：

## 1. Requirements 需求

The scope of this document is a requirements description for Device Management. This document describes a set of functional requirements \(partly on an abstract level\) for the management of a Device’s changeable parameters, as seen from the Management Authority’s points of view. <br/> 本文档的范围是设备管理的要求描述。 本文档描述了从管理机构的角度来看，用于管理设备的可变参数的一组功能需求（部分在抽象层面上）。

This document contains information applicable to Network Operators, terminal and network manufacturers, enterprises, independent software vendors, content providers, and service providers.<br/> 本文档包含适用于网络运营商，终端和网络制造商，企业，独立软件供应商，内容提供商和服务提供商的信息。

This document covers the requirements needed to supply the core Device Management service. Additional, related functionality not described here may involve requirements outside the scope of this document. This additional functionality shall not interfere with the core service described in this document.<br/> 本文档涵盖提供核心设备管理服务所需的要求。 此外，此处未描述的相关功能可能涉及本文档范围之外的要求。 此附加功能不应干扰本文档中描述的核心服务。

## 2. Protocol 协议
This document describes a management protocol using the SyncML Representation Protocol [REPPRO]. This protocol is called the OMA Device Management Protocol, abbreviated as OMA DM Protocol, and it defines the protocol for various management procedures.<br/>
本文档描述了使用SyncML表示协议[REPPRO]的管理协议。 该协议被称为OMA设备管理协议（缩写为OMA DM协议），并且其定义用于各种管理过程的协议。

## 3. Bootstrap 初始化
This document defines how an OMA DM device is brought from a ‘clean’ state, to a state where it is capable to initiate a management session with a provisioned management server.<br/>
本文档定义了OMA DM设备如何从“干净”状态进入其能够发起与预配置管理服务器的管理会话的状态。

## 4. Representation Protocol 表示协议
This document covers the Device Management usage of the SyncML Representation Protocol.<br/>
本文档介绍了SyncML表示协议的设备管理使用。

## 5. Security 安全
This document describes OMA-DM security requirements in general, and provides description of transport layer security, application layer security, etc. It also describes security mechanisms that are used to provide for integrity, confidentiality and authentication.<br/>
本文档总体描述OMA-DM安全要求，并提供传输层安全性，应用层安全性等的描述。它还描述了用于提供完整性，机密性和认证的安全机制。

## 6. Notification Initiated Session 通知启动会话
This document specifies the OMA Device Management Notification Initiation package from the server. A management server can use this notification capability to cause the DM client to initiate a connection back to the management server.<br/>
本文档从服务器指定OMA设备管理通知启动包。管理服务器可以使用该通知能力来使得DM客户端发起到管理服务器的连接。

## 7. Standardized Objects 标准化对象
This document defines a set of management objects. Some of these are mandatory for all OMA DM compliant devices and others are optional. The objects are defined using the OMA DM Device Description Framework.<br/>
本文档定义了一组管理对象。 其中一些对所有符合OMA DM的设备是强制性的，而其他是可选的。 使用OMA DM设备描述框架定义对象。

## 8. Tree and Description 树及其描述
This document defines the management tree and the Nodes on which the OMA DM protocol acts. A standardized way to describe these Nodes is also specified.<br/>
本文档定义了OMA DM协议所在的管理树和节点。还规定了描述这些节点的标准化方法。

## 9. Tree and Description Serialization 树及其描述的序列化
This specification defines how to transform a runtime management tree into an xml or wbxml file. With this specification it is possible to transform a MO or complete/part of the Management Tree to or from an xml or wbxml file.<br/>
此规范定义了如何将运行时管理树转换为xml或wbxml文件。使用此规范，可以将管理树的MO或完整/部分转换为xml或wbxml文件或从xml或wbxml文件中转换。

## 10. Firmware Update Management Object 固件更新管理对象
This document specifies management object(s) and their necessary behaviour to support the updating of firmware in mobile devices. It leverages the OMA DM enabler [OMADM] and supports alternate download mechanisms (such as OMA Download [DLOTA]). This represents the interface between the client and server required to manage the update of a mobile device’s firmware.<br/>
本文档规定了管理对象及其支持的移动设备中固件更新的必要行为。它利用OMA DM启用程序[OMADM]并支持备用下载机制（例如OMA下载[DLOTA]）。这表示在管理移动设备的固件更新所需的客户端和服务器之间的接口。

The content and format of the update package, and the process used to update firmware in the device, are implementation specific and are not covered by this specification. <br/>
更新包的内容和格式以及用于更新设备中的固件的过程是实现特定的，并且不被本规范所涵盖。
