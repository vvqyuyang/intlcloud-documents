>?CCN 型 VPN 网关及相关功能灰度中，如有需要，请提交 [工单申请](https://console.cloud.tencent.com/workorder/category)。
> 
CCN 型 VPN 网关可以关联至云联网，实现 IDC 与云联网间的加密通信。本文介绍如何将 CCN 型 VPN 网关关联至云联网。

## 背景信息
CCN 类型的 VPN 网关可以关联至云联网，每个 CCN 型 VPN 网关可以建立多个 VPN 加密通道，每个 VPN 通道可以打通一个本地 IDC。
![](https://main.qcloudimg.com/raw/9c3a75859af98ace2bfe0bcc341d1f8d.png)

将 CCN 类型的 VPN 网关关联至云联网步骤如下：
1. [创建 CCN 型 VPN 网关](#step1)：VPN 网关是云联网建立 VPN 连接的出口网关，与对端网关配合使用。
2. [ 关联云联网实例](#step2)：将创建的 CCN 型 VPN 网关与云联网实例关联。
3. [创建对端网关](#step3)：对端网关是用来记录 IDC 端的 IPsec VPN 网关公网 IP 地址的逻辑对象（IDC 端必须有固定公网 IP），需与腾讯云 VPN 网关配合使用，一个 VPN 网关可与多个对端网关建立加密的 VPN 网络通道。
4. [创建 VPN 通道](#step4)： VPN 通道支持 IPsec 加密协议，用于保护数据传输的信息安全。
5. [启用 IDC 网段](#step5)：将 SPD 策略中的对端网段加入云联网中。

## 操作步骤

<span id="step1" />

### 步骤一：创建 CCN 型 VPN 网关
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 在左侧导航栏中选择【VPN连接】>【VPN网关】。
3. 在顶部导航栏选择【地域】，并在 “VPN 网关“页面单击【+新建】。
4. 在弹出的“新建VPN网关”窗口中，填写 VPN 网关名称（如 TomVPNGw），选择关联网络、带宽上限、计费方式，单击【创建】即可。VPN 网关创建完成后，系统随机分配公网 IP，如 `203.195.147.82`。
>?如需将 CCN 型 VPN 网关新建在指定的可用区下，请提交 [工单申请](https://console.cloud.tencent.com/workorder/category)。
>
 - 网关名称：填写 VPN 网关名称，不超过60个字符。
 - 关联网络：选择云联网。
 - 带宽上限：按需选择 VPN 网关的带宽上限。
 - 计费方式：按需选择 VPN 网关的计费方式。
   - 按流量计费：适用于带宽波动较大的场景。
![](https://main.qcloudimg.com/raw/a3c1bcd51643560d524e3b4dd54be18a.png)

<span id="step2" />

### 步骤二：关联云联网实例
- 若您已创建云联网实例，请按如下操作关联云联网：
 1. 返回 “VPN 网关“页面，在 VPN 网关列表中，单击已创建的云联网型 VPN 网关 ID。
 2. 在“基本信息“页面，单击所属网络右侧的<img src="https://main.qcloudimg.com/raw/7b27e195bfc7f7ee82118f80c4c96b28.png" style="margin:-4px 0;"/>，在下拉列表中选择目标云联网实例，并单击【保存】即可。
![](https://main.qcloudimg.com/raw/95c284b4ca949dd4facb816bd305e34b.png)
- 若您未创建云联网实例，请按如下步骤关联云联网：
 1. 在左侧导航栏单击【云联网】。
 2. 在“云联网”页面上方选择【地域】，单击【+新建】。
 3. 在弹出的“新建云联网实例”窗口中进行如下操作，完成后单击【确定】。
   1. 填写云联网实例名称、描述，选择计费模式、服务质量、限速方式。
   2. 在“关联实例”下方选择【VPN 网关】，以及已创建的云联网型 VPN 网关的地域和 ID。
![](https://main.qcloudimg.com/raw/54cba45a12f8d6396f1dcd02b6dff281.png)

<span id="step3" />

### 步骤三：创建对端网关
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 在左侧导航栏选择【VPN 连接】>【对端网关】。
3. 在“对端网关”页面上方选择【地域】，并单击【+新建】。
4. 在弹出的“新建对端网关”窗口中，填写对端网关名称和 IDC 端 VPN 网关的公网 IP，并单击【创建】。
![](https://main.qcloudimg.com/raw/1ee24b6ea02197ee926a2c68cc6b07ad.png)

<span id="step4" />

### 步骤四：创建 VPN 通道
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 在左侧导航栏选择【VPN 连接】>【VPN 通道】。
3. 在 “VPN 通道”页面上方选择【地域】，并单击【+新建】，进入“新建 VPN 通道”页面。
4. 输入通道名称，选择 VPN 网关类型为【云联网】，选择对端网关，并输入预共享密钥（如`123456`），单击【下一步】。
![](https://main.qcloudimg.com/raw/aaa4108a5c7256e787f2c6f464f2c9ce.png)
5. 输入 SPD 策略来限制本端哪些网段和对端哪些网段通信，单击【下一步】。
>!
>- 每个规则中的多个对端网段间相互不能重叠。
>- 同一网关下多个通道内的规则不能重叠。
>- SPD策略中的对端网段可以加入云联网中。
![](https://main.qcloudimg.com/raw/3e93deb482a775a805bf7610a4cb2e1b.png)
6. （可选）配置 IKE 参数，如果不需要高级配置，可直接单击【下一步】。
![](https://main.qcloudimg.com/raw/ba29246e26e44f88966fb22d4392f6e0.png)
7. （可选）配置 IPsec 参数，如果不需要配置，可直接单击【完成】。
![](https://main.qcloudimg.com/raw/a4644041c93d9a4a5365276161ba8e23.png)
8. 创建成功后，返回 VPN 通道列表页，在操作栏下单击【更多】>【下载配置文件】并完成下载。
![](https://main.qcloudimg.com/raw/eb9d4dbd1b4b58c4faa20dcff36bb206.png)

<span id="step5" />

### 步骤五：启用 IDC 网段
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 在左侧导航栏中选择【VPN连接】>【VPN网关】。
3. 在 VPN 网关列表中，单击云联网型 VPN 网关 ID。
4. 在 VPN 网关详情页面，选择【IDC 网段】页签，并启用目标网段。
![](https://main.qcloudimg.com/raw/02b7c6412ac7de7ab50b203768e8ec0d.png)

## 结果验证
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 在左侧导航栏中选择【云联网】。
3. 在云联网列表页中，单击 CCN 型 VPN 网关关联的云联网实例 ID。
4. 在云联网详情页面，选择【路由表】页签，若启用的网段在路由表中，且“状态”为有效，“下一跳”为 CCN 型 VPN 网关，则说明关联成功。
![](https://main.qcloudimg.com/raw/1f7089ad46654f9a3c2a9242c34302a4.png)
