# Security 安全

OMA DM is a protocol based upon SyncML. Its purpose is to allow remote management of any device supporting the OMA DM protocol. Due to the vast range of data needing to be managed on current and future Devices, it is necessary to take account of the value of such data. In many situations, the data being manipulated within a Device (or being transferred to/from the device) is of high value. In some cases this is confidential data and some degree of protection regarding the confidentiality of that data should be offered. In another case, the integrity of the data being transferred must be maintained, since deliberate or accidental corruption of this data can result in lost revenue or subsequent exploits being facilitated. Finally it’s important that both entities (the Device and the Device Management Server) have confidence in the authenticity of the other entity.<br/>
OMA DM是基于SyncML的协议。其目的是允许对支持OMA DM协议的任何设备进行远程管理。 由于需要在当前和未来的设备上管理大量数据，因此有必要考虑这些数据的价值。在许多情况下，在设备内被操纵的数据（或被传送到设备/从设备传送）具有高价值。在某些情况下，这是机密数据，并应提供一定程度的保护以保证数据的保密性。 在另一种情况下，必须维持正在传送的数据的完整性，因为此数据的故意或意外损坏可能导致损失或促进随后的滥用。 最后，重要的是两个实体（设备和设备管理服务器）对其他实体的认证是确信的。

## Definitions 定义
Authentication: Authentication is the process of ascertaining the validity of either the Device or the Device Management Server’s identity.<br/>
认证：认证是确定设备或设备管理服务器的身份的有效性的过程。

Confidentiality: Confidentiality is the ability to keep contents secret from all but the two entities exchanging a message. It does not limit the visibility of the message (being able to eavesdrop), but it does prevent the interpretation of the data being transmitted. Effectively this prevents the contents of a message being understood by anybody but the intended sender and intended recipient.<br/>
保密性：保密性是除了两个实体交换消息时，保持内容秘密的能力。它不限制消息的可见性（能够窃听），但它能阻止对正在传输的数据的解释。实际上，这防止了消息的内容被除了预期发送者和预期接收者之外的任何人理解。

Content: Content means data delivered inside of OMA DM messages `<Data>`-elements.<br/>
内容：内容意味着在OMA DM消息`<Data>` - 元素内递送的数据。

Content Trust: Content Trust means ability to identify the source of the content.<br/>
内容信任：内容信任意味着能够识别内容的来源。

Credentials: Credentials are elements that are required to prove authenticity. Typically a username and a password.<br/>
凭证：凭证是证明真实性所需的元素。通常是用户名和密码。

Device: The Device is, or is to become managed by one or more remote entities (Device Management Servers). A device may have many characteristics, and many parameters may be made available for reading, writing, deleting and modifying by a Device Management Server.<br/>
设备：设备是或将是由一个或多个远程实体（设备管理服务器）管理。 设备可以具有许多特性，并且许多参数可以被设备管理服务器用于读取，写入，删除和修改。

Device Management Server: The Device Management Server is an entity that is responsible for maintaining one or more Devices, in whole or in part. Its role is to facilitate the easy maintenance of a Device.<br/>
设备管理服务器：设备管理服务器是负责整体或部分地维护一个或多个设备的实体。它的作用是方便一个设备的轻松维护。

Integrity: Integrity is the ability for a message to maintain its content or at a minimum, have the ability to detect modification or corruption of its content.<br/>
完整性：完整性是消息维持其内容或最低限度的能力，具有检测其内容的修改或损坏的能力。

Management Session: A continuous connection between the Device and the Device Management Server established for the purpose of carrying out one or more device management operations.<br/>
管理会话：在设备和设备管理服务器之间建立用于执行一个或多个设备管理操作的连续连接。

Management Trust: Management trust means right to manage Device Management Tree in Device.<br/>
管理信任：管理信任意味着管理设备中的设备管理树的权利。

## Abbreviations 缩写
DM Device Management 设备管理

ESN Electronic Serial Number 电子序列号

HMAC Hash Message Authentication Code 哈希消息验证码

IMSI International Mobile Station Identifier 国际移动台标识符

MAC Message Authentication Code 消息验证码

MD Message Digest 消息摘要

OMA Open Mobile Alliance 开放移动联盟

WAP Wireless Application Protocol 无线应用协议

## References 参考
[C.S0023-B_v1.0]: “Removable User Identity Module For Spread Spectrum Systems”, 3GPP2 C.S0023-B version 1.0, URL:http://www.3gpp2.org/Public_html/specs/C.S0023-B_v1.0_040426.pdf

[DMBOOT]:“OMA Device Management Bootstrap, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_Bootstrap-V1_2. URL:http://www.openmobilealliance.org

[DMNOTI]:“OMA Device Management Notification Initiated Session, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_Notification-V1_2. URL:http://www.openmobilealliance.org

[DMPRO]:“OMA Device Management Protocol, Version 1.2”. Open Mobile AllianceTM. OMA-DM_Protocol-V1_2. URL:http://www.openmobilealliance.org

[DMTND]:“OMA Device Management Tree and Description, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_TND-V1_2. URL:http://www.openmobilealliance.org

[DMSTDOBJ]:“OMA Device Management Standardized Objects, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_StdObj-V1_2. URL:http://www.openmobilealliance.org

[GSM11.11]:“Digital cellular Telecommunications system (Phase 2+); Specification of the Subscriber Identity Module - Mobile Equipment (SIM - ME) interface”, (ETSI TS 100 977). URL:http://www.etsi.org/

[IOPPROC]:“OMA Interoperability Policy and Process”, Version 1.1, Open Mobile AllianceTM, OMA-IOP-Process-V1_1, URL:http://www.openmobilealliance.org/

[PROVBOOT]:“Provisioning Bootstrap 1.1”. Open Mobile Alliance . OMA-WAP-ProvBoot-v1_1. URL:http://www.openmobilealliance.org

[PROVSC]:“Provisioning Smart Card Specification Version 1.1”. Open Mobile Alliance . OMA-WAP-ProvSC-v1_1.
URL:http://www.openmobilealliance.org

[RFC1321]:“The MD5 Message-Digest Algorithm”. Network Working Group. April 1992.
URL:http://www.ietf.org/rfc/rfc1321.txt

[RFC1521]:“MIME (Multipurpose Internet Mail Extensions) Part One”. Network Working Group. September 1993. URL:http://www.ietf.org/rfc/rfc1521.txt

[RFC2104]:“HMAC: Keyed-Hashing for Message Authentication”. Network Working Group. February 1997. URL:http://www.ietf.org/rfc/rfc2104.txt

[RFC2119]:“Key words for use in RFCs to Indicate Requirement Levels”, S. Bradner, March 1997,
URL:http://www.ietf.org/rfc/rfc2119.txt

[RFC2616]:“Hypertext Transfer Protocol – HTTP/1.1”. Network Working group. June 1999.
URL:http://www.ietf.org/rfc/rfc2616.txt

[SHA]:“Secure Hash Standard”, NIST FIPS PUB 180-1, National Institute of Standards and Technology, U.S. Department of Commerce, DRAFT, May 1994. URL: http://www.itl.nist.gov/fipspubs/fip180-1.htm

[SSL3.0]:The SSL Protocol, Version 3.0, raft-freier-ssl-version3-02.txt, Transport Layer Security Working Group, Alan O. Freier et al, November 18, 1996. URL:http://www.netscape.com/eng/ssl3/draft302.txt

[TLS]:RFC 2246 - The TLS Protocol Version 1.0, Network Working Group, January 1999.
URL:http://www.ietf.org/rfc/rfc2246.txt

[TS102.221]:“Smart Cards; UICC-Terminal interface; Physical and logical characteristics”, (ETSI TS 102 221), URL:http://www.etsi.org/

[TS131.102]:“Characteristics of the USIM application”, (ETSI TS 131.102), URL:http://www.etsi.org/

[TS151.011]:“Specification of the Subscriber Identity Module - Mobile Equipment (SIM-ME) interface”, (ETSI TS 151 011), URL:http://www.etsi.org/

[WAP-219-TLS]:OMA Wireless Public Key Infrastructure V1.0, Open Mobile Alliance , WAP-219_100-TLS URL:http://www.openmobilealliance.org/

[WBXML1.1]:“WAP Binary XML Content Format Specification”, WAP Forum . SPEC-WBXML-19990616.pdf. URL:http://www.openmobilealliance.org

[WBXML1.2]:“WAP Binary XML Content Format Specification”, WAP Forum . WAP-154-WBXML. URL:http://www.openmobilealliance.org

[WBXML1.3]:“WAP Binary XML Content Format Specification”, WAP Forum . WAP-192-WBXML. URL:http://www.openmobilealliance.org

[WTLS]:“Wireless Transport Layer Security”, Open Mobile Alliance , WAP-261-WTLS, URL:http://www.openmobilealliance.org

[XMLENC]:“XML Encryption Syntax and Processing”. W3C.
URL:http://www.w3.org/TR/2002/REC-xmlenc-core-20021210/

[XMLSIGN]:“XML-Signature Syntax and Processing”. W3C.
URL:http://www.w3.org/TR/2002/REC-xmldsig-core-20020212/

[SYNCHTTP]:“SyncML HTTP Binding Specification”, Open Mobile AllianceTM, OMA-TS-SyncML_HTTPBinding-V1_2, URL:http://www.openmobilealliance.org/

[SYNCOBEX]:“SyncML OBEX Binding Specification”, Open Mobile AllianceTM, OMA-TS-SyncML_OBEXBinding-V1_2, URL:http://www.openmobilealliance.org/

[SYNCWSP]:“SyncML WSP Binding Specification”, Open Mobile Alliance , OMA-TS-SyncML_WSPBinding-V1_2, URL:http://www.openmobilealliance.org/



