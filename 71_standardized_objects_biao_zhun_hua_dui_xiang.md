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

The next figure shows an example of what the device information management object could look like at run-time.<br/>
下图显示了设备信息管理对象在运行时的外观示例。

![](7.1.1.1b.jpeg)

The difference between this and the previous figure is that now the un-named blocks have been instantiated. It is also shown that the `*` character means that a node can occur zero or more times. Note that none of the stored data in the leaf nodes is shown in the figure, what are visible are only the node names.<br/>
这和前一个图的区别在于，现在未命名的块已经被实例化。还示出了`*`字符意味着节点可以出现零次或多次。注意，在图中没有示出叶节点中存储的数据，只有节点名称是可见的。

### 7.1.1.2 DDF compliance DDF合规性
The management object descriptions in this document are normative. However, the descriptions also contain are a number of informative aspects that could be included to enhance readability or serve as examples. Other informative aspects are, for instance, the ZeroOrMore and OneOreMore elements, where implementations MAY introduce restrictions. All these exceptions are listed here:<br/>
本文档中的管理对象的描述是规范性的。然而，描述还包括以增强可读性或作为示例的一些方面的信息。其他信息方面例如ZeroOrMore和OneOreMore元素，其中的实现方法可以引入限制机制。所有这些例外情况都列在这里：
* All XML comments, e.g. `<!-- some text -->`, are informative.<br/>
所有XML注释，例如`<！ - some text - >`，是信息性的。
* The descriptions do not contain an RTProperties element, or any of its child elements, but a description of an actual implementation of this object MAY include these.<br/>
描述不包含RTProperties元素或其任何子元素，但对此对象的实际实现的描述可以包括这些元素。
* If a default value for a leaf node is specified in a description, by the DefaultValue element, an implementation MUST supply its own appropriate value for this element. If the DefaultValue element is present in the description of a node, it MUST be present in the implementation, but MAY have a different value.<br/>
如果在描述中由DefaultValue元素指定了叶节点的默认值，则实现必须为此元素提供自己适当的值。如果DefaultValue元素存在于节点的描述中，则它必须存在于实现中，但可能有不同的值。
* The value of all Man, Mod, Description and DFTitle elements are informative and included only as examples.<br/>
所有Man，Mod，Description和DFTitle元素的值都是信息性的，仅作为示例。
* Below the interior nodes Ext and Bearer, an implementation MAY add further nodes at will.<br/>
在内部节点Ext和Bearer下，实现可以随意添加更多节点。
* The contents of the AccessType element MAY be extended by an implementation.<br/>
AccessType元素的内容可以通过实现扩展。
* If the any of the following AccessType values are specified, they MUST NOT be removed in an implementation: Copy, Delete, Exec, Get, and Replace.<br/>
如果指定了以下任何AccessType值，那么在实现中不能移除它们：复制，删除，执行，获取和替换。
* If the AccessType value Add is specified it MAY be removed in an implementation if the implementation only supports a fixed number of child nodes.<br/>
如果指定了AccessType值Add，如果实现只支持固定数量的子节点，则可以在实现中删除它。
* An implementation MAY replace the ZeroOrMore or OneOreMore elements with ZeroOrN or OneOrN respectively. An appropriate value for N MUST also be given with the ...OrN elements.<br/>
实现可以分别用ZeroOrN或OneOrN替换ZeroOrMore或OneOreMore元素。N的适当值也必须与... OrN元素一起给出。

### 7.1.2 Management objects standardized by other organizations 其他组织的标准化管理对象

OMA DM has been designed so that existing management objects can be managed. These existing management objects have typically already been standardized by other standards organizations.<br/>
OMA DM已设计为可以管理现有的管理对象。这些现有的管理对象通常已经被其他标准组织标准化。

### 7.1.3 The OMA DM management objects OMA DM管理对象
Clients implementing OMA DM MUST support the OMA DM Account management object, DevInfo management object and the DevDetail management object. OMA DM servers MUST support all three management objects as well.<br/>
实现OMA DM的客户端必须支持OMA DM帐户管理对象，DevInfo管理对象和DevDetail管理对象。OMA DM服务器也必须支持所有三个管理对象。

| Management Object 管理对象 | Client Support 客户端支持 | Server Support 服务器支持 | Description 描述 |
| -- | -- | -- | -- |
| DMAcc | MUST | MUST | Settings for the DM client in a managed device.<br/>受管设备中的DM客户端的设置。|
| DevInfo | MUST | MUST | Device information for the OMA DM server. Sent from the client to the server.<br/> OMA DM服务器的设备信息。从客户端发送到服务器。|
| DevDetail | MUST | MUST | General device information that benefits from standardization.<br/>从标准化中受益的一般设备信息。 |
| Inbox | MAY | MAY | Reserved URI where the device SHOULD use the management object identifier to identify the absolute URI.<br/>保留的URI，其中推荐设备使用管理对象标识符来标识绝对URI。 |

The difference between DevInfo and DevDetail is that the DevInfo parameters are needed by the management server for problem free operation of the OMA DM protocol. The DevInfo object is sent from client to server in the beginning of every session.<br/>
DevInfo和DevDetail之间的区别在于管理服务器需要DevInfo参数以用于OMA DM协议的无问题操作。 DevInfo对象在每个会话开始时从客户端发送到服务器。

DevDetail contains other device specific parameters that benefits from being standardized and mandatory. The only difference is that these parameters are not sent from client to server automatically. Instead, these parameters are managed by servers as any other parameters and can be manipulated using OMA DM commands.<br/>
DevDetail包含受益于标准化和强制性的其他设备特定参数。唯一的区别是这些参数不是从客户端自动发送到服务器。相反，这些参数由服务器作为任何其他参数来管理，并且可以使用OMA DM命令来操纵。

#### 7.1.3.1 The DM Account management object DM帐户管理对象
The management object is used to manage settings for OMA DM protocol.<br/>
管理对象用于管理OMA DM协议的设置。

Management object identifier: urn:oma:mo:oma-dm-dmacc:1.0<br/>
管理对象标识符：rn:oma:mo:oma-dm-dmacc:1.0

![](7.1.3.1.jpeg)
Parameters are also described in Device Management Application Characteristic registration document [w7] which is used as a part of OMA Client Provisioning specifications [ERELDCP]. General mapping rules of OMA Client Provisioning parameters are described in [DMBOOT]. When the DM Account parameters are derived from OMA Client Provisioning w7 document, see more information about parameter mapping in Appendix.<br/>
参数也在设备管理应用特性注册文档[w7]中描述，该文档是OMA客户端配置规范[ERELDCP]的一部分。 OMA客户端提供参数的一般映射规则在[DMBOOT]中描述。 当DM帐户参数是从OMA客户端配置w7文档派生时，请参阅附录中有关参数映射的更多信息。

The complete DDF description of this management object can be found in [DMAccDDF].<br/>
此管理对象的完整DDF描述可在[DMAccDDF]中找到。

##### 7.1.3.1.1 Node: `<X>`
This interior node acts as a placeholder for one or more accounts or for a fixed node.<br/>
此内部节点充当一个或多个帐户或固定节点的占位符。
* Occurrence: OneOrMore<br/>
出现次数：一次或多次
* Format: Node<br/>
形式：节点
* Access Types: Get<br/>
访问类型：Get
* Values: N/A<br/>
值：无

##### 7.1.3.1.2 Node: `<X>`/AppID
This node specifies the application ID for device management account object.<br/>此节点指定设备管理帐户对象的应用程序ID。
* Occurrence: One<br/>
出现次数：一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values: w7<br/>
值：w7

##### 7.1.3.1.3 Node: `<X>`/ServerID
This node specifies a server identifier for management server used in the management session.<br/>此节点指定管理会话中使用的管理服务器的服务器标识符。
* Occurrence: One<br/>
出现次数：一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values: `<Server identifier>`<br/>
值：`<Server identifier>`

##### 7.1.3.1.4 Node: `<X>`/Name
This node specifies user displayable name for the management server.<br/>
此节点指定管理服务器的用户可显示名称。
* Occurrence: ZeroOrOne<br/>
出现次数：零次或一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values: `<User displayable name>`<br/>
值：`<User displayable name>`

##### 7.1.3.1.5 Node: `<X>`/PrefConRef
This node specifies a reference to preferred connectivity. It is expected that either a proxy or NAP MO is specified, but other, implementation-specific connectoids MAY be referenced.<br/>
此节点指定对首选连接的引用。它期望指定代理或NAP MO，但是可以引用其他方法实现特定的连接。
* Occurrence: ZeroOrOne<br/>
出现次数：零次或一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values:  URI to a management object or implementation specific identifier.
<br/>
值：URI到管理对象或实现特定标识符。

##### 7.1.3.1.6 Node: `<X>`/ToConRef/
The ToConRef interior node is used to allow application to refer to a collection of connectivity definitions. Several connectoids MAY be listed for a given application under this interior node.<br/>
ToConRef内部节点用于允许应用程序引用连接定义的集合。对于这个内部节点下的给定应用，可以列出几个连接体。
* Occurrence: ZeroOrOne<br/>
出现次数：零次或一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values: N/A<br/>
值：无

##### 7.1.3.1.7 Node: `<X>`/ToConRef/`<X>`
This run-time node acts as a placeholder for one or more connectivity parameters.<br/>
此运行时节点充当一个或多个连接参数的占位符。
* Occurrence: OneOrMore<br/>
出现次数：一次或多次
* Format: Node<br/>
形式：节点
* Access Types: Get<br/>
访问类型：Get
* Values: N/A<br/>
值：无

##### 7.1.3.1.8 Node: `<X>`/ToConRef/`<X>`/ConRef
The ConRef leaf indicates the linkage to connectivity parameters.<br/>
ConRef叶表示连接到连接参数。
* Occurrence: One<br/>
出现次数：一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values:  URI to a management object or implementation specific identifier.
<br/>
值：URI到管理对象或实现特定标识符。

##### 7.1.3.1.9 Node: `<X>`/AppAddr
This node is used to specify multiple Management Server addresses.<br/>
此节点用于指定多个管理服务器地址。
* Occurrence: One<br/>
出现次数：一次
* Format: Node<br/>
形式：节点
* Access Types: Get<br/>
访问类型：Get
* Values: N/A<br/>
值：无

##### 7.1.3.1.10 Node: `<X>`/AppAddr/`<X>`
This interior node acts as a placeholder for separating one or more Server Addresses.<br/>
该内部节点充当用于分离一个或多个服务器地址的占位符。
* Occurrence: OneOrMore<br/>
出现次数：一次或多次
* Format: Node<br/>
形式：节点
* Access Types: Get<br/>
访问类型：Get
* Values: N/A<br/>
值：无

##### 7.1.3.1.11 Node: `<X>`/AppAddr/`<X>`/Addr
This node specifies a Management Server address.<br/>
此节点指定管理服务器地址。
* Occurrence: One<br/>
出现次数：一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values: Dependent upon AddrType<br/>
值：取决于AddrType

##### 7.1.3.1.12 Node: `<X>`/AppAddr/`<X>`/AddrType
This node specifies a Management Server address type.<br/>
此节点指定管理服务器地址类型。
* Occurrence: One<br/>
出现次数：一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values:  “URI”, “IPv4” or “IPv6”. If no value exists the default type MUST be “URI”.<br/>
值：“URI”，“IPv4”或“IPv6”。如果没有值，默认类型必须是“URI”。

##### 7.1.3.1.13 Node: `<X>`/AppAddr/`<X>`/Port
This node specifies Port information for Management Server address.<br/>
此节点指定管理服务器地址的端口信息。
* Occurrence: OneOrMore<br/>
出现次数：一次或多次
* Format: Node<br/>
形式：节点
* Access Types: Get<br/>
访问类型：Get
* Values: N/A<br/>
值：无

##### 7.1.3.1.14 Node: `<X>`/AppAddr/`<X>`/Port/`<X>`
This interior node acts as a placeholder for separating one or more Port settings.<br/>
该内部节点充当用于分离一个或多个端口设置的占位符。
* Occurrence: OneOrMore<br/>
出现次数：一次或多次
* Format: Node<br/>
形式：节点
* Access Types: Get<br/>
访问类型：Get
* Values: N/A<br/>
值：无

##### 7.1.3.1.15 Node: `<X>`/AppAddr/`<X>`/Port/`<X>`/PortNbr
This node specifies port number.<br/>此节点指定端口号。
* Occurrence: One<br/>
出现次数：一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values: The port number MUST be a decimal number and must fit within the range of a 16 bit unsigned integer.<br/>
值：端口号必须是十进制数，并且必须符合16位无符号整数的范围。

##### 7.1.3.1.16 Node: `<X>`/AAuthPref
This is a string-valued parameter whose possible values are the names of the various possible authentication types (AAuthType values), e.g. "DIGEST". If this node is present, the client SHOULD use this authentication type when connecting to the server. The use of this node is intended to reduce the number of round trips between client and server that would be caused by authentication challenges. If a client supports this leaf node and the value is empty, the default behaviour is to indicate the authentication mechanism negotiated in the previous session if one exists.<br/>
这是一个字符串值参数，其可能的值是各种可能的认证类型（AAuthType值）的名称，例如 “DIGEST”。 如果此节点存在，推荐客户端在连接到服务器时使用此认证类型。该节点的使用旨在减少由认证质询引起的客户端和服务器之间的往返次数。如果客户端支持此叶节点并且该值为空，则默认行为是指示在上一个会话中协商的认证机制（如果存在）。
* Occurrence: ZeroOrOne<br/>
出现次数：零次或一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values: See AAuthTypes in section 7.1.3.1.20.<br/>
值：请参阅第7.1.3.1.20节中的AAuthTypes。

##### 7.1.3.1.17 Node: `<X>`/AppAuth
This node specifies authentication information.<br/>
此节点指定认证信息。
* Occurrence: OneOrMore<br/>
出现次数：一次或多次
* Format: Node<br/>
形式：节点
* Access Types: Get<br/>
访问类型：Get
* Values: N/A<br/>
值：无

##### 7.1.3.1.18 Node: `<X>`/AppAuth/`<X>`
This interior node acts as a placeholder for separating one or more authentication settings.<br/>
该内部节点充当用于分离一个或多个认证设置的占位符。
* Occurrence: OneOrMore<br/>
出现次数：一次或多次
* Format: Node<br/>
形式：节点
* Access Types: Get<br/>
访问类型：Get
* Values: N/A<br/>
值：无

##### 7.1.3.1.19 Node: `<X>`/AppAuth/`<X>`/AAuthLevel
This node specifies the authentication level.<br/>
此节点指定认证级别。
* Occurrence: One<br/>
出现次数：一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values: 值：

|  | Status 状态 | Interpretation 解释 |
| -- | -- | -- |
| CLCRED | Optional 可选 | Credentials client uses to authenticate itself to the OMA DM Server at the DM protocol level.<br/> 凭据客户端用于在DM协议级别向OMA DM服务器认证自身。|
| SRVCRED | Optional 可选 | Credentials server uses to authenticate itself to the OMA DM Client at the DM protocol level.<br/>凭据服务器用于在DM协议级别向OMA DM客户端认证自身。 |
| OBEX | Optional 可选  | Credentials server uses to authenticate itself to the OMA DM Client at the DM protocol level. NOTE: If this AAuthLevel is selected only HTTP-BASIC, HTTP-DIGEST and TRANSPORT are possible AAuthTypes. <br/>OBEX身份验证凭据。注意：如果选择此AAuthLevel，则只有HTTP-BASIC，HTTP-DIGEST和TRANSPORT可能是AAuthTypes。 |
| HTTP | Optional 可选 | Credentials for HTTP (/WSP) authentication. NOTE: If this AAuthLevel is selected only HTTP-BASIC, HTTP-DIGEST and TRANSPORT are possible AAuthTypes.<br/>用于HTTP（/ WSP）身份验证的凭据。注意：如果选择此AAuthLevel，则只有HTTP-BASIC，HTTP-DIGEST和TRANSPORT可能是AAuthTypes。 |

##### 7.1.3.1.20 Node: `<X>`/AppAuth/`<X>`/AAuthType
This node specifies the authentication type.<br/>
此节点指定认证类型。
* Occurrence: One<br/>
出现次数：一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values: 值：

|  | Status 状态 | Interpretation 解释 |
| -- | -- | -- |
| HTTP-BASIC | Optional 可选 | HTTP basic authentication done according to RFC 2617.<br/> HTTP基本认证根据RFC2617完成。 |
| HTTP-DIGEST | Optional 可选 | HTTP digest authentication done according to RFC 2617.<br/> HTTP摘要认证根据RFC2617完成。 |
| BASIC | Optional 可选 | DM 'syncml:auth-basic' authentication as specified in [DMSEC].<br/> DM 'syncml：auth-basic'身份验证，如[DMSEC]中所指定。|
| DIGEST | Optional 可选 | DM 'syncml:auth-md5' authentication as specified in [DMSEC].<br/>DM 'syncml：auth-md5'验证，如[DMSEC]中指定。 |
| HMAC | Optional 可选 | DM 'syncml:auth-MAC' authentication as specified in [DMSEC].<br/> DM 'syncml：auth-MAC'验证，如[DMSEC]中指定。 |
| X509 | Optional 可选 | 'syncml:auth-X509' authentication done according to [REPPRO].<br/> 根据[REPPRO]完成的“syncml：auth-X509”身份验证。 |
| SECURID | Optional 可选 | 'syncml:auth-securid' authentication done according to [REPPRO].<br/>根据[REPPRO]完成的“syncml：auth-securid”身份验证。 |
| SAFEWORD | Optional 可选 | 'syncml:auth-safeword' authentication done according to [REPPRO].<br/>根据[REPPRO]完成的“syncml：auth-safeword”身份验证。 |
| DIGIPASS | Optional 可选 | 'syncml:auth-digipass' authentication done according to [REPPRO].<br/>根据[REPPRO]完成的“syncml：auth-digipass”身份验证。 |
| TRANSPORT | Optional 可选 | Secure Transport authentication is used. Transport layer authentication is beyond the scope of OMA DM Security.<br/> 使用安全传输身份验证。传输层认证超出了OMA DM安全的范围。 |

##### 7.1.3.1.21 Node: `<X>`/AppAuth/`<X>`/AAuthName
This node specifies the authentication name.<br/>
此节点指定认证名称。
* Occurrence: ZeroOrOne<br/>
出现次数：零次或一次
* Format: Chr<br/>
形式：字符
* Access Types: Get<br/>
访问类型：Get
* Values: `<Authentication name>`<br/>
值：`<Authentication name>`

##### 7.1.3.1.22 Node: `<X>`/AppAuth/`<X>`/AAuthSecret
This node specifies the authentication secret.<br/>
此节点指定认证密钥。
* Occurrence: ZeroOrOne<br/>
出现次数：零次或一次
* Format: Chr<br/>
形式：字符
* Access Types: No Get<br/>
访问类型：No Get
* Values: `<Authentication secret>`<br/>
值：`<Authentication secret>`

##### 7.1.3.1.23 Node: `<X>`/AppAuth/`<X>`/AAuthData
This node specifies the authentication data relating to the AAuthType.<br/>
此节点指定与AAuthType相关的认证数据。
* Occurrence: ZeroOrOne<br/>
出现次数：零次或一次
* Format: Bin<br/>
形式：二进制
* Access Types: No Get<br/>
访问类型：No Get
* Values: `<Authentication data>`<br/>
值：`<Authentication data>`

##### 7.1.3.1.24 Node: `<X>`/Ext/
The Ext is an interior node for where the vendor specific information about device management application is being placed (vendor meaning application vendor, device vendor, OS vendor etc.). Usually the vendor extension is identified by vendor specific name under the ext node. The tree structure under the vendor identified is not defined and can therefore include a non-standard sub-tree.<br/>
Ext是用于放置设备管理应用的供应商特定信息（供应商，意为应用供应商，设备供应商，操作系统供应商等）的内部节点。通常，供应商扩展由ext节点下的供应商特定名称标识。在所识别的供应商下的树结构未被定义，并且因此可以包括非标准子树。

#### 7.1.3.2 The DevInfo management object DevInfo管理对象
Management object identifier: urn:oma:mo:oma-dm-devinfo:1.0<br/>
管理对象标识符：urn：oma：mo：oma-dm-devinfo：1.0

The following figure shows an overview of the DevInfo management object.<br/>下图显示了DevInfo管理对象的概述。

![](7.1.3.2.jpeg)

The nodes making up DevInfo have the following meanings:<br/>
构成DevInfo的节点具有以下含义：

* Ext: An optional, interior node, designating the only branch of the DevInfo sub tree into which extensions can be added, permanently or dynamically.<br/>
Ext: 可选的内部节点，指定DevInfo子树的唯一分支，可以永久或动态地向其中添加扩展。

* Bearer: An optional, interior node of the DevInfo sub tree in which items related to the bearer (CDMA, etc.) are stored. Use of this sub tree can be mandated by other standards.<br/>
Bearer: DevInfo子树的可选的内部节点，其中存储与承载（CDMA等）相关的项目。使用此子树可以由其他标准强制。

* DevId: A unique identifier for the device. SHOULD be globally unique and MUST be formatted as a URN as defined in [RFC2141].<br/>
DevId: 设备的唯一标识符。应该是全局唯一的，并且必须格式化为[RFC2141]中定义的URN。

* Man: The manufacturer identifier.<br/> 
Man: 制造商标识符。

* Mod: A model identifier (manufacturer specified string).<br/>
Mod: 模型标识符（制造商指定的字符串）。

* DmV: OMA device management client version identifier (manufacturer specified string).<br/>
DmV:  OMA设备管理客户端版本标识符（制造商指定的字符串）。

* Lang: The current language setting of the device. The syntax of the language tags and their use are defined in [RFC1766]. Language codes are defined by ISO in the standard ISO639.<br/>
设备的当前语言设置。语言标记的语法及其使用在[RFC1766]中定义。语言代码由ISO在标准ISO639中定义。

The complete DDF description of this management object can be found in [DevInfoDDF].<br/>
此管理对象的完整DDF描述可在[DevInfoDDF]中找到。


#### 7.1.3.3 The DevDetail management object DevDetail管理对象
Management object identifier: urn:oma:mo:oma-dm-devdetail:1.0<br/>
管理对象标识符：urn：oma：mo：oma-dm-devdetail：1.0

The following figure shows an overview of the DevDetail management object.<br/>下图显示了DevDetail管理对象的概述。

![](7.1.3.3.jpeg)

The nodes making up DevDetail have the following meanings:<br/>
构成DevDetail的节点具有以下含义：

* Ext: An optional, interior node, designating the only branch of the DevDetail sub tree into which extensions can be added, permanently or dynamically.<br/>
Ext: 可选的内部节点，指定DevDetail子树的唯一分支，可以永久或动态地向其中添加扩展。

* Bearer: An optional, interior node, designating a branch of the DevDetail sub tree into which items related to the bearer (CDMA, etc.) are stored. Use of this sub tree can be mandated by other standards.<br/>
Bearer: 可选的内部节点，指定DevDetail子树的分支，其中存储与承载（CDMA等）相关的项目。使用此子树可以由其他标准强制。

* URI/MaxDepth: Specifies the maximum depth of the management tree supported by the device. The maximum depth of the tree is defined as the maximum number of URI segments that the device supports. The value is a 16 bit, unsigned integer encoded as a numerical string. The value ‘0’ means that the device supports a tree of ‘unlimited’ depth.<br/>
URI/MaxDepth: 指定设备支持的管理树的最大深度。树的最大深度定义为设备支持的最大URI段数。 该值是作为数字字符串编码的16位无符号整数。值'0'意味着设备支持“无限”深度的树。

* URI/MaxTotLen: Specifies the maximum total length of any URI used to address a node or node property. The maximum total length of a URI is defined as the largest total number of characters making up the URI which the device can support. Note that depending on the character set this might not be the same as the number of bytes. The value is a 16 bit, unsigned integer encoded as a numerical string. The value ‘0’ means that the device supports URI of ‘unlimited’ length.<br/>
URI/MaxTotLen: 指定用于寻址节点或节点属性的任何URI的最大总长度。URI的最大总长度被定义为构成设备可以支持的URI的最大字符总数。请注意，根据字符集，这可能不同于字节数。该值是作为数字字符串编码的16位无符号整数。值“0”表示设备支持“无限”长度的URI。

* URI/MaxSegLen: Specifies the maximum total length of any URI segment in a URI used to address a node or node property. The maximum total length of a URI segment is defined as the largest number of characters which the device can support in a single URI segment. Note that depending on the used character set this might not be the same as the number of bytes. The value is a 16 bit, unsigned integer encoded as a numerical string. The value ‘0’ means that the device supports URI segments of ‘unlimited’ length.<br/>
URI/MaxSegLen: 指定用于寻址节点或节点属性的URI中任何URI段的最大总长度。URI段的最大总长度被定义为设备在单个URI段中可以支持的最大字符数。请注意，根据使用的字符集，这可能与字节数不同。该值是作为数字字符串编码的16位无符号整数。值'0'表示设备支持'无限'长度的URI段。

* DevTyp: Device type, e.g. PDA, pager, or phone.<br/>
DevTyp: 设备类型，例如 PDA，寻呼机或电话。

* OEM: Original Equipment Manufacturer of the device.<br/>
OEM: 设备的原始设备制造商。

* FwV: Firmware version of the device.<br/>
FwV: 原始设备设备的制造商。

* SwV: Software version of the device.<br/>
SwV: 设备的软件版本。

* HwV: Hardware version of the device.<br/>
HwV: 设备的硬件版本。

* LrgObj: Indicates whether the device supports the OMA DM Large Object Handling specification, as defined in [DMPRO].<br/>
LrgObj: 指示设备是否支持[DMPRO]中定义的OMA DM大对象处理规范。

It is RECOMMENDED that the combination of HwV, SwV, FwV, Man, Mod, and OEM provide a unique signature identifying the specific version of software, thus providing a means for other implementations to make special provisions based on that identification.<br/>
建议HwV，SwV，FwV，Man，Mod和OEM的组合提供识别软件的特定版本的唯一签名，从而为其他实现提供基于该识别做出特殊配置的方法。

The complete DDF description of this management object can be found in [DevDetailDDF].<br/>
此管理对象的完整DDF描述可以在[DevDetailDDF]中找到。

#### 7.1.3.4 The Inbox URI 收件箱URI
Management object identifier: urn:oma:mo:oma-dm-inbox:1.0<br/>
管理对象标识符：urn：oma：mo：oma-dm-inbox：1.0 <br/>

In some circumstances a Management Object’s URI is not the preferred addressing method and the management object identifier is enough information for the device to resolve a suitable location for that Management Object. In that case the URI: “./Inbox” is a reserved location for this purpose.<br/>
在一些情况下，管理对象的URI不是优选的寻址方法，并且管理对象标识符对于设备解析该管理对象的合适位置来说足够了。在这种情况下，URI：“./Inbox”是为此目的的保留位置。

For example a device’s DDF description MAY indicate if that device is supporting the “./Inbox” concept. In that definition it is possible to define the only access type “Add”. Then a server MAY send a Management Object to that device with the URI: “./Inbox” and then the device SHOULD use the management object identifier to resolve the correct location in the management tree to add that Management Object. In this case the server can not Get that object from the URI: “./Inbox” after it is added. The client’s ACL for “./Inbox” MAY also set access rights so only some servers are allowed to use this feature.<br/>
例如，设备的DDF描述可以指示该设备是否支持“./Inbox”概念。在该定义中，可以定义唯一的访问类型“Add”。然后服务器可以向该设备发送具有URI：“./Inbox”的管理对象，然后设备应该使用管理对象标识符来解析管理树中的正确位置以添加该管理对象。在这种情况下，服务器不能在URI添加后从“./Inbox”URI获取该对象。客户端的“./Inbox”ACL也可以设置访问权限，只允许某些服务器使用此功能。

DM Clients MUST NOT permit a Get operation on the “./Inbox”. A DM Client SHALL return the status code “Command not allowed” (405) in response to a Get which targets “./Inbox” or any direct or indirect child node of “./Inbox”.<br/>
DM客户端不得在“./Inbox”上允许Get操作。DM客户端响应于Get目标“./Inbox”或“./Inbox”的任何直接或间接子节点时，返回状态代码“Command not allowed”（405）。

The following figure shows an overview of the Inbox URI:<br/>
下图显示了收件箱URI的概述：

![](7.1.3.4.jpeg)

The node has the following meaning:<br/>
该节点具有以下含义：

Inbox: An optional, interior node.<br/>
收件箱：可选的内部节点。