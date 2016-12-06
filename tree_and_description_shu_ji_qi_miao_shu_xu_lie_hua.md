# Tree and Description Serialization树及其描述的序列化

This specification defines how to convert a runtime Management Tree or sub tree (i.e. an MO) into an xml or wbxml structure. This specification is useful whenever an MO needs to be created from one entity, moved outside of the DM Protocol session to another entity in an interoperable fashion. This specification is optional to support.<br/>
该规范定义了如何将运行时管理树或子树（即MO）转换为xml或wbxml结构。当需要从一个实体创建MO，并以可互操作的方式将其从DM协议会话移动到另一实体时，该规范是有用的。此规范是可选的支持。

## Definitions 定义
Management tree: The mechanism by which the management client interacts with the device, e.g. by storing and retrieving values from it and by manipulating the properties of it, for example the access control lists.<br/>
管理树：管理客户端与设备交互的机制，例如，通过存储和检索它的值，并通过操作它的属性，例如访问控制列表。

Leaf node: A node that can store a value, but cannot have child nodes. The Format property of a leaf node is not node.<br/>
叶节点：可以存储值，但不能有子节点的节点。叶节点的Format属性不是节点。

Interior node: A node that may have child nodes, but cannot store any value. The Format property of an interior node is node.<br/>
内部节点：可能具有子节点，但不能存储任何值的节点。内部节点的Format属性是节点。

## Abbreviations 缩写
OMA: Open Mobile Alliance 开放移动联盟

ACL: Access Control List 访问控制列表

DDF: Device Description Framework 设备描述框架

TNDS: Tree and Description Serialization 树及其描述的序列化

## Reference 参考
[DMREPU]: “OMA Device Management Representation Protocol, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_RepPro-V1_2. URL:http://www.openmobilealliance.org

[DMTND]: “OMA Device Management Tree and Description, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_TND-V1_2. URL:http://www.openmobilealliance.org

[IOPPROC]:“OMA Interoperability Policy and Process”, Version 1.1, Open Mobile AllianceTM, OMA-IOP-Process-V1_1, URL:http://www.openmobilealliance.org

[ISO8601]: ISO 8601:2000, Data elements and interchange formats -- Information interchange -- Representation of dates and times
URL:http://www.iso.ch/

[RFC2119]: “Key words for use in RFCs to Indicate Requirement Levels”, S. Bradner, March 1997,
URL:http://www.ietf.org/rfc/rfc2119.txt

[RFC2234]:“Augmented BNF for Syntax Specifications: ABNF”. D. Crocker, Ed., P. Overell. November 1997, URL:http://www.ietf.org/rfc/rfc2234.txt

[RFC2396]:“Uniform Resource Identifiers (URI): Generic Syntax”. T. Berners-Lee, et al. August 1998. URL:http://www.ietf.org/rfc/rfc2396.txt

[XMLSCHEMADT]: “XML Schema Part 2: Datatypes”, W3C Recommendation 02 May 2001, URL:http://www.w3.org/XML/Schema/