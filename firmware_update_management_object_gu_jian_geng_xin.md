# Firmware Update Management Object 固件更新管理对象

This specification provides information on management objects associated with firmware updates in OMA-DM based mobile devices and the behaviour associated with the processing of the management objects. Also specified is behaviour associated with the ‘Exec’ command and Generic Alerts.<br/>
该规范提供关于与基于OMA-DM的移动设备中的固件更新相关联的管理对象的信息以及与管理对象的处理相关联的行为。还指定了与“Exec”命令和“通用警报”相关联的行为。

The problem solved is the lack of an interoperable firmware update solution for mobile devices. This specification provides an interface between client and server to support this firmware update. This solution comprises the download of update package(s), the subsequent installation of the update package(s) to update firmware, and the reporting of success or error results and associated status information. <br/>
解决的问题是缺少用于移动设备的可互操作的固件更新解决方案。此规范提供客户端和服务器之间的接口以支持此固件更新。该解决方案包括下载更新包，随后安装更新包以更新固件，以及报告成功或错误结果以及相关的状态信息。

This specification enables mobile operators, service providers, infrastructure manufacturers, device manufacturers, and software vendors to develop and deploy interoperable firmware update solutions. <br/>
该规范使移动运营商，服务提供商，基础设施制造商，设备制造商和软件供应商能够开发和部署可互操作的固件更新解决方案。

The primary target audience for these management objects is engineers providing firmware update solutions and update package download solutions.<br/>
这些管理对象的主要目标受众是提供固件更新解决方案和更新包下载解决方案的工程师。

## Definitions 定义
See also the DM Tree and Description [DMTND] document for definitions of terms related to the management tree.<br/>
有关与管理树相关的术语的定义，另请参阅DM树和描述[DMTND]文档。

## Abbreviations 缩写
FUMO: Firmware Update Management Object 固件更新管理对象

OMA: Open Mobile Alliance 开放移动联盟

## References 参考
[DMPRO]: “OMA Device Management Protocol, Version 1.2”. Open Mobile Alliance. OMA-TS-DM-Protocol-V1_2, URL:http://www.openmobilealliance.org

[DMTND]: “OMA Device Management Tree and Description, Version 1.2”. Open Mobile Alliance. OMA-TS-DM-TND-V1_2. URL:http://www.openmobilealliance.org

[IOPPROC]: “OMA Interoperability Policy and Process”, Version 1.13, Open Mobile Alliance™, OMA-IOP-Process-V1_13, URL:http://www.openmobilealliance.org/

[RFC2119]: “Key words for use in RFCs to Indicate Requirement Levels”, S. Bradner, March 1997, URL:http://www.ietf.org/rfc/rfc2119.txt

[RFC2234]: “Augmented BNF for Syntax Specifications: ABNF”. D. Crocker, Ed., P. Overell. November 1997, URL:http://www.ietf.org/rfc/rfc2234.txt

[DLOTA]: OMA Download, Version 1.0, Open Mobile Alliance. URL:http://www.openmobilealliance.org/documents.html 

[DMNOTI]: “OMA Device Management Notification Initiated Session, Version 1.2”. Open Mobile Alliance. OMA-TS-DM-Notification-V1_2. URL:http://www.openmobilealliance.org

[DMSTDOBJ]: “OMA Device Management Standardized Objects, Version 1.2”. Open Mobile Alliance. OMA-TS-DM-StdObj-V1_2. URL:http://www.openmobilealliance.org

[RFC2616]：“Hypertext Transfer Protocol – HTTP/1.1”. Network Working group. June 1999. URL: http://www.ietf.org/rfc/rfc2616.txt

