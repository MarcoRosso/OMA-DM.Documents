# 1.2 Introduction

As differentiation between Device types grows and Device functionality broadens, the difficulty in provisioning these Devices with service-specific parameters and software increases.<br/>
随着设备类型的差异化和设备功能的扩大，为这些设备配置服务特定参数和软件的难度增加。

In addition, Device administration servers and systems face an increasingly difficult task in keeping track of the status and configuration of the Devices they manage.<br/>
此外，设备管理服务器和系统跟踪其管理的设备的状态和配置的任务变得越来越困难。

A Device is any User terminal which is primarily used in mobile scenarios. They may be equipped with a smart card (where applicable), which is under the sphere of influence of a specific Management Authority. The scope of Device Management includes both the Device itself and smart card. A Device could be, for example, a WAP- or MMS-capable handheld, a smart phone, PDA, or a notebook computer. PDAs, handhelds, smart phones and notebooks can be attached to a wireless modem via hardware integration, cable, IR, and Bluetooth.<br/>
设备是主要用于移动场景中的任何用户终端。他们可能配备有智能卡（如适用），这是在特定管理机构的影响范围内。设备管理的范围包括设备本身和智能卡。设备可以是例如具有WAP或MMS能力的手持设备，智能电话，PDA或笔记本计算机。 PDA，手持设备，智能手机和笔记本电脑可以通过硬件集成，电缆，红外和蓝牙连接到无线调制解调器。

Each of the requirements may limit the target Device to the specific subset of capabilities of a Device considering the fact that each of the Devices has different constraints from each other due mainly to capabilities in particular for mobile phone handset. When such requirements or use cases are specified, the capabilities of Device(s) that each requirement or use case is targeting should clearly be described in this specification. Devices which are under the control of a Management Authority should support transparent forced setting of all parameters covered by the Management Authority Control.<br/>
由于协议主要是针对移动电话手机的能力而每个设备彼此具有不同的限制，因此每个需求可以将目标设备限制到所有设备能力的特定子集。当指定了这些要求或用例时，每个需求或用例所针对的设备的能力应在本规范中清楚地描述。受管理机构控制的设备应支持对管理权限控制所涵盖的所有参数的透明强制设置。

The actors involved in Device Management include Management Authorities (including Network Operators, Enterprise Managers, Service Providers), Device Management Systems, Subscribers and Users.<br/>
设备管理参与的参与者包括管理机构（包括网络运营商，企业管理器，服务提供商），设备管理系统，订户和用户。

The objective of this document is to develop a standardized approach to Device Management.<br/>
本文件的目的是开发一种标准化的设备管理方法。

This document defines the requirements for Device Management as a framework to enable such functionality as:
* Bootstrap provisioning of configuration data to a Device
* Remote maintenance of configuration data of a Device
* Reporting of Device capabilities and configuration to a Management Authority
* Downloading/Updating and Retrieving status of Management Authority’s software, or operating system components/firmware to a Device
* Device diagnostics, performance reporting, and fault management
* Secure transmission of exchanged data to and from the Device
* Access rights management
* Cost-effective administration of configuration and software data on the Management Authority’s side
* Easy handling or virtual invisibility of diagnostic/update actions on the Subscriber's side
* Device conformance to policy established by the OMA
* Segregation of management ownership between one ore more entities. For example, the operator and enterprise can share management responsibilities
* Device conformance to Policy established by the Management Authority(s)
* Transfer of Management Authority. For example, the management rights are partially or fully transferred
between Management Authorities
* Integration of new software (downloaded or otherwise) into the existing Device Management framework
* Management, download and installation of software at all levels above hardware to the Device in the form of complete code, patching and deltas as applicable in communication with the Device Management Server via wired and unwired mechanisms

本文档将设备管理的要求定义为以下功能的框架：
* 将配置数据配置到设备
* 远程维护设备的配置数据
* 向管理机构报告设备功能和配置
* 下载/更新和检索管理中心软件或操作系统组件/固件的状态到设备
* 设备诊断，性能报告和故障管理
* 安全地传输交换的数据到设备和从设备传输
* 访问权限管理
* 在管理机构方面成本有效地管理配置和软件数据
* 在订阅者端轻松处理或虚拟隐藏诊断/更新操作
* 设备符合OMA制定的政策
* 在一个或多个实体之间分离管理所有权。 例如，运营商和企业可以共享管理责任
* 设备符合管理机构制定的政策
* 管理权移交。 例如，管理权被部分或全部转移管理机构之间
* 将新软件（已下载或以其他方式）集成到现有设备管理框架中
* 通过有线和无线机制与设备管理服务器通信，以完整代码，修补和增量的形式，在设备高于硬件的所有级别上管理，下载和安装软件
