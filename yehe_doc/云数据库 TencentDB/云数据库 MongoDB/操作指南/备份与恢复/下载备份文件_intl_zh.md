本文为您介绍通过控制台和云服务器下载 MongoDB 备份文件的操作。

## 步骤1：生成备份文件
1. 登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，在实例列表，单击实例名，进入实例管理页面。
2. 在实例管理页面，选择【备份与回档】>【备份任务列表】页，选择需要下载的备份文件，单击“操作”列的【下载】。
>?您也可以通过右上角的【手动备份】生成当前时刻的备份文件。
>
![](https://main.qcloudimg.com/raw/2995c172841a888402275133d31f9d2f.png)
3. 在弹出的对话框，单击【确定】，启动文件下载任务。

## 步骤2：下载备份文件
1. 登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)，在实例列表，单击实例名，进入实例管理页面。
2. 在实例管理页面，选择【备份与回档】>【下载文件列表】页，查看任务生成进度。
![](https://main.qcloudimg.com/raw/02d08a9ca234f07c43be2c59f08e187d.png)
3. 文件生成完成后，推荐您复制下载地址，并 [登录到云数据库所在 VPC 下的 CVM（Linux 系统） ](https://intl.cloud.tencent.com/zh/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)中，运用 wget 命令进行内网高速下载，更高效。
>?
>- 您也可以单击【外网下载】，直接通过浏览器下载备份到本地。
>- wget 命令格式：`wget -c '内网地址' -O backup.tar`
>

