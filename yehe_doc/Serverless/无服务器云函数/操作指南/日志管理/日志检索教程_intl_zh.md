## 操作场景
云函数 SCF 于2021年01月29日起进行日志服务升级，接入腾讯云日志服务 CLS。详情可参见 [云函数日志服务变更说明](https://intl.cloud.tencent.com/document/product/583/39328)。

云函数 SCF 向2021年01月29日及以后的新增函数提供日志高级检索功能。在 [云函数控制台](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) 内嵌日志服务 CLS 检索分析页面，支持关键词搜索，您可以使用查询语法组合关键词进行检索。


>?若您的函数于2021年01月29日前创建，且需进行日志检索，则请参见 [日志检索教程（旧）](https://intl.cloud.tencent.com/document/product/583/34382)。





## 操作步骤
参考以下步骤对函数使用日志高级检索功能：
1. 登录 [云函数控制台](https://console.cloud.tencent.com/scf/index?rid=1)，选择左侧导航栏中的【函数服务】。
2. 在“函数服务”列表页面，选择需检索日志的函数名，进入“函数管理”页面。
3. 在“函数管理”页中，选择【日志查询】>【高级检索】。
4. 在“高级检索”页中，您可使用关键词进行搜索，或使用查询语法组合关键词进行检索。**语法规则详情可参见 [日志检索语法与规则](https://intl.cloud.tencent.com/document/product/614/30439)。**
5. 配置检索内容后，单击右侧的【检索分析】。查询完成后结果如下图所示：
![](https://main.qcloudimg.com/raw/f0f51eecc4e0e034875a5834cb2c4862.png)



