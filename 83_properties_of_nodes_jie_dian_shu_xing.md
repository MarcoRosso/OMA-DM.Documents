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
