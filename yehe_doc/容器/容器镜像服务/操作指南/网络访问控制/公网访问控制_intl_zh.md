
## 操作场景

腾讯云容器镜像服务（Tencent Container Registry，TCR）企业版支持公网访问控制，可基于白名单策略限制来自公网环境的客户端对实例的访问，保障实例内的数据隐私安全。新创建的 TCR 企业版实例默认不开启公网访问入口，即无法使用处在公网环境内的开发测试服务器直接进行镜像的推送，拉取操作。
本文档介绍如何在 TCR 企业版实例中配置公网访问控制。

## 前提条件
在配置 TCR 企业版实例的公网访问控制前，您需要成功 [购买企业版实例](https://cloud.tencent.com/document/product/1141/51110)。


## 操作步骤
### 开启公网访问入口
1. 登录 [容器镜像服务](https://console.cloud.tencent.com/tcr) 控制台，选择左侧导航栏中的【访问控制】>【公网访问】。
2. 在“公网访问”页面，如果需要切换实例，请在页面上方选择实例所在地域，并在【实例名称】下拉列表中进行选择。
3. 选择【开启公网访问入口】即可开始开启入口。
待该按钮状态由【开启中】变为【关闭公网访问入口】，且【添加公网白名单】为可选择状态，则说明入口已开启。如下图所示：
入口开启后，仍默认拒绝全部来源的公网访问。
![](https://main.qcloudimg.com/raw/84a4ef80fa06ea6126b7ecc40ab52a12.png)


### 配置访问策略
1. 在“公网访问”页面，单击【添加公网白名单】并在弹出窗口中配置公网 IP 地址段及备注信息。如下图所示：
![](https://main.qcloudimg.com/raw/2c910090e35cd2229360ec9723a6b44d.png)
 - **所属实例**：配置公网访问策略的目标实例，可在“公网访问”页面顶部的“实例名称”下拉框中修改。
 - **公网IP地址段**：放通的公网 IP 地址段。支持单个 IPV4 地址或 CIDR，例如 `192.168.0.0/24`，不建议直接输入 `0.0.0.0/0` 以放开全部公网访问。
 - **备注**：访问策略的备注信息，可选，支持输入中文。
4. 配置完成后单击【确定】，该公网访问白名单策略即被添加并生效。
>?
>- 如需修改该白名单信息，可删除后再次新建。
>- 若公网访问入口无法开启或白名单策略无法新建，您可 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们。
>
