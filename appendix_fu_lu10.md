# Appendix 附录

## Recommendations 推荐

a) It is anticipated that updating the firmware will require that the device become inoperable during the time of the firmware upgrade. It is also likely that the update process will not be capable of immediately returning to operating condition in the case of an interruption. In the case that the device cannot immediately return to operating condition, it is recommended that the end-user be presented with a warning that the device will be offline and the approximate time of the update prior to beginning the firmware installation.<br/>
a）预期更新固件将要求设备在固件升级期间变得不可操作。还有可能的是，更新过程将不能够在中断的情况下立即返回到操作条件。在设备不能立即返回到操作状态的情况下，建议向终端用户显示设备将离线的警告以及在开始固件安装之前显示大致更新时间。

b) Deletion of the Update package under the /x/ node is an activity that needs to be conducted after successful update, after an unsuccessful update attempt and after an aborted update attempt. However, any specification when such deletes should occur is not addressed in this specification. The management client could choose to delete it as soon as an update is successfully or unsuccessfully terminated, or whenever prompted to do so by the DM server.<br/>
b）删除/x/节点下的更新包是一个需要在成功更新后进行的活动，或在失败的更新尝试和中止更新后进行。然而，当这种删除应该发生的时间的任何规范在本说明书中没有涉及。管理客户端可以选择在更新成功或被终止时或者在DM服务器提示这样做时立即将其删除。

c) PkgURL and PkgData are mutually exclusive. Only one of them needs to be set.<br/>
c）PkgURL和PkgData是互斥的。只需要设置其中一个。

d) The PkgData node contains the actual binary firmware upgrade package. Once the package is installed, the client could remove the data to save space, leaving the node empty. Similarly, and the end of an update activity, the client could remove the update package downloaded from a server specified by a PkgURL.
d）PkgData节点包含实际的二进制固件升级包。安装软件包后，客户端可以删除数据以节省空间，将节点保留为空。类似地，更新活动结束后，客户端可以移除从由PkgURL指定的服务器下载的更新包。

