## 操作场景
云硬盘是云上可扩展的存储设备，用户可以在创建云硬盘后随时扩展其大小，以增加存储空间，同时不失去云硬盘上原有的数据。
云硬盘扩容完成后，需要 [扩展分区及文件系统（Windows）](https://intl.cloud.tencent.com/document/product/362/31601)或 [扩展分区及文件系统（Linux）](https://intl.cloud.tencent.com/document/product/362/31602)将扩容部分的容量划分至已有分区内，或者将扩容部分的容量格式化成独立的新分区。
>!MBR 格式分区支持的磁盘最大容量为2TB。如果您的硬盘分区为 MBR 格式，且需要扩容到超过2TB时，建议您重新创建并挂载一块数据盘，使用 GPT 分区方式后将数据拷贝至新盘中。

## 扩容数据盘
当扩容类型为数据盘的云硬盘时，您可通过以下3种方式进行扩容。

### 通过云服务器控制台扩容（推荐）
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index)。
2. 选择目标云服务器所在行的【更多】>【资源调整】>【云硬盘扩容】。
3. 在弹出的“云硬盘扩容”窗口中选择需扩容的数据盘，并单击【下一步】。
4. 在“调整容量”步骤中，设置目标容量（必须大于或等于当前容量），并单击【下一步】。
5. 在“扩容分区及文件系统”步骤中，查阅注意事项，单击【开始调整】即可。如下图所示：
6. 根据目标云服务的操作系统类型，您需要 [扩展分区及文件系统（Windows）](https://intl.cloud.tencent.com/document/product/362/31601)或 [扩展分区及文件系统（Linux）](https://intl.cloud.tencent.com/document/product/362/31602)将扩容部分的容量划分至已有分区内，或者将扩容部分的容量格式化成独立的新分区。

### 通过云硬盘控制台扩容
1. 登录 [云硬盘控制台](https://console.cloud.tencent.com/cvm/cbs)。
2. 选择目标云硬盘的【更多】>【扩容】。
3. 选择需要的新容量大小（必须大于或等于当前大小）。
4. 完成支付。
5. 根据目标云服务的操作系统类型，您需要执行 [扩展分区及文件系统（Windows）](https://intl.cloud.tencent.com/document/product/362/31601)或 [扩展分区及文件系统（Linux）](https://intl.cloud.tencent.com/document/product/362/31602)将扩容部分的容量划分至已有分区内，或者将扩容部分的容量格式化成新的独立分区。

### 通过 API 扩容
您可以使用 ResizeDisk 接口扩容指定的弹性云盘，具体操作请参考 [扩容云硬盘](https://intl.cloud.tencent.com/document/product/362/16310)。

## 扩容系统盘
当扩容类型为系统盘的云硬盘时，您可通过以下2种方式进行扩容。

### 通过云服务器控制台扩容（推荐）
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/index)，选择目标云服务器所在行的【更多】>【资源调整】>【云硬盘扩容】。
2. 在弹出的“云硬盘扩容”窗口中选择需扩容的系统盘，并单击【下一步】。
3. 在“调整容量”步骤中，设置目标容量（必须大于或等于当前容量），并单击【下一步】。
4. 在“扩容分区及文件系统”步骤中，查阅注意事项，勾选“同意强制关机”后，单击【开始调整】即可。如下图所示：
5. 完成控制台的扩容操作后，请对应云服务器实际的操作系统，[查看 Linux 实例 cloudinit 配置](#confirmLinuxConfig) 或 [查看 Windows 实例 cloudinit 配置](#confirmwindowsConfig)，根据确认结果按需进行扩容分区及文件系统操作。


### 通过重装系统扩容
您也可以在云服务器进行 [重装系统](https://intl.cloud.tencent.com/document/product/213/4933) 操作时，同时实现系统盘扩容。


## 相关操作
<span id="confirmLinuxConfig"></span>
### 查看 Linux 实例 cloudinit 配置
完成扩容操作后，请 [登录 Linux 实例](https://intl.cloud.tencent.com/document/product/213/5436) 确认 `/etc/cloud/cloud.cfg` 是否包含 growpart 及 resizefs 配置项。
 - 是，则无需进行其他操作。如下图所示：
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
    - **growpart**：扩展分区大小到磁盘大小。
    - **resizefs**：扩展调整`/`分区文件系统到分区大小。
 - 否，则需根据目标云服务的操作系统类型，手动扩文件系统及分区。您需要执行 [扩展分区及文件系统（Linux）](https://intl.cloud.tencent.com/document/product/362/31602)，将扩容部分的容量划分至已有分区内或将扩容部分的容量格式化为新的独立分区。
<span id="confirmwindowsConfig"></span>
### 查看 Windows 实例 cloudinit 配置
完成扩容操作后，请 [登录 Windows 实例](https://intl.cloud.tencent.com/zh/document/product/213/5435) 确认 `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\cloudbase-init.conf` 中的 plugin 是否包含 ExtendVolumesPlugin 配置项。
 - 是，则无需进行其他操作。
 - 否，则需根据目标云服务的操作系统类型，手动扩文件系统及分区。您需要执行 [扩展分区及文件系统（Windows）](https://intl.cloud.tencent.com/document/product/362/31601)，将扩容部分的容量划分至已有分区内或将扩容部分的容量格式化为新的独立分区。
