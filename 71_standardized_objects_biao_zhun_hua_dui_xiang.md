# 7.1 Standardized Objects 标准化对象
## 7.1.1 Management Objects 管理对象
Management objects are logical collections of related nodes that enable the targeting of management operations, using OMA DM protocol commands. Each node in a management object can be as small as an integer or large and complex like a background picture or screen saver. The OMA DM protocol is agnostic about the contents, or values, of the management objects and treats the node values as opaque data.<br/>
管理对象是相关节点的逻辑集合，使用OMA DM协议命令实现管理操作的目标。管理对象中的每个节点可以小到整数或大及复杂到如背景图片或屏幕保护程序。OMA DM协议对管理对象的内容或值是不可知的，并且将节点值视为不透明数据。

### 7.1.1.1 Management Objects 管理对象
OMA DM management objects are defined using the OMA DM Device Description Framework [DMTND], or DDF. The use of this description framework produces detailed information about the device in question. However, due to the high level of detail in these descriptions, they are sometimes hard for humans to digest and it can be a time consuming task to get an overview of a particular objects structure.<br/>

In order to make it easier to quickly get an overview of how a management object is organized and its intended use, a simplified graphical notation in the shape of a block diagram is used in this document. Even though the notation is graphical, it still uses some printable characters, e.g. to denote the number of occurrences of a node. These are mainly borrowed from the syntax of DTDs for XML. The characters and their meaning are defined in the following table.<br/>



