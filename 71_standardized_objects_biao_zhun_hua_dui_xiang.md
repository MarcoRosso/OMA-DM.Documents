# 7.1 Standardized Objects 标准化对象
## 7.1.1 Management Objects 管理对象
Management objects are logical collections of related nodes that enable the targeting of management operations, using OMA DM protocol commands. Each node in a management object can be as small as an integer or large and complex like a background picture or screen saver. The OMA DM protocol is agnostic about the contents, or values, of the management objects and treats the node values as opaque data.<br/>
管理对象是相关节点的逻辑集合，使用OMA DM协议命令实现管理操作的目标。管理对象中的每个节点可以小到整数或大及复杂到如背景图片或屏幕保护程序。OMA DM协议对管理对象的内容或值是不可知的，并且将节点值视为不透明数据。

### 7.1.1.1 Management Objects 管理对象
OMA DM management objects are defined using the OMA DM Device Description Framework [DMTND], or DDF. The use of this description framework produces detailed information about the device in question. However, due to the high level of detail in these descriptions, they are sometimes hard for humans to digest and it can be a time consuming task to get an overview of a particular objects structure.<br/>
OMA DM管理对象使用OMA DM设备描述框架[DMTND]或DDF来定义。该描述框架的使用产生关于所讨论的设备的详细信息。 然而，由于这些描述中的高水平的细节，它们有时对于人来说是难以消化的，并且获得对特定对象结构的概述可能是耗时的任务。

In order to make it easier to quickly get an overview of how a management object is organized and its intended use, a simplified graphical notation in the shape of a block diagram is used in this document. Even though the notation is graphical, it still uses some printable characters, e.g. to denote the number of occurrences of a node. These are mainly borrowed from the syntax of DTDs for XML. The characters and their meaning are defined in the following table.<br/>
为了使得概述管理对象如何组织及预期其用途更容易快速，在本文档中使用框图形状的简化图形符号。 即使符号是图形的，它仍然使用一些可打印的字符，例如。以表示节点的出现次数。这些主要是从XML的DTD的语法借用。字符及其含义在下表中定义。

| Character 字符 | Meaning 含义 |
| -- | -- |
| + | one or many occurrences 出现一次或多次 |
| * | zero or more occurrences 出现零次或多次 |
| ？ | zero or one occurrences 出现零次或一次 |

If none of these characters is used the default occurrence is exactly once.<br/>
如果没有使用这些字符，默认出现的次数的正好是一次。

There is one more feature of the DDF that needs to have a corresponding graphical notation, the un-named block. These are blocks that act as placeholders in the description and are instantiated with information when the nodes are used at run-time. Un-named blocks in the description are represented by a lower case character in italics, e.g. *x*.<br/>
有一个更多的功能的DDF需要有一个相应的图形符号，即未命名的块。这些是在描述中用作占位符的块，并且在节点运行使用时信息实例化。描述中的未命名块由斜体字的小写字符表示，例如 *x*。

Each block in the graphical notation corresponds to a described node, and the text is the name of the node. If a block contains an *x*, it means that the name is not known in the description and that it will be assigned at run-time. The names of all ancestral nodes are used to construct the URI for each node in the management object. It is not possible to see the actual parameters, or data, stored in the nodes by looking at the graphical notation of a management object.<br/>
图形符号中的每个块对应于一个所描述的节点，并且文本是节点的名称。如果块包含*x*，则意味着名称在描述中未知，并且将在运行时分配。所有祖先节点的名称用于为管理对象中的每个节点构造URI。不可能通过查看管理对象的图形符号来查看存储在节点中的实际参数或数据。

The following is an example of what a management object can look like when it is expressed using the graphical notation. This particular object is the OMA DM Device Information management object.<br/>
以下是使用图形表示法表示管理对象时的示例。这个特定对象是OMA DM设备信息管理对象。
![](7.1.1.1a.jpeg)
Naturally, this graphical overview does not show all the details of the full description, but it provides a good map of the description so that it is easier to find the individual nodes. Although the figure only provides an elevated view of the description, there are still some things worth noticing. All the blocks with names in place occur exactly once, except Ext and Bearer that are optional and may not be present at all. One of the named nodes, DevInfo, has child nodes; it is an interior node. With the exception of Ext and Bearer, none of the other named nodes can have any children of their own; they are leaf nodes. The un-named leaf nodes are marked with `*`. This means that although the description only contains one node description at this position in the tree, there can be any number of instantiated nodes at run-time, including none. The only limit is that the node names MUST be unique and memory MUST be available to store the nodes.<br/>
自然地，该图形概述不显示完整描述的所有细节，但是它提供了描述的好的图，使得更容易找到各个节点。虽然图中只提供了一个概括的描述，但还有一些值得注意的事情。所有具有名称的块都恰好出现一次，除了Ext和Bearer是可选的，并且可能根本不存在。其中一个命名节点DevInfo具有子节点；它是一个内部节点。除了Ext和Bearer之外，没有其他命名节点可以有自己的任何子节点；它们是叶节点。未命名的叶节点用`*`标记。这意味着虽然描述部分在树中的该位置仅包含一个节点描述，但是在运行时可以有任何数量的实例化节点，数量也可以是没有。唯一的限制是节点名称必须是唯一的，并且存储器必须可用于存储节点。

The next figure shows an example of what the device information management object could look like at run-time.<b/r>
下图显示了设备信息管理对象在运行时的外观示例。



