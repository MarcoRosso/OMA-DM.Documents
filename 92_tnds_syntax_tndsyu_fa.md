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