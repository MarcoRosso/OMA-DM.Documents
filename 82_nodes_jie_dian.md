# 8.2 Nodes 节点
## 8.2.1 Common characteristics of Nodes 节点的共同特征
Nodes are the entities which can be manipulated by management actions carried over the OMA DM protocol. A Node can be as small as an integer or a large and complex like a background picture or screen saver. The OMA DM protocol is agnostic about the contents, or values, of the Nodes and treats the Leaf Node values as opaque data.<br/>
节点是可以通过OMA DM协议承载的管理动作来操纵的实体。节点可以小到整数或大和复杂到如背景图片或屏幕保护程序。OMA DM协议对节点的内容或值是不可知的，并且将叶节点值视为不透明数据。

An Interior Node can have an unlimited number of child Nodes linked to it in such a way that the complete collection of all Nodes in a management database forms a tree structure. Each Node in a tree MUST have a unique URI.<br/>
内部节点可以具有无限数量的与其链接的子节点，使得管理数据库中的所有节点的完整集合形成树结构。 树中的每个节点必须具有唯一的URI。

Each Node has properties associated with it; these properties are defined in 8.3.1. All properties, except the ACL, are valid only for the Node to which they are associated.<br/>
每个节点具有与其相关联的属性; 这些属性在8.3.1中定义。除ACL之外的所有属性仅对与其关联的节点有效。


