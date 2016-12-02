# Standardized Objects 标准化对象

Other OMA DM specifications define the syntax and semantics of the OMA DM protocol. However, the usefulness of such a protocol would be limited if the managed entities in devices required different data formats and displayed different behaviors. To avoid this situation this specification defines a number of mandatory management objects for various uses in devices. These objects are primarily associated with OMA DM and SyncML configuration.<br/>
其他OMA DM规范定义了OMA DM协议的语法和语义。然而，如果设备中的管理实体需要不同的数据格式并且显示不同的行为，则这种协议的有用性将受到限制。为了避免这种情况，本规范定义了用于设备中的各种用途的多个强制管理对象。这些对象主要与OMA DM和SyncML配置相关联。

Since device manufacturers will always develop new functions in their devices and since these functions often are proprietary, no standardized management objects exist for them. To make these functions manageable in the devices that have them, a device description framework is needed that can provide servers with the necessary information they must have in order to manage the new functions. The intention with this framework is that device manufacturers will publish descriptions of their devices as they enter the market. Organizations operating device management servers should then only have to feed the new description to their servers for them to automatically recognize and manage the new functions in the devices.<br/>
由于设备制造商将始终在其设备中开发新功能，并且由于这些功能通常是专有的，因此不存在用于它们的标准化管理对象。为了使这些功能在具有它们的设备中可管理，需要设备描述框架，其可以向服务器提供他们必须具有的必要信息以便管理新功能。这个框架的意图是，设备制造商将在他们进入市场时发布他们的设备的描述。操作设备管理服务器的组织应该只需要向其服务器馈送新的描述，以便他们自动识别和管理设备中的新功能。

## References 参考
[DMAccDDF]: “OMA Device Management Account Management Object DDF, Version 1.2”. Open Mobile Alliance . OMA-SUP-MO_DM_DMAcc-V1_2. URL:http://www.openmobilealliance.org

[DMBOOT]: “OMA Device Management Bootstrap, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_Bootstrap-V1_2. URL:http://www.openmobilealliance.org

[DMDDFDTD]: “OMA DM Device Description Framework DTD, Version 1.2”. Open Mobile Alliance . URL:http://www.openmobilealliance.org/tech/DTD/dm_ddf-v1_2.dtd

[DevDetailDDF]:“OMA Device Management Detail Information Management Object DDF, Version 1.2”. Open Mobile Alliance . OMA-SUP-MO_DM_DevDetail-V1_2. URL:http://www.openmobilealliance.org

[DevInfoDDF]:“OMA Device Management Information Management Object DDF, Version 1.2”. Open Mobile Alliance . OMA-SUP-MO_DM_DevInfo-V1_2. URL:http://www.openmobilealliance.org

[DMPRO]:“OMA Device Management Protocol, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_Protocol-V1_2. URL:http://www.openmobilealliance.org

[DMSEC]:“OMA Device Management Security, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_Security-V1_2. URL:http://www.openmobilealliance.org

[DMTND]:“OMA Device Management Tree and Description, Version 1.2”. Open Mobile Alliance . OMA-TS-DM_TND-V1_2. URL:http://www.openmobilealliance.org

[ERELDCP]:“Enabler Release Definition for OMA Client Provisioning Specifications, version 1.1”. Open Mobile Alliance  . OMA-ERELD-ClientProvisioning-V1_1. URL:http://www.openmobilealliance.org

[IOPPROC]:“OMA Interoperability Policy and Process”, Version 1.1, Open Mobile AllianceTM, OMA-IOP-Process-V1_1, URL:http://www.openmobilealliance.org/

[REPPRO]:“SyncML Representation Protocol”, Version 1.2, Open Mobile AllianceTM, OMA-IOP-Process-V1_1, URL:http://www.openmobilealliance.org/

[RFC1766]:“Tags for the Identification of Languages”. H. Alvestrand. March 1995.
URL:http://www.ietf.org/rfc/rfc1766.txt

[RFC2119]:“Key words for use in RFCs to Indicate Requirement Levels”, S. Bradner, March 1997,
URL:http://www.ietf.org/rfc/rfc2119.txt

[RFC2141]:“URN Syntax”, R. Moats, May 1997, URL:http://www.ietf.org/rfc/rfc2141.txt

[RFC2234]:“Augmented BNF for Syntax Specifications: ABNF”. D. Crocker, Ed., P. Overell. November 1997, URL:http://www.ietf.org/rfc/rfc2234.txt

[RFC2373]:“Internet Protocol Version 6 Addressing Architecture”. R. Hinden and S. Deering. July 1998.
URL:http://www.ietf.org/rfc/rfc2373.txt

[RFC2396]:“Uniform Resource Identifiers (URI): Generic Syntax”. T. Berners-Lee, R. Fielding, L. Masinter. August 1998. URL:http://www.ietf.org/rfc/rfc2396.txt

[RFC791]:“Internet Protocol: Darpa Internet Protocol Program Specification”. September 1981.
URL:http://www.ietf.org/rfc/rfc791.txt

[w7]:“OMA w7 Application Characteristic for DM Version 1.0”. Open Mobile Alliance . OMA-w7-Application-Characteristic-for-DM-V1_0. URL:http://www.openmobilealliance.org
