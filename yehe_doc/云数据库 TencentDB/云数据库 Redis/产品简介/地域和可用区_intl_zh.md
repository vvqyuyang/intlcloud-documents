
云数据库 Redis 提供多地域的支持，云服务器 CVM 支持的地域，云数据库 Redis 均会支持。

## 网络说明
- 同地域下（保障同一账号，且同一个 VPC 内）的云资源之间可通过内网互通，可以直接使用 [内网 IP](https://intl.cloud.tencent.com/document/product/213/5225) 访问。
- 处于同一地域不同可用区的云服务器 （网络为私有网络）访问 Redis（网络为基础网络），需手动配置子网及分配私有网络 IP 后才能互通。
- 处于不同私有网络的云产品，可以通过 [云联网](https://intl.cloud.tencent.com/zh/document/product/1003) 进行通信，此通信方式更较为高速、稳定。
>?云数据库 Redis，建议选择与云服务器相同的地域，可降低访问延迟。

## 地域和可用区
### 中国
<table class="table-striped">
<tbody><tr><th>地域</th><th>可用区</th><th>ZoneId</th></tr>
<tr>
<td rowspan="5">华南地区（广州）<br> ap-guangzhou</td>
<td>广州一区<br> ap-guangzhou-1</td><td>100001</td></tr>	
<tr>
<td>广州二区<br> ap-guangzhou-2</td><td>100002</td></tr>
<tr>
<td>广州三区<br> ap-guangzhou-3</td><td>100003</td></tr>
<tr>
<td>广州四区<br> ap-guangzhou-4</td><td>100004</td></tr>
<tr>
<td>广州六区<br> ap-guangzhou-6</td><td>100006</td></tr>
<tr>
<td rowspan="7">华东地区（上海）<br>ap-shanghai</td>
<td>上海一区<br>ap-shanghai-1</td><td>200001</td></tr>
<tr>
<td>上海二区<br>ap-shanghai-2</td><td>200002</td></tr>
<tr>
<td>上海三区<br>ap-shanghai-3</td><td>200003</td></tr>
<tr>
<td>上海四区<br>ap-shanghai-4</td><td>200004</td></tr>
<tr>
<td>上海五区<br>ap-shanghai-5</td><td>200005</td></tr>
<tr>
<td>上海六区<br>ap-shanghai-6</td><td>200006</td></tr>
<tr>
<td>上海七区<br>ap-shanghai-7</td><td>200007</td></tr>
<tr>
<td rowspan="2">华东地区（南京）<br>ap-nanjing</td>
<td>南京一区<br>ap-nanjing-1</td><td>330001</td></tr>
<tr>
<td>南京二区<br>ap-nanjing-2</td><td>330002</td></tr>
<tr>
<td rowspan="5">华北地区（北京）<br>ap-beijing</td>
<td>北京一区<br>ap-beijing-1</td><td>800001</td></tr>
<tr>
<td>北京二区<br>ap-beijing-2</td><td>800002</td></tr>
<tr>
<td>北京三区<br>ap-beijing-3</td><td>800003</td></tr>
<tr>
<td>北京四区<br>ap-beijing-4</td><td>800004</td></tr>
<tr>
<td>北京五区<br>ap-beijing-5</td><td>800005</td></tr>
<tr>
<td rowspan="2">华北地区（天津）<br>ap-tianjin</td>
<td>天津一区<br>ap-tianjin-1</td><td>360001</td></tr>
<tr>
<td>天津二区<br>ap-tianjin-2</td><td>360002</td></tr> 
<tr>
<td rowspan="2">西南地区（成都）<br>ap-chengdu</td>
<td>成都一区<br>ap-chengdu-1</td><td>160001</td></tr>
<tr>
<td>成都二区<br>ap-chengdu-2</td><td>160002</td></tr>    
<tr>
<td >西南地区（重庆）<br>ap-chongqing</td>
<td>重庆一区<br>ap-chongqing-1</td><td>190001</td></tr>
<tr>
<td rowspan="3">港澳台地区（中国香港）<br>ap-hongkong</td>
<td>香港一区（中国香港节点可用于覆盖港澳台地区）<br>ap-hongkong-1</td><td>300001</td></tr>
<tr>
<td>香港二区（中国香港节点可用于覆盖港澳台地区）<br>ap-hongkong-2</td><td>300002</td></tr>
<tr>
<td>香港三区（中国香港节点可用于覆盖港澳台地区）<br>ap-hongkong-3</td><td>300003</td></tr>
<tr>
<td>港澳台地区（中国台北）<br>ap-taipei</td>
<td>台北一区<br>ap-taipei-1</td><td>390001</td></tr>
</tbody></table>	

### 其他国家和地区
<table class="table-striped">
<tbody><tr><th>地域</th><th>可用区</th><th>ZoneId</th></tr>
<tr>
<td rowspan="2">亚太东南（新加坡）<br>ap-singapore</td>
<td>新加坡一区（新加坡节点可用于覆盖亚太东南地区）<br>ap-singapore-1</td><td>900001</td></tr>
<tr>
<td>新加坡二区（新加坡节点可用于覆盖亚太东南地区）<br>ap-singapore-2</td><td>900002</td></tr>
<tr>
<td>亚太东南（曼谷）<br>ap-bangkok </td>
<td>曼谷一区  （曼谷节点可用于覆盖亚太东南地区）<br>ap-bangkok-1</td><td>230001</td>
<tr>
<td rowspan="2">亚太南部（孟买）<br>ap-mumbai</td>
<td>孟买一区（孟买节点可用于覆盖亚太南部地区）<br>ap-mumbai-1</td><td>210001</td></tr>
<tr>
<td>孟买二区（孟买节点可用于覆盖亚太南部地区）<br>ap-mumbai-2</td><td>210002</td></tr>		
<tr>
<td rowspan="2">亚太东北（首尔）<br>ap-seoul</td>
<td>首尔一区（首尔节点可用于覆盖亚太东北地区）<br>ap-seoul-1</td><td>180001</td></tr>
<tr>
<td>首尔二区（首尔节点可用于覆盖亚太东北地区）<br>ap-seoul-2</td><td>180002</td></tr>
<tr>
<td >亚太东北（东京）<br>ap-tokyo</td>
<td>东京一区（东京节点可用于覆盖亚太东北地区）<br>ap-tokyo-1</td><td>250001</td></tr>
<tr>
<td rowspan="2">美国西部（硅谷）<br>na-siliconvalley</td>
<td>硅谷一区（硅谷节点可用于覆盖美国西部）<br>na-siliconvalley-1</td><td>150001</td></tr>
<tr>
<td>硅谷二区（硅谷节点可用于覆盖美国西部）<br>na-siliconvalley-2</td><td>150002</td></tr>
<tr>
<td rowspan="2">美国东部（弗吉尼亚）<br>na-ashburn</td>
<td>弗吉尼亚一区 （弗吉尼亚节点可用于覆盖美国东部地区）<br>na-ashburn-1</td><td>220001</td></tr>
<tr>
<td>弗吉尼亚二区 （弗吉尼亚节点可用于覆盖美国东部地区）<br>na-ashburn-2</td><td>220002</td></tr>
<tr>
<td>北美地区（多伦多）<br>na-toronto</td><td>多伦多一区（多伦多节点可用于覆盖北美地区）<br>na-toronto-1</td><td>400001</td></tr>
<tr>
<td>欧洲地区（法兰克福）<br>eu-frankfurt</td><td>法兰克福一区（法兰克福节点可用于覆盖欧洲地区）<br>eu-frankfurt-1</td><td>170001</td></tr>
<td >欧洲地区（莫斯科）<br>eu-moscow</td>
<td>莫斯科一区（莫斯科节点可用于覆盖欧洲地区）<br>eu-moscow-1</td><td>240001</td></tr>
</tbody></table>

