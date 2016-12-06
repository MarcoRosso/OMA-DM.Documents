# 8.5 Device Description Framework 设备描述框架
## 8.5.1 Rationale for a Device Description Framework 设备描述框架的原理
In an ideal world all devices would display the same structure and behavior to a management system. But since different vendors are competing with each other on the market for various kinds of devices, it seems very unlikely that this would ever happen. But management systems still need to understand each individual device even though they do appear to have different internal structures and behaviors.<br/>
在理想的世界中，所有设备将向管理系统显示相同的结构和行为。 但是，由于不同的供应商在市场上与各种设备相互竞争，看起来不太可能发生这种情况。 但是管理系统仍然需要理解每个单独的设备，即使它们看起来具有不同的内部结构和行为。

To address this issue the concept of a device description framework is introduced. In short this framework prescribes a way for device vendors to describe their devices so that a management system can understand how to manage the device. The following figure illustrates the principle.<br/>
为了解决这个问题，引入了设备描述框架的概念。简而言之，该框架规定了设备供应商描述他们的设备的方式，使得管理系统可以理解如何管理设备。下图说明了原理。

![](8.5.1.jpeg)
By using a description framework we also make sure that the total management system based on OMA DM is flexible and easily extendible. And that it can accommodate not only the demands we put on it today but also the ones we might have tomorrow. We also avoid a situation where all future management needs would have to be standardized before they could be used in devices to simplify the use of these devices.<br/>
通过使用描述框架，我们还确保基于OMA DM的总管理系统是灵活的并且易于扩展。它不仅能适应我们今天提出的要求，而且能适应我们明天可能提出的要求。我们还避免了一种情况，即所有未来的管理需求必须标准化，然后才能用于设备，以简化这些设备的使用。

It is important to note that the description framework needs to co-exist with the existing standardized Management Objects, and that the borderline between the standardized Management Objects and Management Objects described by the framework will change over time. This will mainly happen when a standards body decides to create specifications on how their technology should be managed. It is in the interest of the OMA Device Management committee to encourage and support such initiatives from standard bodies active in wireless standardization, so that the set of standardized Management Objects increases.<br/>
重要的是要注意，描述框架需要与现有的标准化管理对象共存，并且框架所描述的标准化管理对象和管理对象之间的边界将随时间而改变。这将主要发生在标准机构决定创建关于如何管理其技术的规范时。符合OMA设备管理委员会的利益的是鼓励和支持活跃于无线标准化的标准机构的这些举措，以便增加标准化管理对象的集合。

## 8.5.2 The OMA DM Device Description Framework OMA DM设备描述框架
Today there exist a number of different description frameworks, but none of these seem to suit the purposes of OMA DM. There are also activities in other standards bodies that aim to develop new frameworks specifically for the wireless industry. With this in mind, OMA DM does currently not specify the use of any particular framework.<br/>
今天，存在许多不同的描述框架，但是这些框架似乎都不符合OMA DM的目的。其他标准机构也还有活动，旨在为无线行业开发新的框架。考虑到这一点，OMA DM目前没有规定使用任何特定的框架。

However, the need for a description framework remains and therefore OMA DM RECOMMEND using the following simple framework as an interim solution. This proposed description framework is defined by an XML DTD. Descriptions of Management Objects, or complete Management Trees, are valid XML documents. Device manufactures using the description framework MUST make the device descriptions available to DM Servers. The mechanism for this is currently not being standardized.<br/>
然而，描述框架是仍然需要的，因此OMA DM推荐使用以下简单框架作为临时解决方案。提出的这个描述框架由XML DTD定义。管理对象或完整管理树的描述是有效的XML文档。使用描述框架的设备制造商必须使设备描述可用于DM服务器。 其机制目前尚未标准化。

The OMA DM Device Description Framework DTD is defined in [DMDDFDTD].<br/>
OMA DM设备描述框架DTD在[DMDDFDTD]中定义。

## 8.5.3 XML usage XML用法
The OMA DM DDF information XML documents are specified using well-formed XML. However, they MAY not be valid XML. That is, they do not need to specify the XML prolog. They only need to specify properly identified name space element types from the OMA DM DDF information DTD. This restriction allows for the OMA DM DDF information to be specified with greater terseness than would be possible if a well-formed, valid XML document was REQUIRED.<br/>
使用格式良好的XML指定OMA DM DDF信息XML文档。但是，它们可能不是有效的XML。也就是说，他们不需要指定XML序言。他们只需要从OMA DM DDF信息DTD中指定正确标识的名称空间元素类型。这种限制允许以比如果需要格式良好的有效XML文档的情况下可能更严格地来指定OMA DM DDF信息。

This DTD makes heavy use of XML name spaces. Name spaces MUST be declared on the first element type that uses an element type from the name space.<br/>
此DTD大量使用XML名称空间。名称空间必须在使用名称空间中的元素类型的第一个元素类型上声明。

Names in XML are case sensitive. The element types in the OMA DM DDF information DTD are defined in [DMDDFDTD] or the URN syncml:dmddf.<br/>
XML中的名称区分大小写。OMA DM DDF信息DTD中的元素类型在[DMDDFDTD]或URN syncml：dmddf中定义。

OMA DM also makes use of XML standard attributes, such as xml:lang. Any XML standard attribute can be used in a XML document conforming to this DTD.<br/>
OMA DM还使用XML标准属性，如xml：lang。任何XML标准属性都可以在符合此DTD的XML文档中使用。

## 8.5.4 Framework Elements 框架元素
This section explains the elements used in the description framework DTD.<br/>
本节介绍在描述框架DTD中使用的元素。

### 8.5.4.1 Structural elements 结构元素
These elements provide various kinds of structural information of the described Management Object.<br/>
这些元素提供所描述的管理对象的各种结构信息。

#### 8.5.4.1.1 MgmtTree
Usage: Container for one or more described Management Objects.<br/>
用法：一个或多个描述的管理对象的容器。

Parent Elements: none<br/>
父元素：无

Restrictions: This MUST be the root element of all descriptions.<br/>
限制：这必须是所有描述的根元素。

Content Model:(VerDTD, Man?, Mod?, Node+)<br/>
内容模型：(VerDTD, Man?, Mod?, Node+)

#### 8.5.4.1.2 VerDTD
Usage: Specifies the major and minor version identifier of the OMA DM Description Framework specification used to represent the OMA DM description.<br/>
用法：指定用于表示OMA DM描述的OMA DM描述框架规范的主要和次要版本标识符。

Parent Elements: MgmtTree<br/>
父元素：MgmtTree

Restrictions: Major revisions of the specification create incompatible changes that will generally require a new parser. Minor revisions involve changes that do not impact basic compatibility of the parser. When the XML document conforms to this revision of the OMA DM Device Description Framework the value MUST be 1.2. The element type MUST be included in the MgmtTree.<br/>
限制：规范的主要修订版创建不兼容的更改，这通常需要一个新的解析器。 次要修订涉及不影响解析器的基本兼容性的更改。当XML文档符合OMA DM设备描述框架的此版本时，值必须为1.2。元素类型必须包含在MgmtTree中。

Content Model: (#PCDATA)<br/>
内容模型：(#PCDATA)

#### 8.5.4.1.3 Man
Usage: Specifies the manufacturer of the device. <br/>
用法：指定设备的制造商

Parent Elements: MgmtTree<br/>
父元素：MgmtTree

Restrictions: This element is OPTIONAL. <br/>
限制：此元素是可选的。

Content Model: (#PCDATA)<br/>
内容模型：(#PCDATA)

#### 8.5.4.1.4 Mod
Usage: Specifies the model number of the device. <br/>
用法：指定设备的型号。

Parent Elements: MgmtTree<br/>
父元素：MgmtTree

Restrictions: This element is OPTIONAL. <br/>
限制：此元素是可选的。

Content Model: (#PCDATA)<br/>
内容模型：(#PCDATA)

#### 8.5.4.1.5 Node
Usage: Specifies a Node.<br/>
用法：指定一个节点。

Parent Elements: MgmtTree <br/>
父元素：MgmtTree

Restrictions: This element is recursive. A Node with a Value element MUST always terminate the recursion. It is possible for a Node to omit both the next recursive Node and a Value, this means that the hierarchy of Nodes continues elsewhere. This can be used to increase readability of very deep trees. In the continuation, the Path element MUST contain a full URI that specifies the insertion point in the tree.<br/>
限制：此元素是递归的。具有Value元素的节点必须始终终止递归。节点可以省略下一个递归节点和值，这意味着节点的层次结构在其他地方继续。这可以用于增加非常深的树的可读性。在继续中，Path元素必须包含指定树中插入点的完整URI。

ContentModel:(NodeName, Path?, RTProperties?, DFProperties?, (Node`*`|Value?))<br/>
内容模型：(NodeName, Path?, RTProperties?, DFProperties?, (Node`*`|Value?))

Example: The following XML is a description of a number of Nodes that form the URI Vendor/ISP/GWInfo/GWName. Note that all the details of DFProperties are deliberately left out.<br/>
示例：以下XML是形成URI Vendor/ISP/GWInfo/GWName的多个节点的描述。请注意，DFProperties的所有详细信息都会被故意忽略。

```
<MgmtTree>
  <Node>
    <NodeName>Vendor</NodeName>
     <DFProperties>...</DFProperties>
     <Node>
       <NodeName>ISP</NodeName>
       <DFProperties>...</DFProperties>
       <Node>
        <NodeName>GWInfo</NodeName>
        <DFProperties>...</DFProperties>
        <Node>
          <NodeName>GWName</NodeName>
          <DFProperties>...</DFProperties>
          <Value>gw.yyy.se</Value>
        </Node>
      </Node>
     </Node>
  </Node>
</MgmtTree>
```
#### 8.5.4.1.6 NodeName
Usage: Specifies the name of the described Node.<br/>
用法：指定描述的节点的名称。

Parent Elements: Node<br/>
父元素：Node

Restrictions: See [RFC2396] for general restrictions on URI. The NodeName element MAY be empty. If empty, this means that the name of the Node MUST be assigned when the Node is created. When the Node name is assigned at Node creation time, the value for the name is set to the last segment of the URI specified as Target for the command that results in the Node being created. See also section 8.4.7.3.<br/>
限制：有关URI的一般限制，请参阅[RFC2396]。NodeName元素可以为空。如果为空，这意味着在创建节点时必须分配节点的名称。当节点名称在节点创建时分配时，名称的值将设置为指定为目标的URI的最后一个段，用于创建节点的命令。参见8.4.7.3节。

Content Model: (#PCDATA)
内容模型：(#PCDATA)

#### 8.5.4.1.7 Path
Usage: Specifies the URI up to, but not including, the described Node.<br/>
用法：指定URI，但不包括描述的节点。

Parent Elements: Node<br/>
父元素：Node

Restrictions: OPTIONAL element. If omitted, the URI for the Node MUST be constructed by concatenating all ancestral NodeName and Path values. This concatenated value MUST form the correct URI. Path SHOULD only be used inside Node elements that are child elements to the MgmtTree element. For general restrictions, see [RFC2396].<br/>
限制：可选元素。如果省略，则节点的URI必须通过连接所有祖先NodeName和Path值来构造。这个连接的值必须形成正确的URI。路径应该只在作为MgmtTree元素的子元素的Node元素中使用。有关一般限制，请参见[RFC2396]。

Content Model: (#PCDATA)<br/>
内容模型：(#PCDATA)

Example: The following XML is an alternative way to describe the same Management Objects as in the example in section 8.5.4.1.5. This description specifies the same URI as the other example: Vendor/ISP/GWInfo/GWName. Note that all the details of DFProperties are deliberately left out.<br/>
示例：以下XML是描述与第8.5.4.1.5节中的示例相同的管理对象的另一种方法。此描述指定与另一个示例相同的URI：Vendor/ISP/GWInfo/GWName。 请注意，DFProperties的所有详细信息都会被故意忽略。
```
<MgmtTree>
  <Node>
    <NodeName>Vendor</NodeName>
    <DFProperties>...</DFProperties>
  </Node>
  <Node>
    <NodeName>ISP</NodeName>
    <Path>Vendor</Path>
    <DFProperties>...</DFProperties>
  </Node>
  <Node>
    <NodeName>GWInfo</NodeName>
    <Path>Vendor/ISP</Path>
    <DFProperties>...</DFProperties>
  </Node>
  <Node>
    <NodeName>GWName</NodeName>
    <Path>Vendor/ISP/GWInfo</Path>
    <DFProperties>...</DFProperties>
    <Value>gw.yyy.se</Value>
  </Node>
</MgmtTree>
```
#### 8.5.4.1.8 Value
Usage: Specifies a default value for Nodes that are instantiated using the current description. <br/>
用法：指定使用当前描述实例化的节点的默认值。

Parent Elements: Node<br/>
父元素：Node

Restrictions: OPTIONAL element. If omitted, the Node description does not specify any default value for the Node. In this case the initial value of new Nodes are undefined.<br/>
限制：可选元素。如果省略，节点描述不会为节点指定任何默认值。在这种情况下，新节点的初始值是未定义的。

#### 8.5.4.1.9 RTProperties
Usage: Aggregating element for run-time properties, i.e. properties that the Nodes have in a device at run-time. Used to specify which properties the described Node supports at run-time. Can also be used to supply default values for supported run-time properties.<br/>
用法：聚合运行时属性的元素，即节点在运行时在设备中具有的属性。用于指定所描述的节点在运行时支持的属性。也可以用于为支持的运行时属性提供默认值。

Parent Elements: Node<br/>
父元素：Node

Restrictions: OPTIONAL element. If omitted, the Node MUST only support the mandatory run-time properties ACL, Format, Name and Type. If any optional properties are supported, they MUST be specified by using this element.<br/>
限制：可选元素。如果省略，节点必须只支持强制运行时属性ACL，格式，名称和类型。如果支持任何可选属性，则必须使用此元素指定它们。

Content Model: (ACL?, Format?, Name?, Size?, Title?, TStamp?, Type, VerNo?)<br/>
内容模型：（ACL？，Format？，Name？，Size？，Title？，TStamp？，Type，VerNo？）

#### 8.5.4.1.10 DFProperties
Usage: Aggregating element for description framework properties, i.e. properties that Nodes have in the description framework and that are not explicitly present at run-time.<br/>
用法：聚合描述框架属性的元素，即节点在描述中具有的属性框架，并且没有在运行时显式存在。

Parent Elements: Node<br/>
父元素：Node

Restrictions: This is a REQUIRED element.<br/>
限制：这是一个必须元素。

Content Model:(AccessType, DefaultValue?, Description?, DFFormat, Occurrence?, Scope?, DFTitle?, DFType, CaseSense?)<br/>
内容模型：（AccessType，DefaultValue ?, Description？，DFFormat，Occurrence？，Scope，DFTitle，DFType，CaseSense？）

### 8.5.4.2 Run-time property elements 运行时属性元素
The usage of the run-time properties in the description framework reflects the mandatory/optional status of the corresponding run-time property. These elements can also be used to describe default values for the supported properties. Since these properties can change at run-time, the values of these properties in the description and in a real device will differ.<br/>
在描述框架中运行时属性的使用反映了相应运行时属性的强制/可选状态。这些元素也可用于描述支持的属性的默认值。由于这些属性在运行时可能会更改，因此这些属性在描述中和实际设备中的值会有所不同。

The RTProperties element,which encapsulates the run-time properties,is OPTIONAL within its parent element Node. The purpose of this is to make it possible to omit the RTProperties element if only the mandatory propertiesare supported and there is no need to specify any default values.If the RTProperties element is used in a description,all the mandatory run-time properties MUST be specified.<br/>
RTProperties元素（封装运行时属性）在其父元素Node中是可选的。这样做的目的是如果只支持强制属性，则RTProperties元素可以省略，并且不需要指定任何默认值。如果在描述中使用RTProperties元素，则所有强制运行时属性必须被指定。

#### 8.5.4.2.1 ACL
Usage: Specifies support for the ACL property. MAY be used to specify a default value for the property. <br/>
用法：指定对ACL属性的支持。可用于指定属性的默认值。

Parent Elements: RTProperties<br/>
父元素：RTProperties

Restrictions: If a value is specified it MUST be formatted according to section 8.3.7.1.5.<br/>
限制：如果指定了值，则必须根据8.5.7.1.5节进行格式化。

Content Model: (#PCDATA)<br/>
内容模型：(#PCDATA)

#### 8.5.4.2.2 Format
Usage: Specifies support for the Format property. MAY be used to specify a default value for the property. <br/>
用法：指定对Format属性的支持。 可用于指定属性的默认值。

Parent Elements: RTProperties<br／>
父元素：RTProperties

Restrictions: If a default value is specified for the described Node, the Format property MUST specify the correct format of the Node value.<br/>
限制：如果为描述的节点指定了默认值，则Format属性必须指定Node值的正确格式。

Content Model: (b64 | bin | bool | chr | int | node | null | xml | date |time |float)<br/>
内容模型：（b64 | bin | bool | chr | int | node | null | xml | date | time | float）

#### 8.5.4.2.3 Name
Usage: Specifies support for the Name property. MAY be used to specify a default value for the property. <br/>
用法：指定对Name属性的支持。可用于指定属性的默认值。

Parent Elements: RTProperties<br/>
父元素：RTProperties

Restrictions: See [RFC2396]. If a default property value is specified, it SHOULD be the same as the value of the NodeName element.<br/>
限制：参见[RFC2396]。如果指定了默认属性值，则它应该与NodeName的值相同。

Content Model: (#PCDATA)<br/>
内容模型：(#PCDATA)

#### 8.5.4.2.4 Size
Usage: Specifies support for the Size property. MAY be used to specify a default value for the property. Within its parent element, the Size element is defined as optional. Size MUST NOT be used for Interior Nodes. In Node elements describing Leaf Nodes the Size element MAY be used within RTProperties.<br/>
用法：指定对Size属性的支持。可用于指定属性的默认值。在其父元素中，Size元素被定义为可选。 Size不能用于内部节点。在描述叶节点的节点元素中，可以在RTProperties中使用Size元素。

Parent Elements: RTProperties<br/>
父元素：RTProperties

Restrictions: If a value is specified it MUST be formatted according to section 8.3.4.<br/>
限制：如果指定了值，则必须根据第8.3.4节进行格式化。

Content Model: (#PCDATA)<br/>
内容模型：(#PCDATA)

#### 8.5.4.2.5 Title
Usage: Specifies support for the Title property. MAY be used to specify a default value for the property. <br/>
用法：指定对Title属性的支持。可用于指定属性的默认值。

Parent Elements: RTProperties<br/>
父元素：RTProperties

Restrictions: If a value is specified it MUST be formatted according to section 8.3.4.<br/>
限制：如果指定了值，则必须根据第8.3.4节进行格式化。

Content Model: (#PCDATA)<br/>
内容模型：(#PCDATA)

#### 8.5.4.2.6 TStamp
Usage: Specifies support for the TStamp property. MAY be used to specify a default value for the property. <br/>
用法：指定对TStamp属性的支持。可用于指定属性的默认值。

Parent Elements: RTProperties<br/>
父元素：RTProperties

Restrictions: If a value is specified it MUST be formatted according to section 8.3.4.<br/>
限制：如果指定了值，则必须根据第8.3.4节进行格式化。

Content Model: (#PCDATA)<br/>
内容模型：（#PCDATA）

#### 8.5.4.2.7 Type
Usage: Specifies support for the Type property. MAY be used to specify a default value for the property. <br/>
用法：指定对Type属性的支持。可用于指定属性的默认值。

Parent Elements: RTProperties<br/>
父元素：RTProperties

Restrictions: For Leaf Nodes, if a default value is specified for the described Node, the Type property MUST be used to specify the correct MIME type of the Node’s present value using a single MIME element. For Interior Nodes a DDFName element MUST be present and specify a valid Management Object identifier, which MAY be empty.<br/>
限制：对于叶节点，如果为描述的节点指定了默认值，则必须使用Type属性来使用单个MIME元素指定节点的当前值的正确MIME类型。对于内部节点，一个DDFName元素必须存在，并指定一个有效的管理对象标识符，它可以是空的。

Content Model:(MIME | DDFName)
内容模型：(MIME | DDFName)

#### 8.5.4.2.8 VerNo
Usage: Specifies support for the VerNo property. MAY be used to specify a default value for the property. <br/>
用法：指定对VerNo属性的支持。可用于指定属性的默认值。

Parent Elements: RTProperties<br/>
父元素：RTProperties

Restrictions: If a value is specified it MUST be formatted according to section 8.3.4.<br/>
限制：如果指定了值，则必须根据第8.3.4节进行格式化。

Content Model: (#PCDATA)<br/>
内容模型：（#PCDATA）

#### 8.5.4.2.9 b64
Usage: OMA DM format description. Specifies that the Node value is Base64 encoded. <br/>
用法：OMA DM格式描述。指定Node值为Base64编码。

Parent Elements:Format, DFFormat
父元素：Format, DFFormat

Restrictions: None.
限制：无

Content Model: EMPTY
内容模型：EMPTY

#### 8.5.4.2.10 bin
Usage: OMA DM format description. Specifies that the Node value is binary data. <br/>
用法：OMA DM格式描述。指定Node值是二进制数据。

ParentElements:Format, DFFormat<br/>
父元素：Format, DFFormat

Restrictions: None.<br/>
限制：无

Content Model: EMPTY
内容模型：EMPTY

#### 8.5.4.2.11 bool
Usage: OMA DM format description. Specifies that the Node value is a Boolean. <br/>
用法：OMA DM格式描述。指定Node值是布尔值。

Parent Elements:Format, DFFormat<br/>
父元素：Format, DFFormat

Restrictions: None.<br/>
限制：无。

Content Model: EMPTY
内容模型：EMPTY

#### 8.5.4.2.11 bool
Usage: OMA DM format description. Specifies that the Node value is a Boolean. <br/>
用法：OMA DM格式描述。 指定Node值是布尔值。

Parent Elements:Format, DFFormat<br/>
父元素：Format, DFFormat

Restrictions: None.<br/>
限制：无。

Content Model: EMPTY<br/>
内容模型：EMPTY

#### 8.5.4.2.12 chr
Usage: OMA DM format description. Specifies that the Node value is text.<br/>
用法：OMA DM格式描述。 指定Node值为文本。

Parent Elements:Format, DFFormat<br/>
父元素：Format, DFFormat

Restrictions: The character set used is specified either by the transport protocol, MIME content type header or XML prologue.<br/>
限制：使用的字符集由传输协议，MIME内容类型标头或XML序列指定。

Content Model: EMPTY<br/>
内容模型：EMPTY

#### 8.5.4.2.13 int
Usage: OMA DM format description. Specifies that the Node value is a 32-bit signed integer. <br/>
用法：OMA DM格式描述。指定Node值是32位有符号整数。

Parent Elements:Format, DFFormat
父元素：Format, DFFormat

Restrictions: None.<br/>
限制：无

Content Model: EMPTY<br/>
内容模型：EMPTY

#### 8.5.4.2.14 node
Usage: OMA DM format description. Specifies that the Node is an Interior Node. <br/>
用法：OMA DM格式描述。指定节点是内部节点。 

Parent Elements:Format, DFFormat
<br/>父元素：Format, DFFormat

Restrictions: This Format MUST only be used for Interior Nodes.<br/>
限制：此格式必须只用于内部节点。
