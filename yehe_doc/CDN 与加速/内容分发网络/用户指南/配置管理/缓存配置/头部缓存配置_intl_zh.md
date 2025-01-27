

## 配置场景
除资源内容外，腾讯云 CDN 默认会缓存以下来自于源站的头部，并返回给用户：
+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges

若您的源站存在特殊头部，需要 CDN 进行缓存并返回给用户，可通过开启头部缓存配置实现。

## 配置指南
### 查看配置
登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，在菜单栏里选择【域名管理】，单击域名右侧【管理】，即可进入域名配置页面，第三栏【缓存配置】中可看到 HTTP 头部缓存配置，默认情况下为开启状态，您可按需自主关闭配置。
![](https://main.qcloudimg.com/raw/0fb4739f743b6242c463672a2f059098.png)

> !头部缓存配置正在全网升级中，若您单击关闭时提示错误，可能由于升级导致，可 [联系我们](https://intl.cloud.tencent.com/zh/support) 进行后台配置项关闭。





