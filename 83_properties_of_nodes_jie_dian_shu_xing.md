# 8.3 Properties of Nodes 节点属性
## 8.3.1 Definition 定义
Properties of Nodes are used to provide meta information about the Node in question. All properties in this section are run- time properties, e.g. they are available during the lifetime of their associated Node. Section 8.5.4.3 deals with the properties used in the context of device descriptions, which are completely separate from the run-time properties dealt with here.<br/>
节点的属性用于提供关于所讨论的节点的元信息。此部分中的所有属性都是运行时属性，例如，它们在其相关联的节点的生存期期间可用。第8.5.4.3节涉及在设备描述的上下文中使用的属性，它与此处处理的运行时属性完全分离。

| Property 属性 | Explanation 解释 |
| -- | -- |
| ACL |  Access Control List 访问控制列表|
| Format | Specifies how Node values should be interpreted <br/> 指定如何解释节点值 |
| Name | The name of the Node in the tree <br/> 树中的节点的名称 |
| Size | Size of the Node value in bytes<br/> 节点的大小（以字节为单位） |
| Title | Human readable name<br/> 人可读名字 |
| TStamp | Time stamp, date and time of last change<br/>时间戳，上次更改的日期和时间|
| Type | The MIME type of a Leaf Node’s value or a URN representing the Management Object identifier for Interior Nodes which root a Management Object sub-tree<br/> 叶节点的值的MIME类型或表示管理对象子树根的内部节点的管理对象标识符的URN |
| VerNo | Version number, automatically incremented at each modification.<br/> 版本号，每次修改时自动递增 |

It MUST NOT be possible to create new properties in an existing device.<br/>
它必须不在现有设备中创建新的属性。

## 8.3.2 Supported properties 支持的属性
Devices MAY support different sets of properties. Some properties are OPTIONAL for a device to implement, but all are REQUIRED for servers. The following table defines property support for devices.<br/>
设备可以支持不同的属性集。 一些属性对于设备来说是可选的，但对于服务器都是必需的。下表定义了设备的属性支持。

| Property 属性 | Device support 设备支持 |
| -- | -- |
| ACL | MUST 必须 |
| Format | MUST 必须 |
| Name | MUST 必须 |
| Size | MAY for Leaf Nodes <br/> 可以用于叶节点 <br/> MUST NOT for Interior Nodes<br/>必须不用于内部节点 |
| Title | MAY 可以 |
| TStamp | MAY 可以 |
| Type | MUST 必须 |
| VerNo | MAY 可以 |

## 8.3.3 Property addressing 属性寻址
The properties of a Node are addressed by appending `?prop=<property_name>` to the Node’s URI. For instance, to access the ACL of an OMA DM account a DM Server could use one of these URIs;<br/>
通过将`?prop=<property_name>`添加到节点的URI来寻址节点的属性。例如，为了访问OMA DM帐户的ACL，DM服务器可以使用这些URI之一;<br/>
           ./DMAcc/xyzInc?prop=ACL<br/>
           DMAcc/xyzInc?prop=ACL<br/>
If a server addresses an unsupported property in a device, an error is returned in the form of an (406) Optional feature not supported status.<br/>
如果服务器寻址设备中遇到不受支持的属性，则会返回（406）Optional feature not supported status的错误。

## 8.3.4 Property values 属性值
Property values MUST be transported by OMA DM as UTF-8 encoded strings. Numerical property values MUST be converted to numerical strings, expressed in decimal. It is NOT RECOMMENDED to use a `<Meta>` element for property values.<br/>
属性值必须由OMA DM作为UTF-8编码字符串传输。数字属性值必须转换为数字字符串，以十进制表示。 不推荐对属性值使用`<Meta>`元素。

It is unnecessary to use a `<Meta>` element for property values because they are all strings. This means that they would all have the same `<Meta>`, like this:<br/>
对于属性值，不必使用`<Meta>`元素，因为它们都是字符串。这意味着它们都将具有相同的`<Meta>`，如下所示：
```
<Meta>
  <Format xmlns=’syncml:metinf’>chr</Format> 
  <Type xmlns=’syncml:metinf’>text/plain</Type>
</Meta>
```

## 8.3.5 Operations on properties 属性操作
The following table defines the allowed operations for each property. An operation on a property is equivalent to an OMA DM command that is performed by a server on the URI of the property.<br/>
下表定义了每个属性允许的操作。对属性的操作等效于由服务器对属性的URI执行的OMA DM命令。

| Property 属性 | Applicable Commands 适用命令 | Comment 备注 |
| -- | -- | -- |
| ACL | Get, Replace | Get and Replace are the only valid commands for ACL manipulation. Note that Replace always replaces the complete ACL.<br/>Get和Replace是ACL操作的唯一有效命令。请注意，Replace始终会替换完整的ACL。 |
| Format | Get |  Automatically updated by Add and Replace commands on the associated Node.<br/>通过关联节点上的添加和替换命令自动更新。 |
| Name | Get, Replace | A Replace is equivalent to a rename of the Node.<br/>Replace等效于节点的重命名。 |
| Size | Get | Automatically updated by the device.<br/> 由设备自动更新。 |
| Title | Get, Replace | Only updated by server actions or software version changes.<br/> 仅通过服务器操作或软件版本更改进行更新。 |
| TStamp | Get | Automatically updated by the device.<br/>由设备自动更新。 |
| Type | Get | Automatically updated by Add and Replace commands on the associated Leaf Node.<br/>在关联的叶节点上通过Add和Replace命令自动更新。 |
| VerNo | Get | Automatically updated by the device.<br/> 由设备自动更新。 |

Properties do not support the Add command. All mandatory properties, and those optional properties that a device implements, MUST be automatically created when a new Node is created. The values of the newly created Node properties areall empty,e.g.`<Data/>`.However,Node properties that have a default value,or are automatically updated by the device, MUST be assigned appropriate values by the device.<br/>
属性不支持Add命令。所有必需属性和设备实现的那些可选属性必须在创建新节点时自动创建。新创建的N节点属性的值为空，例如`<Data/>`。但是，具有默认值或由设备自动更新的节点属性必须由设备分配适当的值。

Use of an unsupported command on a property will result in an error and the status (405) Command not allowed is returned.<br/>
在属性上使用不支持的命令将导致错误，并返回状态（405）Command not allowed。

Property values MAY also change for reasons other than direct server operations. For instance, some devices MAY allow the user to modify the ACL. If this occurs and the device supports the TStamp or VerNo properties, these MUST be updated.<br/>
属性值也可能因直接服务器操作之外的原因而更改。例如，一些设备可以允许用户修改ACL。如果发生这种情况，并且设备支持TStamp或VerNo属性，则必须更新这些属性。

### 8.3.5.1 Properties of Permanent Nodes 永久节点的属性
The semantics of most properties are independent of the permanent/dynamic status of the Node to which they are associated. The exception is the Name property, which MUST NOT be changed for permanent Nodes. Any attempt to perform such a change SHALL fail.<br/>
大多数属性的语义与它们所关联的节点的永久/动态状态无关。异常是Name属性，必须不更改永久节点。 任何尝试执行这样的更改都将失败。

## 8.3.6 Scope of properties 属性范围

With the exception of the ACL property, all properties are only applicable to the Node with which they are associated. Properties are individual characteristics of each Node. There SHALL be no inheritance of property values, implied or specified, other than for the ACL property.<br/>
除ACL属性外，所有属性仅适用于与其关联的节点。属性是每个节点的个别特性。属性值必须没有隐含或指定的继承，这与ACL属性不同。

## 8.3.7 Detailed description of properties 详细的属性描述

### 8.3.7.1 ACL
The ACL property has some unique characteristics when compared to the other properties.<br/>
与其他属性相比，ACL属性具有一些独特的特性。

The access rights granted by an ACL are granted to Server Identifiers and not to the URI, IP address or certificate of a DM Server. The Server Identifier is an OMA DM specific name for a server. A management session is associated with a DM Server Identifier through OMA DM authentication [DMSEC]. All management commands received in one session are assumed to originate from the same DM Server.<br/>
ACL授予的访问权限授予服务器标识符，而不授予DM服务器的URI，IP地址或证书。服务器标识符是服务器的OMA DM特定名称。管理会话通过OMA DM认证[DMSEC]与DM服务器标识符相关联。在一个会话中接收的所有管理命令被假定为源自同一DM服务器。

#### 8.3.7.1.1 ACL and inheritance ACL和继承
Every Node MUST implement the ACL property, but there can be no guarantee that the ACL of every Node has a value assigned to it. However, the root Node MUST always have an ACL value. If a server performs a management operation on a Node with no value set on the ACL the device MUST look at the ACL of the parent Node for a value. If the parent does not have a value for the ACL, the device MUST look at the ACL of the parent’s parent, and so on until an ACL value is found. This search will always result in a found value since the root Node MUST have an assigned ACL value. This way, Nodes can inherit ACL settings from one of their ancestors.<br/>
每个节点必须实现ACL属性，但不能保证每个节点的ACL都有赋值的值。但是，根节点必须始终具有ACL值。如果服务器在没有在ACL上设置值的节点上执行管理操作，则设备必须查看父节点的ACL的值。如果父节点没有ACL的值，则设备必须查看父节点父节点的ACL，以此类推，直到找到ACL值。此搜索将最终找到值，因为根节点必须具有指派的ACL值。这样，节点可以从其祖先中继承ACL设置。

Inheritance only takes place if there is no value assigned to the complete ACL property, i.e. there are no commands present. As soon as any value for an ACL property is present, this value is the only valid one for the current Node. ACL values MUST NOT be constructed by concatenation of values from the current Node and its ancestors.<br/>
仅在没有为完整ACL属性分配值（即没有命令存在）时才会发生继承。一旦ACL属性的任何值存在，此值是当前节点的唯一有效值。ACL值不能通过连接来自当前节点及其祖先的值来构造。

If an ACL does not contain any Server Identifier for a particular command, then this command MUST NOT be present in the ACL. Inheritance does not take place on a per command basis. Whenever an ACL is changed, by a server or by the client itself, care needs to be taken so that command names without Server Identifiers are not stored in the new ACL, resulting in an improperly formatted ACL.<br/>
如果ACL不包含特定命令的任何服务器标识符，则此命令不得存在于ACL中。继承不会在每个命令的基础上发生。每当ACL由服务器或客户端本身更改时，需要注意，没有服务器标识符的命令名称不应存储在新的ACL中，这将导致格式不正确的ACL。

A Get command on the ACL property of a Node MUST return an empty data value, e.g. `<Data/>`, if the ACL for that Node has no commands present (i.e. if the ACL has no value). In other words, the client SHOULD NOT locate an ancestor with a value for the ACL and provide that value.<br/>
如果该节点的ACL没有命令（即如果ACL没有值），对节点的ACL属性的Get命令必须返回一个空数据值，例如 `<Data/>`。换句话说，客户端不应该找到具有ACL的值的祖先并提供该值。

#### 8.3.7.1.2 The root ACL value 根ACL值
The value of the root is special – it is owned by the device. It is also the only Node that MUST have a value assigned to the ACL. The default value for the root ACL SHOULD be `Add=*&Get=*`.<br/>
根的值是特殊的 - 它由设备拥有。它也是唯一必须为ACL分配值的节点。根ACL的默认值应为`Add = *＆Get = *`。

To ensure that any authenticated server always can extend the Management Tree, the root ACL value for the Add command SHOULD NOT be changed. The ACL value for the Add command in the root ACL SHOULD be “`*`”. Any attempt by a server to modify this ACL value MAY fail with the status code (405) Command not allowed.<br/>
为了确保任何已验证的服务器始终可以扩展管理树，Add命令的根ACL值不应该被更改。根ACL中的Add命令的ACL值应为“`*`”。 服务器尝试修改此ACL值可能会失败，并显示状态代码（405）Command not allowed。

#### 8.3.7.1.3 Changing the ACL 更改ACL
The rules for changing the ACL of a Node are different for Interior Nodes and Leaf Nodes.<br/>
更改节点的ACL的规则对于内部节点和叶节点是不同的。
* Interior Nodes 内部节点<br/>
The ACL is valid for the Node and all properties that the Node may have, i.e. the right to access the ACL is controlled by the ACL itself. If a Server Identifier has Replace access rights according to the Node ACL then this Server Identifier can change the ACL value.<br/>
ACL对节点和节点可能具有的所有属性有效，即访问ACL的权限由ACL本身控制。 如果服务器标识符根据节点ACL具有替换访问权限，则此服务器标识符可以更改ACL值。
* Leaf Nodes 叶节点<br/>
The ACL is valid for the Node value and all properties that the Node may have, except the ACL property itself. If a Server Identifier has Replace access rights according to the Node ACL then this Server Identifier can change the Node value and all property values, but not the ACL value.<br/>
ACL对节点值和节点可能具有的所有属性有效，但ACL属性本身除外。如果服务器标识符根据节点ACL具有替换访问权限，则此服务器标识符可以更改节点值和所有属性值，但不能更改ACL值。

However, for both types of Nodes the right to change the ACL of the Node is also controlled by the ACL of the parent Node. Note that any parent Node is by definition an Interior Node. This makes it possible for a Server Identifier with sufficient access to a parent Node to take control of a child Node. This is a two-step process where the server first changes the ACL of the child Node and then can access the Node value, list of children or other Node properties. Note that even if a server has total access to the parent Node according to the parent’s ACL, this does not imply direct access to the child Node value. To change a child Node value the child ACL value MUST be changed first.<br/>
但是，对于这两种类型的节点，更改节点的ACL的权利也由父节点的ACL控制。注意，任何父节点根据定义是内部节点。这使得具有对父节点的足够访问的服务器标识符能够控制子节点。 这是一个两步过程，其中服务器首先更改子节点的ACL，然后可以访问节点值，子节点列表或其他节点属性。请注意，即使服务器根据父节点的ACL对父节点具有完全访问权限，也不意味着可以直接访问子节点值。要更改子节点值，必须首先更改子ACL值。

The ability for a Server Identifier with access to a parent Node to take control of a child Node implies that any Server Identifier with control of the root Node can take control of the complete Management Tree. Doing so is a laborious process that involves many separate management commands being issued by the server. It also implies that, unless two Server Identifiers agree about passing authority between them, transition of authority cannot take place. This also makes ‘hostile takeovers’ of devices impossible. To provide the end user with the ability to change which Server Identifier that controls the root Node some devices MAY implement a UI for this purpose.<br/>
具有访问父节点以控制子节点的服务器标识符的能力意味着具有根节点的控制的任何服务器标识符可以控制完整的管理树。这样做是一个费力的过程，涉及由服务器发出的许多单独的管理命令。它还意味着，除非两个服务器标识符同意在它们之间传递权限，权限的转换不能发生。这也使得设备的“敌意收购”不可能。为了向最终用户提供改变控制根节点的服务器标识符的能力，一些设备可以为此实现UI。

Servers can explicitly set ACL values by performing a Replace operation on the ACL property of any given Node. A successful completion of such an operation is signaled by an (200) OK status code. If the operation fails due to lack of device memory status code (420) Device full is returned. In addition, if the reason for failure is access violation the status code (425) Permission denied is returned.<br/>
服务器可以通过对任何给定节点的ACL属性执行替换操作来显式设置ACL值。这样的操作的成功完成由（200）OK状态码发出信号。如果操作由于缺少设备内存而失败则返回状态代码（420）Device full。此外，如果失败的原因是访问冲突，则返回状态代码（425）Permission denied。

If a server successfully creates a new Node with the Add command the value of the Node’s ACL property is initially set to no value, e.g. <Data/>,. This means that the value is inherited from the parent Node. However, there is one exception to this rule. If a server is adding an Interior Node and does not have Replace access rights on the parent of the new Node then the device MUST automatically set the ACL of the new Node so that the creating server has Add, Delete and Replace rights on the new Node.<br/>

In cases where the above rule does not apply it is RECOMMENDED that the current Server Identifier explicitly set the new Node ACL. This is achieved by using a Replace command on the ACL URI of the new Node. The current server SHOULD set the ACL value so that itself has Delete, Get and Replace access.<br/>

Note that since the only command available to change an ACL is Replace, all existing Server Identifiers and access rights are overwritten. If a server wishes to keep the existing entries in an ACL it MUST read the ACL, perform the needed changes and then Replace the existing ACL with the new one.<br/>



