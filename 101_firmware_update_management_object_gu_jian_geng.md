# 10.1 Firmware Update Management Object 固件更新管理对象

The parameters associated with a single firmware update are assembled into a firmware update management object as shown in Figure. A firmware update management object may be either permanent or dynamic. There may be one or more such firmware update management objects in a device management tree. Only one update package, or reference to an update package, is associated with each such management object.  The grouping or placement within the device management tree of multiple management objects, such as under a common node, is not addressed in this specification. <br/>
与单个固件更新相关联的参数被组装到如图所示的固件更新管理对象中。固件更新管理对象可以是永久的或动态的。在设备管理树中可以存在一个或多个这样的固件更新管理对象。只有一个更新包或对更新包的引用与每个这样的管理对象相关联。在本说明书中没有涉及多个管理对象的设备管理树内的分组或放置，例如在公共节点下。

Management Object identifier: urn:oma:mo:oma-fumo:1.0<br/>
管理对象标识符：urn：oma：mo：oma-fumo：1.0

Protocol Compatibility:  This object is compatible with OMA Device Management, version 1.2 [OMADM] and any later compatible versions of OMA Device Management.<br/>
协议兼容性：此对象与OMA设备管理版本1.2[OMADM]和任何更高版本的OMA设备管理兼容。

![](10.1.jpeg)
## 10.1.1 Firmware Update Management Object Parameters 固件更新管理对象参数
The following are the nodes of the Firmware Update management object.<br/>以下是固件更新管理对象的节点。

## 10.1.1.1 Node: x
This interior node acts as a placeholder for a firmware upgrade package unique identifier.  The node Type property MUST correspond to the management object identifier specified in section 10.1. The manufacturer MAY pre-create permanent nodes for x, allow update package nodes x to be created as needed, or a combination of these two methods.  For example, permanent nodes might be created for all firmware packages known at the time of manufacture, with additional nodes added dynamically as new features become available.  An example would be to include nodes FWPkg1, FWPkg2...FWPkgn. The DDF file provided by the device manufacturer MAY specify where the x node is to be located in the management tree of the device.<br/>
该内部节点充当固件升级包唯一标识符的占位符。节点类型属性必须对应于在第10.1节中指定的管理对象标识符。制造商可以预先创建x的永久节点，允许根据需要创建更新包节点x或这两种方法的组合。例如，可以为制造时已知的所有固件包创建永久节点，随着新特征变得可用，附加节点被动态地添加。 一个示例是包括节点FWPkg1，FWPkg2 ... FWPkgn。设备制造商提供的DDF文件可以指定x节点在设备的管理树中的位置。
Occurrence: ZeroOrMore<br/>
出现次数：零次或多次

Format: Node<br/>
格式：Node

Access Types: Get <br/>
访问类型：Get

Values: N/A <br/>
值：无