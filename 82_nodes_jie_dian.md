# 8.2 Nodes 节点
## 8.2.1 Common characteristics of Nodes 节点的共同特征
Nodes are the entities which can be manipulated by management actions carried over the OMA DM protocol. A Node can be as small as an integer or a large and complex like a background picture or screen saver. The OMA DM protocol is agnostic about the contents, or values, of the Nodes and treats the Leaf Node values as opaque data.<br/>
节点是可以通过OMA DM协议承载的管理动作来操纵的实体。节点可以小到整数或大和复杂到如背景图片或屏幕保护程序。OMA DM协议对节点的内容或值是不可知的，并且将叶节点值视为不透明数据。

An Interior Node can have an unlimited number of child Nodes linked to it in such a way that the complete collection of all Nodes in a management database forms a tree structure. Each Node in a tree MUST have a unique URI.<br/>
内部节点可以具有无限数量的与其链接的子节点，使得管理数据库中的所有节点的完整集合形成树结构。 树中的每个节点必须具有唯一的URI。

Each Node has properties associated with it; these properties are defined in 8.3.1. All properties, except the ACL, are valid only for the Node to which they are associated.<br/>
每个节点具有与其相关联的属性; 这些属性在8.3.1中定义。除ACL之外的所有属性仅对与其关联的节点有效。

## 8.2.2 Details of the Management Tree 管理树的详细信息

As mentioned before the complete structure of all Nodes and the root (the device itself) forms a tree. DM Servers can explore the structure of the tree by using the GET command. If the accessed Node is an Interior Node, a list of all child Node names is returned. If the Interior Node has no children an empty list of child Node names is returned, e.g. `<Data/>`. If the Node is a Leaf Node it MUST have a value, which could be null, and this value is returned. A DM Server MAY maintain information about its current position in the Management Tree.<br/>
如前所述，所有节点和根（设备本身）的完整结构形成一棵树。 DM服务器可以通过使用GET命令来探索树的结构。如果所访问的节点是内部节点，则返回所有子节点名称的列表。如果内部节点没有子节点，则返回子节点名称的空列表，例如。 `<Data />`。如果节点是叶节点，它必须有一个值，它可以为null，并返回此值。 DM服务器可以在管理树中维护关于其当前位置的信息。

Nodes with the Format property set to node are defined as Interior Nodes. Nodes that are not Interior Nodes are defined as Leaf Nodes. Interior Nodes can have 0 or more children, Leaf Nodes cannot have children.<br/>
将格式属性设置为节点的节点定义为内部节点。不是内部节点的节点被定义为叶节点。内部节点可以有0个或更多的孩子，叶节点不能有孩子。

The Management Tree can be extended at run-time. This is done with the Add or Replace command and both new Interior Nodes and new Leaf Nodes can be created. The parent of any new Node MUST be an Interior Node. The device itself can also extend the Management Tree. This could happen as a result of user input or by attaching the some kind of accessory to the device.<br/>
管理树可以在运行时扩展。这通过添加或替换命令完成，并且可以创建新的内部节点和新的叶节点。任何新节点的父节点必须是内部节点。设备本身也可以扩展管理树。这可能由于用户输入或者通过将某种附件附接到设备而发生。

## 8.2.2.1 Addressing object values 寻址对象值

Node values are addressed by presenting a relative URI for the requested Node. The base URI [RFC2396] MUST be the root of the Management Tree in the device. If a valid URI is presented along with a command for which the current Server Identifier has sufficient access rights, the command MUST be executed. The client MUST respond with an appropriate status code. If the command results in a value that is to be sent back to the server, then this value MUST be part of the response. The type of the value is returned as part of the meta information as specified in [AMT].<br/>
通过呈现所请求的节点的相对URI来寻址节点值。基本URI[RFC2396]必须是设备中管理树的根。如果有效的URI与当前服务器标识符的具有足够访问权限的命令一起被呈现，则必须执行该命令。客户端必须用适当的状态代码进行响应。如果命令产生要发送回服务器的值，则此值必须是响应的一部分。该值的类型作为元信息的一部分返回，如[AMT]中指定。

Example: 范例

The following Get command: 以下Get命令
```
  <Get>
     <CmdID>4</CmdID>
     <Item>
        <Target> 
           <LocURI>Vendor/Ring_signals/Default_ring</LocURI>
       </Target>
     </Item>
</Get>
```
could receive a response like this: 可以接收到这样的响应：
```
<Results>
     <CmdRef>4</CmdRef>
     <CmdID>7</CmdID>
     <Item>
       <Data>MyOwnRing</Data>
     </Item>
   </Results>
```

## 8.2.2.2 Addressing Interior Node child lists 寻址内部节点子节点列表

Interior Node child lists are addressed in the same way as Node values. The list of children is returned as an unordered list of names. The individual names in the list are separated by the character “/”. A returned child list has the format node in the meta information of the result. Note that the “/” character MUST NOT be part of any Node names according to [RFC2396].<br/>
内部节点子节点列表与节点值以相同的方式进行寻址。子节点列表作为无序的名称列表返回。列表中的各个名称由字符“/”分隔。返回的子列表在结果的元信息中具有格式节点。注意，根据[RFC2396]，“/”字符不得是任何节点名称的一部分。

Example: 范例

The following Get command: 以下Get命令
```
 <Get>
     <CmdID>4</CmdID>
     <Item>
        <Target> 
            <LocURI>Vendor/Ring_signals</LocURI>
       </Target>
     </Item>
</Get>
```
could receive a response like this: 可以接收到这样的响应：
```
<Results>
     <CmdRef>4</CmdRef>
     <CmdID>7</CmdID>
     <Item>
        <Meta>
          <Format xmlns=’syncml:metinf’>node</Format> 
          <Type xmlns=’syncml:metinf’>text/plain</Type>
        </Meta>
        <Data>Default_ring/Ring1/Ring2/Ring3/Ring4</Data> 
     </Item>
</Results>
```
If a Get command is issued on an Interior Node that does not have any children the client MUST return an empty child list, e.g. `<Data/>`, and the status code (200) OK.<br/>
如果在没有任何子节点的内部节点上发出Get命令，客户端必须返回一个空的子节点列表，例如， `<Data/>`，状态码（200）OK。

## 8.2.2.3 Permanent and Dynamic Nodes 永久和动态节点
Nodes in the Management Tree can be either permanent or dynamic.<br/>
管理树中的节点可以是永久性的也可以是动态的。

Permanent Nodes are typically built in at device manufacture. Permanent Nodes can also be temporarily added to a device by, for instance, connecting new accessory hardware. However, a DM Server cannot create or delete permanent Nodes at runtime.An attempt by a DM Server to delete apermanent Node will return status(405) Command not allowed. The same status code will also be returned for all attempts to modify the Name property of a permanent Node.
永久节点通常在设备制造中内置。永久节点也可以通过例如连接新的附件硬件被临时添加到设备。但是，DM服务器不能在运行时创建或删除永久节点。DM服务器尝试删除永久节点将返回状态（405）Command not allowed。对于修改永久节点的Name属性的所有尝试，也将返回相同的状态代码。

Dynamic Nodes can be created and deleted at runtime by DM Servers. The Add command is used to create new Nodes. The Delete command is used to delete Dynamic Nodes and all their properties. If a deleted Node has children, i.e. is an Interior Node, the children MUST also be deleted.<br/>
动态节点可以在运行时由DM服务器创建和删除。Add命令用于创建新的节点。Delete命令用于删除动态节点及其所有属性。如果被删除的节点具有子节点，即是一个内部节点，子节点也必须被删除。

The complete layout of the permanent Nodes in the Management Tree is reflected in the device description.<br/>
管理树中永久节点的完整布局反映在设备描述中。

## 8.2.2.4 Permanent and Dynamic Nodes 永久和动态节点
As stated in the previous section the Add command is used to create new Nodes. The definition of the Add command in [DMPRO] states that the Node addressed MUST NOT exist in the tree. The name of the newly created Node SHALL be the last segment of the URI presented in the Target element of the Add command. Note that devices might have various constraints as to the lengths of the URI used to address the Management Tree. These constraints MUST be recorded in the ./DevDetail Management Object as specified in [DMSTDOBJ].<br/>
如上一节所述，Add命令用于创建新节点。在[DMPRO]中的Add命令的定义表明，所寻址的节点必须不存在于树中。新创建的节点的名称应该是添加命令的目标元素中呈现的URI的最后一段。注意，设备可能对用于寻址管理树的URI的长度具有各种约束。这些约束必须记录在[DMSTDOBJ]中指定的./DevDetail管理对象中。

Example: 范例

The following Add command: 以下Add命令
```
 <Add>
     <CmdID>5</CmdID>
     <Item>
     <Meta>
        <Format xmlns=’syncml:metinf’>b64</Format>
        <Type xmlns=’syncml:metinf’>audio/myMelodyType</Type>
     </Meta>
     <Target>
        <LocURI>Vendor/Ring_signals/My_beep</LocURI> 
     </Target>
     <Data>jkhdsfKJhdsf89374h</Data>
     </Item>
   </Add>
```
would create a previously non-existing Node called My_beep as a child Node to the Interior Node Vendor/Ring_signals.<br/>
将创建一个以前不存在的名为My_beep的节点作为内部节点Vendor/Ring_signals的子节点。

When a Node is created, all the properties that this Node supports are automatically created by the client. Those property values that depend on information present in the Add or Replace command, e.g. Name, are assigned these values. Properties with a default value (e.g. Name) or a value that is automatically updated by the client (e.g. Size) are also assigned appropriate value at Node creation. Other properties will have no value.<br/>
创建节点时，此节点支持的所有属性都由客户端自动创建。Add或Replace命令中存在的信息的那些属性值，例如Name，用来分配这些属性值。具有默认值（例如Name）或由客户端自动更新的值（例如Size）的属性也在节点创建时分配适当的值。其他属性将没有值。

Interior Nodes are created in the same way. The difference is that the server MUST explicitly say that the new Node is an Interior Node by including a Meta element with a Format value of node.<br/>
内部节点以相同的方式创建。不同之处在于服务器必须通过包括具有节点的格式值的Meta元素来明确地说新节点是内部节点。

Example: 范例
```
 <Add>
     <CmdID>5</CmdID>
     <Item>
     <Target> 
         <LocURI>Vendor/Ring_signals/MyOwnSongs</LocURI>
     </Target>
     <Meta>
          <Format xmlns=’syncml:metinf’>node</Format> 
     </Meta>
     </Item>
 </Add>
```

## 8.2.2.5 Protecting Dynamic Nodes 保护动态节点
Some Dynamic Nodes can be part of a larger context, and only have meaning in this context. Alternatively, the context (a Management Object) might become useless if a detail is lost, e.g. by the deletion of a dynamic Leaf Node. This could for instance be the address of an SMTP server for an e-mail Management Object. To protect this kind of Node from deletion and thus maintain the integrity of the context, the DDF property AccessType can be set so that the Delete command is excluded. This means that a Delete command will fail with status (405) Command not allowed.<br/>
一些动态节点可以是较大上下文的一部分，并且仅在该上下文中具有意义。或者，如果细节丢失，上下文（管理对象）可能变得无用，例如，通过删除动态叶节点。这可以用于电子邮件管理对象的SMTP服务器的地址。为了保护这种节点不被删除，从而保持上下文的完整性，可以设置DDF属性AccessType，以便排除Delete命令。这意味着Delete命令将失败，状态为（405）Command not allowed。

Note that this is not the same thing as a permanent Node. A Node protected by the AccessType property can still be deleted if it is part of a sub-tree that is being deleted. The Delete command acts strictly on the Node it is addressed at, and if that Node is a dynamic Interior Node it will be deleted along with all its child Nodes. If any of these child Nodes have the AccessType property set to exclude Delete they will be deleted anyway. The following table summarizes the protection mechanisms for Dynamic Nodes.<br/>
注意，这不是一个永久的节点。受AccessType属性保护的节点仍然可以删被除，如果它是正在被删除的子树的一部分。Delete命令严格地作用于它被寻址的节点，并且如果该节点是动态内部节点，则它将与其所有子节点一起被删除。如果任何这些子节点的AccessType属性设置为排除删除，它们仍将被删除。下表总结了动态节点的保护机制。

|  |  | How the Node is addressed<br/> 节点如何被寻址 |  |
| -- | -- | -- | -- |
|  | | Directly by URI in a Delete command<br/> 在Delete命令中直接通过URI | Indirectly, as a child of a Node being deleted<br/> 间接地，作为被删除节点的子节点 |
| What AccessType specifies for the Node<br/> 节点的AccessType属性 | Delete allowed<br/> 允许删除 | Deleted<br/>删除 | Deleted<br/>删除 |
| | Delete not allowed<br/> 不允许删除 | Not Deleted<br/>未删除 | Deleted<br/>删除 |

Note that this mechanism is completely independent of the ACL. See chapter 8 .5 for more information on DDF properties.<br/>
请注意，此机制完全独立于ACL。有关DDF属性的更多信息，请参见第8.5章。
