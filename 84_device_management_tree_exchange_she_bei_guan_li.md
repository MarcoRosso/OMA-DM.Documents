# 8.4 Device Management Tree Exchange 设备管理树交换
The Management Tree is a hierarchical arrangement of managed objects in a device, which defines the management view of the device. In order to effectively manage a device, the DM Server SHOULD be able to manage relevant parts of the Management Tree in the device. Without knowing the Management Tree, the DM server would not be able to access a specific managed object in the device and hence effectively manage the device.<br/>
管理树是设备中管理对象的分层布置，其定义设备的管理视图。为了有效地管理设备，DM服务器应该能够管理设备中管理树的相关部分。在不知道管理树的情况下，DM服务器将不能访问设备中的特定的被管理对象，因此能更有效地管理设备。

The method for exchanging Management Tree information between a DM client and a DM server involves:<br/>
在DM客户端和DM服务器之间交换管理树信息的方法包括：
* Representing the wanted information from the tree, without loss of information about its hierarchical structure.<br/>
从树中表示想要的信息，而不损失其层次结构的信息
* Sending it in an OMA DM command to the recipient.<br/>
在OMA DM命令中将其发送到接收者

Management Tree information can be represented and delivered by using an XML representation as described in section 8.5.<br/>
管理树信息可以通过使用第8.5节中描述的XML表示来表示和传递。

The OMA DM specifications allow the DM server to add, replace and delete parts of a Management Tree in a single package, but to get the information from the client DM server requires multiple round trips. The following section specifies a way to Get a part of a Management Tree in a single package.<br/>
OMA DM规范允许DM服务器在单个包中添加，替换和删除管理树的部分，但是从客户端DM服务器获得信息需要多次往返。以下部分指定了在单个程序包中获取管理树的一部分的方法。

## 8.4.1 Requesting a Part of a Management Tree 请求管理树的一部分
The DM server uses the Get command with an attribute in the URI to retrieve the Management Tree information identified by the attribute in the URI. The client SHOULD send all the requested information and the information of the child Nodes to which the DM server has a read access right as specified in the table below. In case this feature is not supported the client SHOULD return status code(406) Optional Feature Not Supported.<br/>
DM服务器使用具有URI中的属性的Get命令来检索由URI中的属性标识的管理树信息。客户端应该发送所有请求的信息和DM服务器具有的读取访问权限的子节点的信息，如下表所指定。如果不支持此功能，客户端应返回状态代码（406）Optional Feature Not Supported。

The attributes are added to the URI specified in the Item element inside the Get command. The Get command and the URI in it have the following format:
`GET <URI>?list=<attribute>`<br/>
属性将添加到Get命令中的Item元素中指定的URI。Get命令和其中的URI具有以下格式：
`GET <URI>？list = <attribute>`

Where the attribute is addressed by appending `?list=<attribute>` to the retrieved Node’s URI.<br/>
其中通过将 `?<list> = <attribute>`追加到检索到的Node的URI来寻址属性。

The possible attributes are:<br/>
可能的属性是：

| Attribute 属性 | Description 描述 |
| -- | -- |
| Struct | The structure of a Management Tree is returned, without any data.<br/> 返回管理树的结构，没有任何数据。 |
| StructData | The structure of the Management Tree is returned, with the Leaf Nodes data.<br/> 返回管理树的结构，其中包含叶节点数据。 |
| TNDS | The returned data is a serialized sub-tree as defined in [DMTNDS].<br/> 返回的数据是在[DMTNDS]中定义的序列化子树。 |

## 8.4.2 Representation Response of the Management Tree 管理树的表示响应

Representing the tree using multiple Item elements inside the OMA DM Result command is the simplest approach. Requested information from the Node (URI in the Get command with attribute) is embedded into an Item inside a Result command with the following requirements (See also the examples in the Appendix):<br/>
在OMA DM Result命令中使用多个Item元素表示树是最简单的方法。来自节点的请求信息（具有属性的Get命令中的URI）被嵌入到Result命令内的项中，它具有以下要求（另见附录中的示例）：

* Struct attribute – Meta MUST be used to indicate the Type and Format of the Node, unless the Type and Format have the default values [META]. LocURI inside the Source MUST indicate the URI of the Node.<br/>
结构属性 - 元必须用于指示节点的类型和格式，除非类型和格式具有默认值[META]。源中的LocURI必须指示节点的URI。