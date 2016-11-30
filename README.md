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