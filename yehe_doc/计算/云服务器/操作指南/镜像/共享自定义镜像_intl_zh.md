## 操作场景

**共享镜像**是将自己已经创建好的 [**自定义镜像**](https://intl.cloud.tencent.com/document/product/213/4942) 共享给**其他用户**使用。用户可以方便地从其他用户那里获得共享镜像，并从中获得需要的组件及添加自定义内容。

> 腾讯云无法保证其他用户共享镜像的完整性或安全性，我们建议用户只使用来自可靠来源的共享镜像。

## 注意事项
 - 每个镜像最多可以共享给50个用户。
 - 共享镜像不能更改名称和描述，仅可用于创建云服务器实例。
 - 共享给其他用户的镜像不占用自身镜像配额。
 - 共享给其他用户的镜像可以删除，但需先取消该镜像所有的共享，取消共享操作详见 [取消共享自定义镜像](/doc/product/213/7148)。获取的共享镜像不可删除。
 - 镜像支持共享到对方账号相同地域内；若需共享到不同地域，需先复制镜像到不同地域再进行共享。
 - 不可将获取的已共享镜像共享给其他用户。

## 操作步骤

### 获取主账号的账号 ID

腾讯云共享镜像通过对端主账号唯一 ID 识别。您可以通知该用户通过以下方式获取主账号的账号 ID：
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/)。
2. 单击右上角的账号名称，选择【账号信息】。
3. 在“账号信息”管理页面，查看并记录主账号的账号 ID 。
4. 通知对方将获取到的账号 ID 发送给自己。

### 通过控制台共享

 1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/)。
 2. 在左侧导航栏中，单击【[镜像](https://console.cloud.tencent.com/cvm/image)】。
 3. 选择【自定义镜像】页签，进入自定义镜像管理页面。
 4. 在自定义镜像列表中，选中您要共享的自定义镜像，单击右侧【共享】。
 5. 在弹出的“共享镜像”窗口中，输入对方主账号的账号 ID，单击【共享】。
 6. 通知对方登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/)，并选择【镜像】>【共享镜像】，即可查看到共享的镜像。
 7. 如需共享给多个用户，请重复上述步骤。

### 通过 API 共享

您可以使用 ShareImage 接口共享镜像。
