## 简介
专用宿主机（CVM Dedicated Host，CDH）提供用户独享的物理服务器资源，满足用户资源独享、资源物理隔离、安全、合规需求，是云服务器产品的补充。专用宿主机搭载了腾讯云虚拟化系统，购买之后，您可在其上灵活创建、管理多个自定义规格的云服务器实例，自主规划物理资源的使用。

## 相关概念

了解腾讯云 CDH 时，通常会涉及到以下概念：
- [**宿主机类型**]()：宿主机的类型，不同类型的宿主机硬件配置不同。
- **本地硬盘类型**：宿主机上的磁盘类型，不同类型的宿主机搭载的磁盘类型不同，有本地硬盘以及本地 SSD 硬盘两种类型。
- **云服务器实例**：在宿主机上分配的云服务器实例，有些文档里也称为子机。
- [**云硬盘**](<https://intl.cloud.tencent.com/zh/document/product/213/4953>)：腾讯云提供的分布式持久块存储设备，可以用作实例的系统盘或可扩展数据盘使用。
- [**镜像**](<https://intl.cloud.tencent.com/zh/document/product/213/4940>)：实例预置模版，包含服务器的预配置环境（操作系统和其他已安装的软件）。
- [**私有网络**](https://intl.cloud.tencent.com/document/product/215/535)：自定义的虚拟网络空间，与其他资源逻辑隔离。
- **IP 地址**：云服务器实例对内和对外的服务地址，也即 [内网 IP 地址](<https://intl.cloud.tencent.com/zh/document/product/213/5225>) 和 [公网 IP 地址](<https://intl.cloud.tencent.com/zh/document/product/213/5224>)。
- [**SSH密钥**](<https://intl.cloud.tencent.com/zh/document/product/213/6092>)：一种比常规密码更安全的登录 Linux 云服务器的方式。
- [**安全组**](<https://intl.cloud.tencent.com/zh/document/product/213/5221>)：对实例进行安全的访问控制，指定进出实例的 IP、协议及端口规则。
- [**地域和可用区**](<https://intl.cloud.tencent.com/zh/document/product/213/6091>)：资源的启动位置。


## 相关服务

- 专用宿主机通过在其上分配云服务器实例使用，云服务器的使用请参考 [云服务器操作指南](https://intl.cloud.tencent.com/zh/document/product/213/16918) 。
- 您可以使用负载均衡横跨多个云服务器实例自动分配来自客户端的请求流量。更多信息，请参考 [负载均衡产品文档](https://intl.cloud.tencent.com/doc/product/214)。
- 您可以在云上部署关系数据库，也可以使用腾讯云云数据库。更多信息，请参考 [云数据库MySQL](https://intl.cloud.tencent.com/doc/product/236)。
- 您可以编写代码调用腾讯云 API 访问腾讯云的产品和服务，更多信息，请参考 [腾讯云 API 文档](https://intl.cloud.tencent.com/zh/document/api)。

## 使用专用宿主机

腾讯云 CDH 提供基于 Web 的用户界面，即控制台，如果您已注册腾讯云账户，您可以直接登录 [ CDH 控制台](https://console.cloud.tencent.com/cvm/cdh)，对您的 CVM 进行操作。
腾讯云 CDH 也提供了 API 接口方便您管理专用宿主机 CDH，有关 CDH API 操作的更多信息，请参阅 [API 文档](https://intl.cloud.tencent.com/document/product/213/33280)。
您可以使用 SDK（支持 PHP/Python/Java/.NET/Node.js）编程或使用腾讯云命令行工具调用 CVM API，具体请参考：

- [使用命令行工具 >>](https://intl.cloud.tencent.com/document/product/1013/33463)

## CDH 定价
CDH 价格信息，请参考 [CDH 产品定价](https://buy.cloud.tencent.com/price/cdh) 。





