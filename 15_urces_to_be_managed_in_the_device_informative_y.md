# 1.5 urces to be managed in the Device (Informative) 要在设备中管理的信息（资料性）

This section provides an overview of the resources which are candidates for being managed using the Device Management mechanism. Categories of parameters and the parameters themselves that are listed in association with a resource are informative only – they are meant to provide guidance, and are not an exhaustive list of required parameters for particular capabilities, applications, or other Device characteristics.<br/>
本节概述了使用设备管理机制管理的资源。与资源相关联列出的参数类别和参数本身仅是信息性的 - 它们旨在提供指导，并且不是用于特定能力，应用或其他设备特性的所需参数的详尽列表。

There may be some special conditions or expectations around the presence, access, or manipulation of managed resources that should be taken into account when defining parameters and some of those conditions are noted here:<br/>
围绕被管理资源的存在，访问或操作可能有的一些特殊条件或期望，在定义参数时应该考虑这些条件或期望，并且在这里注意到这些条件中的一些：

Note that not all resources may be available at a given time depending on a number of factors, such as the presence of accessories or permissions associated with a resource. For example, in Devices with a smart card, some parts of the resources managed in the Device may be specific to a certain IMSI, for example the username & password associated with a bearer. These shall only be active if the specified IMSI is inserted in the Device.<br/>
注意，并非所有资源在给定时间都可用，这取决于多个因素，诸如与资源相关联的附件或许可的存在。例如，在具有智能卡的设备中，在设备中管理的资源的一部分可能特定于某个IMSI，例如与承载相关联的用户名和密码。只有在设备中插入指定的IMSI时，它们才会处于活动状态。

Time-sensitive resources shall be noted as such and their configurability specified such that it is possible to ascertain when such settings apply. For instance, some settings may have one or more time periods with distinct start and stop clock times. Other such settings may only be active for a period measured by cumulative use.<br/>
对时间敏感的资源应该这样注意，指定其可配置性，确定何时应用这些设置。例如，一些设置只应用于一个或多个不同的时间段，它们拥有不同的开始和停止时间。其他此类设置只能在通过累计使用时间来决定是否处于活动状态。

For operationally critical resources it shall be possible to locally or remotely revert the handset back to using a previously working value of the resources, should the new settings fail (e.g. software defined radio). Critical resources should be supported by adequate fault management on or off the Device as appropriate.<br/>
对于操作上关键的资源，如果新的设置失败（例如软件定义的无线电），则可以本地或远程地将听筒恢复到使用资源的先前工作值。关键资源应通过适当的设备上的或关闭的充分的故障管理来支持。

Management data may be set originally by OMA bootstrap methods, then read and maintained via Device Management. Subsequent to booting, resources may be created, added, deleted, or modified in accordance with any implementation of Device Management or OA&M mechanisms.<br/>