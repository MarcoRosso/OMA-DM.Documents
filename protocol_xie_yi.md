# Protocol 协议
The OMA Device Management Protocol allows management commands to be executed on nodes. It uses a package format similar to SyncML Synchronization Protocol [SYNCPRO] and SyncML Representation Protocol [REPPRO]. A node might reflect a set of configuration parameters for a device. Actions that can be taken against this node might include reading and setting parameter keys and values. Another node might be the run-time environment for software applications on a device. Actions that can be taken against this type of node might include installing, upgrading, or uninstalling software elements.<br/>
OMA设备管理协议允许在节点上执行管理命令。 它使用类似于SyncML同步协议[SYNCPRO]和SyncML表示协议[REPPRO]的包格式。 一类节点可能反映设备的一组配置参数。 可以对此节点执行的操作可能包括读取和设置参数键和值。 另一类节点可能是设备上软件应用程序的运行时环境。 可以针对此类型的节点执行的操作可能包括安装，升级或卸载软件元素。

Actions are represented by OMA Device Management Protocol Commands, which are described in [REPPRO] and Device Management Representation Protocol [DMREPPRO]. The commands and message structure used correspond identically to that of the [SYNCPRO]. Thus, the DTD for the Management Protocol is the DTD from [SYNCPRO].<br/>
可执行操作由在[REPPRO]和设备管理表示协议[DMREPPRO]中描述的OMA设备管理协议命令表示。 所使用的命令和消息结构与[SYNCPRO]的命令和消息结构相同。 因此，管理协议的DTD是来自[SYNCPRO]的DTD。

Each node MUST be addressed by a unique full device URI. URIs MUST follow requirements specified in Uniform Resource Identifiers (URI) [RFC2396] with the restrictions as specified in OMA Device Management Tree and Descriptions [DMTND]. Node addressing is defined in [DMTND].<br/>
每个节点必须通过唯一的完整设备URI来寻址。 URI必须遵循具有在OMA设备管理树和描述[DMTND]中指定的有限制的统一资源标识符（URI）[RFC2396]中指定的要求。节点寻址在[DMTND]中定义.

Each node has a type that determines what kind of management content can be set/read on that object. Operations on a certain node require a predefined type of value to be sent and when the object is read, a value of that type is returned. For example a certain node can have a simple text type (text/plain) so simple text values can be set while another node stores complex types like the WAP Provisioning document type and require that value set in that node come with the WAP Provisioning document MIME type. Examples for other objects with complex values can be WAP settings or installed software.<br/>
每个节点具有确定的类型以此确定在该对象上可以设置/读取什么种类的管理内容。特点节点上的操作需要发送预定义类型的值，当读取对象时，将返回该类型的值。例如，某个节点可以具有简单的文本类型（文本/简单），因此可以设置简单的文本值，而另一个节点则存储复杂类型，如WAP配置文档类型，并要求该节点中的值是WAP配置文档MIME类型。具有复杂值的其他对象的示例可以是WAP设置或安装的软件。

In OMA DM Protocol, the target and source of a command are identified by the Target and Source elements respectively. Target refers to the recipient, and Source refers to the originator. Exceptions to this approach are mentioned in management commands requiring exception.<br/>
在OMA DM协议中，命令的目标和源分别由目标和源元素标识。目标是指收件人，而源是指发起者。在需要异常的管理命令中提到了此方法的异常。
## Conventions 约定
All sections and appendixes, except “Scope” and “Introduction”, are normative, unless they are explicitly indicated to be informative.<br/>
除了“范围”和“简介”之外，所有章节和附录都是规范性的，除非明确指出它们是信息性的。

Any reference to components of the DTD's or XML snippets are specified in this “typeface”.<br/>
在此typeface中指定对DTD或XML片段的组件的任何引用。

## Definitions 定义
See SyncML Representation Protocol [REPPRO] and SyncML Synchronization Protocol [SYNCPRO] for definitions of SyncML terms used within this specification.<br/>
有关本规范中使用的SyncML术语的定义，请参阅SyncML表示协议[REPPRO]和SyncML同步协议[SYNCPRO]。

See the DM Tree and Description document [DMTND] for definitions of terms related to the management tree.<br/>
有关与管理树相关的术语的定义，请参阅DM树和描述文档[DEMAND]。

Full device URI: Full path to a device resource specified in the device's context. It is always a URI relative to the devices’ root node. Full device URI must always be used in the present specification.<br/>
完整设备URI: 在设备上下文中指定的设备资源的完整路径。 它总是一个相对于设备根节点的URI。 在本规范中必须始终使用完整设备URI。

Message: Atomic unit in OMA DM Protocol, one packet that the bearer network is able to accept. One OMA DM Protocol package could be divided into many messages.<br/>
消息：OMA DM协议中的原子单元，承载网能够接受的一个分组。 一个OMA DM协议包可以被分成许多消息。

Package: Package is a conceptual set of commands that could be spread over multiple messages.<br/>
包：包是可以分布在多个消息上的一组概念性命令。

Resource: A network data object or service that can be identified by a URI, as defined in Hypertext Transfer Protocol [RFC2616]. Resources may be available in multiple representations (e.g. multiple languages, data formats, size, and resolutions) or vary in other ways.<br/>
资源：可由超文本传输协议[RFC2616]中定义的URI标识的网络数据对象或服务。 资源可以以多种表示（例如，多种语言，数据格式，大小和分辨率）或以其它方式。

## Reference 参考
[DMNOTI]:“OMA Device Management Notification Initiated Session, Version 1.2”. Open Mobile Alliance .
OMA-TS-DM_Notification-V1_2. URL:http://www.openmobilealliance.org

[DMREPPRO]:“OMA Device Management Representation Protocol, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_RepPro-V1_2. URL:http://www.openmobilealliance.org

[DMSEC]:“OMA Device Management Security, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_Security-V1_2. URL:http://www.openmobilealliance.org

[DMSTDOBJ]:“OMA Device Management Standardized Objects, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_StdObj-V1_2. URL:http://www.openmobilealliance.org

[DMTND]:“OMA Device Management Tree and Description, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_TND-V1_2. URL:http://www.openmobilealliance.org

[IOPPROC]:“OMA Interoperability Policy and Process”, Version 1.1, Open Mobile AllianceTM, OMA-IOP-Process-V1_1, URL:http://www.openmobilealliance.org

[META]:
“SyncML Meta Information, version 1.2”. Open Mobile Alliance . OMA-TS-SyncML_MetaInfo-V1_2. URL:http://www.openmobilealliance.org

[REPPRO]:“SyncML Representation Protocol, version 1.2”. Open Mobile Alliance . OMA-TS-SyncML_RepPro-V1_2. URL:http://www.openmobilealliance.org

[RFC2119]:“Key words for use in RFCs to Indicate Requirement Levels”. S. Bradner. March 1997.
URL:http://www.ietf.org/rfc/rfc2119.txt

[RFC2396]:“Uniform Resource Identifiers (URI): Generic Syntax”. T. Berners-Lee, et al. August 1998. URL:http://www.ietf.org/rfc/rfc2396.txt

[RFC2616]:“Hypertext Transfer Protocol -- HTTP/1.1”. R. Fielding, et al. June 1999.
URL:http://www.ietf.org/rfc/rfc2616.txt

[SYNCPRO]:“SyncML Data Sync Protocol, version 1.2”. Open Mobile Alliance . OMA-TS-DS_Protocol-V1_2. URL:http://www.openmobilealliance.org