# 8.6 WBXML Definition WBXML定义

The following tables define the token assignments for the mapping of the DMDDF related DTDs and element types into WBXML as defined by [WBXML1.1], [WBXML1.2], [WBXML1.3].<br/>
下表定义了由[WBXML1.1]，[WBXML1.2]，[WBXML1.3]定义的DMDDF相关DTD和元素类型到WBXML的映射的令牌分配。

## 8.6.1 Code Page Definitions 代码页定义

The following code page tokens represent DM DDF public identifiers. This version of the DM protocol specification utilizes the WBXML code page tokens for identifying DTDs.<br/>
以下代码页令牌表示DM DDF公共标识符。该版本的DM协议规范利用WBXML代码页令牌来标识DTD。

| DTD Name DTD名称| WBXML Code Page Token (Hex Value) WBXML代码页标记（十六进制值）| Formal Public Identifier 正式公共标识符 |
| -- | -- | -- |
| DMDDF | 02 | -//OMA//DTD-DM-DDF 1.2//EN |

## 8.6.2 Token Definitions 令牌定义
The following WBXML token codes represent element types (i.e., tags) from code page x02 (two), OMA DM DDF DTD.<br/>
以下WBXML令牌代码表示来自代码页x02（2），OMA DM DDF DTD的元素类型（即标签）。

| Element Type Name 元素类型名称| WBXML Tag Token (Hex Value) WBXML标记令牌（十六进制值） | 
| -- | -- | 
| AccessType | 05 | 
| ACL | 06 | 
| Add | 07 | 
| b64 | 08 |
| bin | 09 |
| bool | 0A |
| chr | 0B |
| CaseSense | 0C |
| CIS | 0D |
| Copy | 0E |
| CS | 0F |
| date | 10 |
| DDFName | 11 |
| DefaultValue | 12 |
| Delete | 13 |
| Description | 14 |
| DFFormat | 15 |
| DFProperties | 16 |
| DFTitle | 17 |
| DFType | 18 |
| Dynamic | 19 |
| Exec | 1A |
| float | 1B |
| Format | 1C |
| Get | 1D |
| int  | 1E |
| Man | 1F |
| MgmtTree | 20 |
| MIME | 21 |
| Mod | 22 |
| Name | 23 |
| Node | 24 |
| node | 25 |
| NodeName | 26 |
| null | 27 |
| Occurrence | 28 |
| One | 29 |
| OneOrMore | 2A |
| OneOrN | 2B |
| Path | 2C |
| Permanent | 2D |
| Replace | 2E |
| RTProperties | 2F |
| Scope | 30 |
| Size | 31 |
| time | 32 |
| Title | 33 |
| TStamp | 34 |
| Type | 35 |
| Value | 36 |
| verDTD | 37 |
| verNo | 38 |
| xml | 39 |
| ZeroOrMore | 3A |
| ZeroOrN | 3B |
| ZeroOrOne | 3C |