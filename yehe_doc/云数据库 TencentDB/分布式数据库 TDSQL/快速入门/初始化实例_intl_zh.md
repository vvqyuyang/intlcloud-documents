本文为您介绍通过 TDSQL MySQL版 控制台初始化实例的操作。

## 操作步骤
1. 登录 [TDSQL MySQL版 控制台](https://console.cloud.tencent.com/dcdb)，在实例列表选择未初始化的实例，在“操作”列选择【更多】>【初始化】。

2. 在弹出的初始化对话框，根据需要选择配置后，单击【确定】。
 - 支持字符集：选择 MySQL 数据库支持的字符集。
 - 表名大小写敏感：数据库表名大小写是否敏感。
 -  开启强同步：开启强同步可以保证在主机故障时备机数据的一致性，至少需要2个节点方可正常运行。
![](https://main.qcloudimg.com/raw/2deee0a9b8a0bbc564b3ef1a290f060c.png)
3. 返回实例列表，待实例状态变为“运行中”，即可进行连接数据库操作。

