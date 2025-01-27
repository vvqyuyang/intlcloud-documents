## 功能介绍

QUIC (Quick UDP Internet Connections) 是一个通用的网络协议，能够保障网络安全性，同时减少传输和连接时的延时，避免网络拥塞。

腾讯云 CDN 已开启 QUIC 内测，您可以 [提交申请表](https://intl.cloud.tencent.com/apply/p/g0lwu71z0i7) 申请试用。如果您已经提交申请，我们将在15个工作日对您的申请进行审核。



## 内测指南

若您通过了内测审核，则可以在控制台上为测试域名开启 QUIC 平台，进行测试。
>!QUIC 平台现为测试平台，尚未全量，建议您仅对新的测试域名开启 QUIC 平台，不要使用业务域名。

登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，新添域名时，您可通过选中 QUIC 平台项，为域名接入 QUIC 平台：
![](https://main.qcloudimg.com/raw/2098308cd8a8c1a0321c0164646b7700.png)
**配置约束：**

- 流媒体点播加速业务类型的域名暂不支持 QUIC。
- 开启IPv6访问后不可开启 QUIC。


成功添加域名后，可进入域名管理，切换 Tab 至【HTTPS 配置】，即可找到【QUIC】配置：
默认为关闭状态，您可自助开启，开启前请先配置 HTTPS 证书：
![](https://main.qcloudimg.com/raw/e697e32b39948d56610285c80043f1de.png)



>!业务类型切换涉及资源平台调度，接入 QUIC 平台后，建议您不要再切换域名的业务类型。



