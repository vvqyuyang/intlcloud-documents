应用创建成功后，您可通过【功能配置】为您当前的应用开启 [旁路推流](#bypass)、[云端录制](#record) 和 [高级权限控制](#purview) 功能，该页面所有功能配置修改成功后大约5分钟生效。

<span id="bypass"></span>
## 旁路推流配置

### 注意事项

- 基于 UDP 传输协议的 TRTC 服务，通过协议转换将音视频流对接到 [云直播](https://intl.cloud.tencent.com/document/product/267) 系统，这个过程称之为“旁路推流”。
- 旁路推流功能默认关闭，开启旁路推流功能需先开通云直播服务。
- 将旁路推流用于 [CDN 直播观看](https://intl.cloud.tencent.com/document/product/647/35242) 时，云直播将会按直播观看产生的下行流量/带宽收取相关费用，详见 [云直播>流量带宽计费](https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#bill-by-traffic.2Fbandwidth) 说明。
- 将旁路推流用于 [云端录制](https://intl.cloud.tencent.com/document/product/647/35426) 时，将会产生录制、录制文件存储等费用，详见 [云端录制与回放>相关费用](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8) 说明。
- 若您在 [云直播控制台](https://console.cloud.tencent.com/live/domainmanage) 给旁路推流使用的推流域名（`xxxx.livepush.myqcloud.com`）绑定了录制、转码、截图鉴黄、水印等收费功能的模板，则旁路推流时会产生模板对应的 [增值费用](https://intl.cloud.tencent.com/document/product/267/2819) 。

<span id="open_bypass"></span>
### 开启旁路推流功能
1. 进入实时音视频控制台，选择【[应用管理](https://console.cloud.tencent.com/trtc/app)】。
2. 选择需要修改功能配置的应用，单击目标应用所在行的【功能配置】。
3. 在【旁路推流配置】中，单击【启用旁路推流】右侧的按钮。
4. 在弹出的【开启旁路推流功能】弹框中，**仔细阅读风险说明**；若确认开通，单击【开启旁路推流功能】即可。

<span id="select"></span>
### 选择旁路推流方式
[旁路推流功能开启](#open_bypass) 后，您可以根据实际业务情况选择旁路的推流方式：

- **指定流旁路**：选择“指定流旁路”后：如果不需要混流转码，请调用客户端 SDK [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) 接口直接发起旁路推流；如果需要混流转码，请根据 [云端混流转码](https://intl.cloud.tencent.com/document/product/647/34618) 文档指引操作，混流转码后会自动旁路推流。
- **全局自动旁路**：选择“全局自动旁路”后，TRTC 所有上行音视频流都会被自动旁路推流到云直播系统。


<span id="close__bypass"></span>
### 关闭旁路推流功能
如果您需要关闭旁路推流功能，具体操作步骤如下：
1. 单击【[应用管理](https://console.cloud.tencent.com/trtc/app)】，选择需要修改功能配置的应用，单击目标应用所在行的【功能配置】。
2. 在【旁路推流配置】中，单击【启用旁路推流】右侧的按钮。
3. 在弹出的【关闭旁路推流功能】弹框中，**仔细阅读风险说明**；若确认关闭，单击【关闭旁路推流功能】即可。


<span id="record"></span>
## 云端录制配置

### 注意事项
- 实时音视频服务通过旁路推流使用 [云直播](https://intl.cloud.tencent.com/document/product/267) 的能力为您提供全程的云端录制功能，并将录制下来的文件存储到 [云点播](https://intl.cloud.tencent.com/document/product/266) 平台。
- 录制功能使用的是云直播服务的能力，将产生云直播的直播录制费用，以当月直播录制并发峰值路数为结算标准，详细计费规则请参见 [云直播 > 直播录制价格说明](https://intl.cloud.tencent.com/document/product/267/39605) 。
- 录制后的文件存储在云点播平台，将产生云点播的存储费用，按录制文件存储在云点播平台的存储容量计费，详细计费规则请参见 [云点播 > 视频存储（日结）价格说明](https://intl.cloud.tencent.com/document/product/266/14666) 。
- 如需播放或下载录制的视频文件，将会产生云点播服务的流量（视频加速）费用，按下行加速流量计费，详细计费规则请参见 [云点播 > 视频加速（日结）价格说明](https://intl.cloud.tencent.com/document/product/266/14666) 。
- 云端录制功能默认关闭，启用云端录制功能需要先开通云直播和云点播服务。
- 云端录制依赖旁路推流，请先启用 [旁路推流](#open_bypass)。


<span id="open_record"></span>
### 启用云端录制功能
TRTC 的云端录制，可以将房间中的每一个用户的音视频流都录制成一个独立的文件，若您需开启云端录制功能，详细操作指引请参见 [实现云端录制与回放](https://intl.cloud.tencent.com/document/product/647/35426#open)。

<span id="change_record"></span>
### 修改云端录制配置
>! 修改云端录制配置可能会影响您线上正在运行的业务数据，请确认风险后谨慎操作。

1. 单击【[应用管理](https://console.cloud.tencent.com/trtc/app)】，选择需要修改云端录制配置的应用，单击目标应用所在行的【功能配置】。
2. 在【功能配置】>【云端录制配置】中，单击右侧的【编辑】进入云端录制配置修改页。
4. 根据实际情况修改 [配置信息](https://intl.cloud.tencent.com/document/product/647/35426#recordType)，单击【确定】即可保存修改。


<span id="close_record"></span>
### 关闭云端录制功能
关闭云端录制后将导致您线上正在运行的业务无法进行云端录制，包括手动录制和自动录制。请确认您的业务确实不再需要云端录制功能时再关闭。

1. 单击【[应用管理](https://console.cloud.tencent.com/trtc/app)】，选择需要修改功能配置的应用，单击目标应用所在行的【功能配置】。
2. 在【功能配置】>【云端录制配置】中，单击【启用云端录制】右侧的按钮。
3. 仔细阅读关闭后的影响，若确认关闭云端录制，单击【关闭云端录制】即可。



<span id="purview"></span>
## 高级权限控制
如果您希望给某些房间中加入进房限制或者上麦限制，也就是仅允许指定的用户去进房或者上麦，而您又担心在客户端判断权限很容易遭遇破解攻击，那么可以考虑 [开启高级权限控制](https://intl.cloud.tencent.com/document/product/647/35157)。


### 注意事项
开启高级权限控制后，当前 SDKAppID 的所有用户都需要在 TRTCParams 中正确传入 privateMapKey 参数才能成功进房。如果线上有使用此 SDKAppID 的用户，请不要轻易开启此功能。


### 启用高级权限控制
1. 单击【应用管理】，选择需要开启高级权限控制的应用，单击目标应用所在行的【功能配置】。
2. 在【功能配置】>【高级权限控制】中，单击右侧的【启用高级权限控制】右侧按钮。

### 关闭高级权限控制
1. 单击【应用管理】，选择需要关闭高级权限控制的应用，单击目标应用所在行的【功能配置】。
2. 在【功能配置】>【高级权限控制】中，单击右侧的【关闭高级权限控制】右侧按钮。

## 相关文档
- 若需创建新的应用，具体操作请参见 [创建应用](https://intl.cloud.tencent.com/document/product/647/39077)。
- 若需在应用列表中搜索相关应用，具体操作请参见 [搜索应用](https://intl.cloud.tencent.com/document/product/647/39078)。
- 若需查看应用的基本信息，具体操作请参见 [应用信息](https://intl.cloud.tencent.com/document/product/647/39079)。
- 若需在云端混流转码时设置自定义背景图片，可在素材管理中添加对应的图片素材，具体操作请参见 [素材管理](https://intl.cloud.tencent.com/document/product/647/39081)。
- 若需快速跑应用通配套的 Demo 源码，具体操作请参见 [快速上手](https://intl.cloud.tencent.com/document/product/647/39082)。





应用创建成功后，您可通过【功能配置】为您当前的应用开启 [旁路推流](#bypass)、[云端录制](#record) 和 [高级权限控制](#purview) 功能，该页面所有功能配置修改成功后大约5分钟生效。

<span id="bypass"></span>
## 旁路推流配置

### 注意事项

- 基于 UDP 传输协议的 TRTC 服务，通过协议转换将音视频流对接到 [云直播](https://intl.cloud.tencent.com/document/product/267) 系统，这个过程称之为“旁路推流”。
- 旁路推流功能默认关闭，开启旁路推流功能需先开通云直播服务。
- 将旁路推流用于 [CDN 直播观看](https://intl.cloud.tencent.com/document/product/647/35242) 时，云直播将会按直播观看产生的下行流量/带宽收取相关费用，详见 [云直播>流量带宽计费](https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#bill-by-traffic.2Fbandwidth) 说明。
- 将旁路推流用于 [云端录制](https://intl.cloud.tencent.com/document/product/647/35426) 时，将会产生录制、录制文件存储等费用，详见 [云端录制与回放>相关费用](https://intl.cloud.tencent.com/document/product/647/35426#.E7.9B.B8.E5.85.B3.E8.B4.B9.E7.94.A8) 说明。
- 若您在 [云直播控制台](https://console.cloud.tencent.com/live/domainmanage) 给旁路推流使用的推流域名（`xxxx.livepush.myqcloud.com`）绑定了录制、转码、截图鉴黄、水印等收费功能的模板，则旁路推流时会产生模板对应的 [增值费用](https://intl.cloud.tencent.com/document/product/267/2819) 。

<span id="open_bypass"></span>
### 开启旁路推流功能
1. 进入实时音视频控制台，选择【[应用管理](https://console.cloud.tencent.com/trtc/app)】。
2. 选择需要修改功能配置的应用，单击目标应用所在行的【功能配置】。
3. 在【旁路推流配置】中，单击【启用旁路推流】右侧的按钮。
4. 在弹出的【开启旁路推流功能】弹框中，**仔细阅读风险说明**；若确认开通，单击【开启旁路推流功能】即可。

<span id="select"></span>
### 选择旁路推流方式
[旁路推流功能开启](#open_bypass) 后，您可以根据实际业务情况选择旁路的推流方式：

- **指定流旁路**：选择“指定流旁路”后：如果不需要混流转码，请调用客户端 SDK [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) 接口直接发起旁路推流；如果需要混流转码，请根据 [云端混流转码](https://intl.cloud.tencent.com/document/product/647/34618) 文档指引操作，混流转码后会自动旁路推流。
- **全局自动旁路**：选择“全局自动旁路”后，TRTC 所有上行音视频流都会被自动旁路推流到云直播系统。


<span id="close__bypass"></span>
### 关闭旁路推流功能
如果您需要关闭旁路推流功能，具体操作步骤如下：
1. 单击【[应用管理](https://console.cloud.tencent.com/trtc/app)】，选择需要修改功能配置的应用，单击目标应用所在行的【功能配置】。
2. 在【旁路推流配置】中，单击【启用旁路推流】右侧的按钮。
3. 在弹出的【关闭旁路推流功能】弹框中，**仔细阅读风险说明**；若确认关闭，单击【关闭旁路推流功能】即可。


<span id="record"></span>
## 云端录制配置

### 注意事项
- 实时音视频服务通过旁路推流使用 [云直播](https://intl.cloud.tencent.com/document/product/267) 的能力为您提供全程的云端录制功能，并将录制下来的文件存储到 [云点播](https://intl.cloud.tencent.com/document/product/266) 平台。
- 录制功能使用的是云直播服务的能力，将产生云直播的直播录制费用，以当月直播录制并发峰值路数为结算标准，详细计费规则请参见 [云直播 > 直播录制价格说明](https://intl.cloud.tencent.com/document/product/267/39605) 。
- 录制后的文件存储在云点播平台，将产生云点播的存储费用，按录制文件存储在云点播平台的存储容量计费，详细计费规则请参见 [云点播 > 视频存储（日结）价格说明](https://intl.cloud.tencent.com/document/product/266/14666) 。
- 如需播放或下载录制的视频文件，将会产生云点播服务的流量（视频加速）费用，按下行加速流量计费，详细计费规则请参见 [云点播 > 视频加速（日结）价格说明](https://intl.cloud.tencent.com/document/product/266/14666)  。
- 云端录制功能默认关闭，启用云端录制功能需要先开通云直播和云点播服务。
- 云端录制依赖旁路推流，请先启用 [旁路推流](#open_bypass)。


<span id="open_record"></span>
### 启用云端录制功能
TRTC 的云端录制，可以将房间中的每一个用户的音视频流都录制成一个独立的文件，若您需开启云端录制功能，详细操作指引请参见 [实现云端录制与回放](https://intl.cloud.tencent.com/document/product/647/35426#open)。

<span id="change_record"></span>
### 修改云端录制配置
>! 修改云端录制配置可能会影响您线上正在运行的业务数据，请确认风险后谨慎操作。

1. 单击【[应用管理](https://console.cloud.tencent.com/trtc/app)】，选择需要修改云端录制配置的应用，单击目标应用所在行的【功能配置】。
2. 在【功能配置】>【云端录制配置】中，单击右侧的【编辑】进入云端录制配置修改页。
4. 根据实际情况修改 [配置信息](https://intl.cloud.tencent.com/document/product/647/35426#recordType)，单击【确定】即可保存修改。


<span id="close_record"></span>
### 关闭云端录制功能
关闭云端录制后将导致您线上正在运行的业务无法进行云端录制，包括手动录制和自动录制。请确认您的业务确实不再需要云端录制功能时再关闭。

1. 单击【[应用管理](https://console.cloud.tencent.com/trtc/app)】，选择需要修改功能配置的应用，单击目标应用所在行的【功能配置】。
2. 在【功能配置】>【云端录制配置】中，单击【启用云端录制】右侧的按钮。
3. 仔细阅读关闭后的影响，若确认关闭云端录制，单击【关闭云端录制】即可。



<span id="purview"></span>
## 高级权限控制
如果您希望给某些房间中加入进房限制或者上麦限制，也就是仅允许指定的用户去进房或者上麦，而您又担心在客户端判断权限很容易遭遇破解攻击，那么可以考虑 [开启高级权限控制](https://intl.cloud.tencent.com/document/product/647/35157)。


### 注意事项
开启高级权限控制后，当前 SDKAppID 的所有用户都需要在 TRTCParams 中正确传入 privateMapKey 参数才能成功进房。如果线上有使用此 SDKAppID 的用户，请不要轻易开启此功能。


### 启用高级权限控制
1. 单击【应用管理】，选择需要开启高级权限控制的应用，单击目标应用所在行的【功能配置】。
2. 在【功能配置】>【高级权限控制】中，单击右侧的【启用高级权限控制】右侧按钮。

### 关闭高级权限控制
1. 单击【应用管理】，选择需要关闭高级权限控制的应用，单击目标应用所在行的【功能配置】。
2. 在【功能配置】>【高级权限控制】中，单击右侧的【关闭高级权限控制】右侧按钮。

## 相关文档
- 若需创建新的应用，具体操作请参见 [创建应用](https://intl.cloud.tencent.com/document/product/647/39077)。
- 若需在应用列表中搜索相关应用，具体操作请参见 [搜索应用](https://intl.cloud.tencent.com/document/product/647/39078)。
- 若需查看应用的基本信息，具体操作请参见 [应用信息](https://intl.cloud.tencent.com/document/product/647/39079)。
- 若需在云端混流转码时设置自定义背景图片，可在素材管理中添加对应的图片素材，具体操作请参见 [素材管理](https://intl.cloud.tencent.com/document/product/647/39081)。
- 若需快速跑应用通配套的 Demo 源码，具体操作请参见 [快速上手](https://intl.cloud.tencent.com/document/product/647/39082)。




