# Tree and Description 树及其描述

Other OMA DM specifications define the syntax and semantics of the OMA DM protocol. However, the usefulness of such a protocol would be limited if the managed entities in devices required different data formats and displayed different behaviors. To avoid this situation this specification defines a number of mandatory Management Objects for various uses in devices. These objects are primarily associated with OMA DM and SyncML configuration.<br/>
其他OMA DM规范定义了OMA DM协议的语法和语义。然而，如果设备中的管理实体需要不同的数据格式并且显示不同的行为，则这种协议的有用性将受到限制。为了避免这种情况，本规范定义了用于设备中的各种用途的多个强制管理对象。这些对象主要与OMA DM和SyncML配置相关联。

Since device manufacturers will always develop new functions in their devices and since these functions often are proprietary, no standardized Management Objects exist for them. To make these functions manageable in the devices that have them, a device description framework is needed that can provide servers with the necessary information they must have in order to manage the new functions. The intention with this framework is that device manufacturers will publish descriptions of their devices as they enter the market. Organizations operating DM Servers should then only have to feed the new description to their servers for them to automatically recognize and manage the new functions in the devices.<br/>
由于设备制造商将始终在其设备中开发新功能，并且由于这些功能通常是专有的，因此不存在用于它们的标准化管理对象。为了使这些功能在具有它们的设备中可管理，需要设备描述框架，其可以向服务器提供他们必须具有的必要信息以便管理新功能。这个框架的意图是，设备制造商将在他们进入市场时发布他们的设备的描述。然后，运行DM服务器的组织只需要向其服务器馈送新描述，以便他们自动识别和管理设备中的新功能。

## Definitions 定义
Access Control List: A list of identifiers and access rights associated with each identifier.<br/>
访问控制列表: 与每个标识符相关联的标识符和访问权限的列表。

Description Framework: A specification for how to describe the management syntax and semantics for a particular device type.<br/>
描述框架：如何描述特定设备类型的管理语法和语义的规范。

Dynamic Node: A Node is dynamic if the DDF property Scope is set to Dynamic, or if the Scope property is unspecified.<br/>
动态节点：如果DDF属性“范围”设置为“动态”，或如果未指定“范围”属性，则节点是动态的。<br/>

Interior Node: A Node that may have child Nodes, but cannot store any value. The Format property of an Interior Node is node.<br/>
内部节点：可能有子节点但不能存储任何值的节点。内部节点的Format属性是节点。

Leaf Node: A Node that can store a value, but cannot have child Nodes. The Format property of a Leaf Node is not node.<br/>
叶节点：可以存储值但不能具有子节点的节点。叶节点的Format属性不是节点。

Management Object: A Management Object is a subtree of the Management Tree which is intended to be a (possibly singleton) collection of Nodes which are related in some way. For example, the ./DevInfo Nodes form a Management Object. A simple Management Object may consist of one single Node.<br/>
管理对象：管理对象是管理树的子树，其旨在成为以某种方式相关的节点的集合（可能是单例）。 例如，./DevInfo节点形成管理对象。 一个简单的管理对象可以由一个单一的节点组成。

Management Object Identifier: The Type property describing the kind of data stored as the Management Object’s value.<br/>
管理对象标识符：Type属性描述作为管理对象的值存储的数据的类型。

DM Server: A network based entity that issues OMA DM commands to devices and correctly interprets responses sent from the devices.<br/>
DM服务器：基于网络实体，向设备发出OMA DM命令，并正确解释从设备发送的响应。

Management Tree: The mechanism by which the management client interacts with the device, e.g. by storing and retrieving values from it and by manipulating the properties of it, for example the access control lists.
<br/>
管理树：管理客户端与设备交互的机制，例如， 通过存储和检索它的值，并通过操作它的属性，例如访问控制列表。

Node: A Node is a single element in a Management Tree. There can be two kinds of Nodes in a Management Tree: Interior Nodes and Leaf Nodes. The Format property of a Node provides information about whether a Node is a leaf or an Interior Node.<br/>
节点: 节点是管理树中的单个元素。管理树中可以有两种节点：内部节点和叶节点。节点的Format属性提供关于节点是叶节点还是内部节点的信息。

Permanent Node: A Node is permanent if the DDF property Scope is set to Permanent. If a Node is not permanent, it is dynamic. A permanent Node can never be deleted.<br/>
永久节点：如果DDF属性范围设置为永久，则节点是永久的。如果节点不是永久的，则它是动态的。永久节点永远不能被删除。

Server Identifier: The OMA DM internal name for a DM Server. A DM Server is associated with an existing Server Identifier in a device through OMA DM authentication.<br/>
服务器标识符：DM服务器的OMA DM内部名称。DM服务器通过OMA DM认证与设备中的现有服务器标识符相关联。

## Abbreviations 缩写
OMA Open Mobile Alliance 开放移动联盟

ACL Access Control List  访问控制列表

DDF Device Description Framework 设备描述框架