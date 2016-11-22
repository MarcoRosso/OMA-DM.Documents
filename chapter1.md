# Requirements 需求

## 1.Terminology and Conventions 术语和约定
### 1.1 Conventions 约定
The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in [RFC2119]. <br/>
本文档中的关键词“必须”，“必须不”，“必须”，“必须”，“必须不”，“推荐”，“不推荐”，“推荐”，“可以”和“可以” 解释如[RFC2119]中所述。（根据该文档，MUST、REQUIRED和SHALL, MUST NOT和SHALL NOT, SHOULD和RECOMMENDED,SHOULD NOT和NOT RECOMMENDED，MAY和OPTIONAL均为相同含义，故分别译为必须，必须不，推荐，不推荐，可以。） 
### 1.1 Definitions 定义
Archiving of applications: The process initiated by the Device Management System or the Device itself that, together with DRM policies, allows applications to be moved to an offline or online storage medium. These remotely stored applications may run on request by the User, and be transparently restored to the device or the User may take explicit action to restore the application. The process includes all actions required to temporarily replace applications on demand.<br/>
应用程序归档：由设备管理系统或设备本身启动的与DRM策略一起将应用移动到离线或在线存储介质的过程。这些远程存储的应用可以由用户请求运行，并且被透明地恢复到设备，或者用户可以采取明确的动作来恢复应用。该过程包括临时替换需要的应用程序所需的所有操作。

Backup and Restore: The secure and reliable offline storage of personal information, parameters and applications that can be used at a later date to restore the device. The backup copy can be stored locally, remotely or as a combination of both.<br/>
备份和恢复：安全可靠的离线存储个人信息，参数和应用程序，可以在以后使用以恢复设备。 备份副本可以本地，远程或作为两者的组合存储。

Bootstrap Provisioning: The process of installing parameters and/or applications on a Device to establish a given service for the first time, or for the purposes of resetting a Device to initial settings.<br/>
引导配置：在设备上安装参数和/或应用程序以首次建立特定服务或将设备重置为初始设置的过程。

Content Provider:An entity that provides data which forms the basis of a service.<br/>
内容提供者：提供形成服务基础的数据的实体。

Continuous Provisioning: The process where a Device is updated with new data, parameters, or application upgrades to replace pre-existing versions.<br/>
连续配置：使用新数据，参数或应用程序升级更新设备以替换以前存在的版本的过程。


Device: In this context, a Device is a voice and/or data terminal that uses a Wireless Bearer for data transfer. Device types may include (but are not limited to): mobile phones (GSM, CDMA, 3GSM, etc.), data-only terminals, PDAs, laptop computers, PCMCIA cards for data communication, unattended data-only Devices (e.g., vending machines), and smart cards if associated with these Devices. If within a particular context an associated smart card should not be regarded as part of a Device this is marked explicitly.<br/>
设备：在此上下文中，设备是使用无线承载进行数据传输的语音和/或数据终端。设备类型可以包括（但不限于）：移动电话（GSM，CDMA，3GSM等），数据终端，PDA，笔记本电脑，用于数据通信的PCMCIA卡，无人值守的数据设备（如自动售货机）和智能卡（如果与这些设备相关联）。如果在特定上下文中，相关联的智能卡不应被视为设备的一部分，则这应该被明确地标记。

Device Discovery: A mechanism to allow devices to identify each other for the purposes of performing some data exchange. <br/>
设备发现：允许设备识别彼此以执行某些数据交换的机制。

Device Query: The process of polling a mobile Device for a specific piece of information.<br/>
设备查询：针对特定信息轮询移动设备的过程。








