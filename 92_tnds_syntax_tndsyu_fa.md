# 9.2 TNDS Syntax TNDS语法
## 9.2.1 Supported properties in file 文件中支持的属性
All properties are defined and described in [DMTND]. Only a subset of these properties are valid in the file. The following table defines the subset of valid properties together with the requirements level for how it must be supported depending on if an entity is decoding or encoding a TNDS object:<br/>
所有属性在[DMTND]中定义和描述。 只有这些属性的一部分在文件中有效。 下表定义了有效属性的子集以及根据实体是否对TNDS对象进行解码或编码而必须支持的属性的要求级别：

| Property 性质 | Decode 解码 | Encode 编码 |
| -- | -- | -- |
| MgmtTree | MUST 必须| MUST 必须|
| VerDTD | MUST 必须 | MUST 必须 |
| Man | MAY 可选 | MAY 可选  |
| Mod | MAY 可选 | MAY 可选 |
| Node | MUST 必须 | MUST 必须 |
| NodeName | MUST 必须 | MUST 必须 |
| Path | MUST 必须 | MUST 必须 |
| Value| MUST 必须 | MUST 必须 |
| RTProperties | MUST 必须 | MUST 必须 |
| ACL | MUST 必须 | MAY 可选 |
| Format | MUST 必须 | MAY 可选 |
| Title | MAY 可选 | MAY 可选 |
| TStamp | MAY 可选 | MAY 可选 |
| Type | MUST 必须  | MUST 必须  |
| VerNo | MAY 可选 | MAY 可选 |

## 9.2.2 TNDS DTD
The DTD is specified in [DMTND]. All extra behavior and restriction compared to the DTD definitions is defined later in this chapter. A compliant TNDS object MUST follow all rules in this specification. The TNDS object byte stream can be encoded as xml or as wbxml. Two different MIME-types are defined to indicate what encoding type the byte stream uses.<br/>
DTD在[DMTND]中指定。与DTD定义相比，所有额外的行为和限制在本章后面定义。合规的TNDS对象必须遵循本规范中的所有规则。TNDS对象字节流可以编码为xml或wbxml。定义了两种不同的MIME类型以指示字节流使用哪种编码类型。

## 9.2.3 TNDS Elements TNDS元素
This section defines the elements that are allowed in the TNDS object.<br/>
此部分定义在TNDS对象中允许的元素。

### 9.2.3.1 Structural elements 结构元素
#### 9.2.3.1.1 MgmtTree
Usage: Container for one or more described management objects. <br/>
用法：一个或多个描述的管理对象的容器。

Parent Elements: none<br/>
父元素：无

Restrictions: This MUST be the root element of all descriptions.<br/>
限制：这必须是所有描述的根元素。

#### 9.2.3.1.2 VerDTD
Usage: Specifies the major and minor version identifier of the SyncML DM Description Framework specification used to represent the SyncML DM description.<br/>
用法：指定用于表示SyncML DM描述的SyncML DM描述框架规范的主要和次要版本标识符。

Parent Elements: MgmtTree<br/>
父元素：MgmtTree

Restrictions: Major revisions of the specification create incompatible changes which will generally require a new parser. Minor revisions involve changes that do not impact basic compatibility of the parser. When the XML document conforms to this revision of the SyncML Tree and Description specification [DMTND] the value MUST be 1.2. The element type MUST be included in the MgmtTree.<br/>
限制：规范的主要修订版会创建不兼容的更改，这通常需要一个新的解析器。次要修订涉及的部分不影响解析器的基本兼容性的更改。 当XML文档符合SyncML树和描述规范[DMTND]的此修订版时，值必须为1.2。 元素类型必须包含在MgmtTree中。

#### 9.2.3.1.3 Man
Usage: Specifies the device manufacturer name of the device the TNDS object is created from. <br/>
用法：指定从中创建TNDS对象的设备的设备制造商名称。 

Parent Elements: MgmtTree<br/>
父元素：MgmtTree

Restrictions: This element is OPTIONAL.<br/>
限制：此元素是可选的。

#### 9.2.3.1.4 Mod
Usage: Specifies the device manufacturer’s model number of the device the TNDS object is created from. <br/>
用途：指定从中创建TNDS对象的设备的设备制造商型号。

Parent Elements: MgmtTree
父元素：MgmtTree

Restrictions: This element is OPTIONAL.
限制：此元素是可选的。

#### 9.2.3.1.5 Node
Usage: Specifies a node. <br/>
用法：指定节点。

Parent Elements: MgmtTree<br/>
父元素：MgmtTree

Restrictions: This element is recursive. A Node with a Value element MUST always terminate the recursion. It is possible for a Node to omit both the next recursive Node and a Value, this means that the hierarchy of Nodes continues elsewhere. This can be used to increase readability of very deep trees. In the continuation, the Path element MUST contain a full URI that specifies the insertion point in the tree.<br/>
限制：此元素是递归的。具有Value元素的节点必须始终终止递归。节点可以省略下一个递归节点和值，这意味着节点的层次结构在其他地方继续。这可以用于增加非常深的树的可读性。在继续中，Path元素必须包含指定树中插入点的完整URI。

Example: The following XML is a description of a number of nodes that form the URI Vendor/ISP/GWInfo/GWName.<br/>
示例：以下XML是形成URI Vendor/ ISP / GWInfo / GWName的多个节点的描述。
```
<MgmtTree> 
  <Node>
    <NodeName>Vendor</NodeName> 
    <RTProperties>...</RTProperties> 
    <Node>
    <NodeName>ISP</NodeName> 
    <RTProperties>...</RTProperties> 
      <Node>
      <NodeName>GWInfo</NodeName> 
      <RTProperties>...</RTProperties> 
        <Node>
        <NodeName>GWName</NodeName> 
        <RTProperties>...</RTProperties> 
        <Value>gw.yyy.se</Value>
        </Node> 
      </Node>
   </Node>
 </Node> 
</MgmtTree>
```

#### 9.2.3.1.6 NodeName

Usage: Specifies the name of the described node. <br/>
用法：指定所描述节点的名称。

Parent Elements: Node<br/>
父元素：Node

Restrictions: See [RFC2396] for general restrictions on URI. The NodeName element MAY be empty. If empty, this means that the name of the node MUST be assigned when the node is created. When the node name is assigned at node creation time, the value for the name is set to the last segment of the URI specified as Target for the command this results in the node being created. See also in [DMTND].<br/>
限制：有关URI的一般限制，请参阅[RFC2396]。 NodeName元素可以为空。如果为空，这意味着在创建节点时必须分配节点的名称。在节点创建分配节点名称时，名称的值将设置为指定为目标的URI的最后一个段，这将导致节点的创建。 参见[DMTND]。

If NodeName is omitted then the client may use the Type to decide where in the tree the structure should be created.<br/>
如果忽略NodeName，则客户端可以使用类型来决定应该在树中的哪里创建结构。
