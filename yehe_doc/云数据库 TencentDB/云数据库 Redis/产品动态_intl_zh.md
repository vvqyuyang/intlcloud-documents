## 2020年12月
<table>
<tr><th width=20%>动态名称</th><th width=50%>动态描述</th><th width=10%>发布时间</th><th width=20%>相关文档</th></tr>
<tr>
<td>Redis 混合存储版更名为云数据库 Tendis</td>
<td>Redis 混合存储版本正式更名为云数据库 Tendis，启用独立产品入口，独立控制台。</td>
<td>2020-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1083/39286" target="_blank">云数据库 Tendis</a></td>
</tr>
<tr>
<td>支持多可用区部署</td>
<td>云数据库 Redis 支持同地域下跨多个可用区部署副本，相对单可用区实例（主节点和副本节点在同一可用区），多可用区实例具有更高的可用性和容灾能力。</td>
<td>2020-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/39812" target="_blank">多可用区</a></td>
</tr>
</table>

## 2020年09月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>支持5秒监控粒度</td>
<td>Redis 监控粒度从1分钟升级到5秒，新版本中对 Redis 的监控进行了全面的升级。</td>
<td>2020-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/38743" target="_blank">监控功能（5秒粒度）</a></td>
</tr>
</table>

## 2020年07月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>支持版本升级</td>
<td>Redis 新增版本升级功能，支持标准版低版本升级到高版本，包括2.8升级至4.0、2.8升级至5.0、4.0升级至5.0。</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/37710" target="_blank">升级实例版本</a></td>
</tr>
<tr>
<td>支持架构升级</td>
<td>Redis 新增架构升级功能，一键完成标准架构到集群架构升级，帮助业务快速扩展性能和容量。</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/37860" target="_blank">升级实例架构</a></td>
</tr>
</table>

## 2020年06月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>Redis 混合存储版上线</td>
<td>云数据库 Redis 混合存储版正式发布，100%兼容 Redis 协议，最大可降低内存成本80%，与内存版一致的热数据性能，兼容性、性能、成本可完美平衡。</td>
<td>2020-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1083/39296" target="_blank">混合存储版（集群架构）</a></td>
</tr>
</table>

## 2020年04月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>DTS 支持 Redis 5.0</td>
<td>支持通过数据传输服务 DTS 迁移数据和升级版本至 Redis 5.0。</td>
<td>2020-04</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/239/31941" target="_blank">使用 DTS 进行迁移</a><li><a href="https://intl.cloud.tencent.com/document/product/239/32546" target="_blank">使用 DTS 进行版本升级</a></td>
</tr>
</table>

## 2020年03月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>支持服务不可用事件告警</td>
<td>Redis 支持服务不可用事件告警支持功能，支持实例主备切换、服务不可用、只读副本故障切换、只读副本不可用4个类型的事件告警通知。</td>
<td>2020-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31947" target="_blank">配置告警</a></td>
</tr>
<tr>
<td>支持自助调整带宽</td>
<td>Redis 控制台实例详情页支持自助调整实例网络带宽，集群版带宽规格全面升级，所有分片规格带宽升级至384Mbps。</td>
<td>2020-03</td>
<td>-</td>
</tr>
<tr>
<td>2.8版本监控视图切换</td>
<td>为提供更准确的监控信息，我们将2.8版本实例的监控信息更新为了 cluster 视图，如果您是使用 API 从云监控获取监控数据，您需要将代码中的视图由 redisuuid 切换为 cluster。</td>
<td>2020-03</td>
<td>-</td>
</tr>
</table>


## 2020年02月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>新购实例默认256个 DB（Data Base）</td>
<td>Redis 2.8、4.0、5.0 标准版、集群版，新购实例默认 DB 数量由原来16个升级为256个。</td>
<td>2020-02</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/239/31959" target="_blank">内存版（标准架构）</a><li><a href="https://intl.cloud.tencent.com/document/product/239/18336" target="_blank">内存版（集群架构）</a></td>
</tr>
</table>

## 2020年01月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>Redis 5.0 上线</td>
<td>Redis 发布5.0标准版、集群版，支持最新的 STREAM 数据结构，ZSET 提供新的命令 ZPOPMIN、ZPOPMAX，延续4.0版本的所有特性，扩容不断连接、4TB超大规格、千万QPS并发能力。</td>
<td>2020-01</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/239/31959" target="_blank">内存版（标准架构）</a><li><a href="https://intl.cloud.tencent.com/document/product/239/18336" target="_blank">内存版（集群架构）</a></td>
</tr>
</table>

## 2019年10月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>支持访问管理</td>
<td>支持通过访问管理来创建策略，允许子帐号使用他们所需要的资源或权限。</td>
<td>2019-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/32845" target="_blank">访问管理</a></td>
</tr>
<tr>
<td>支持控制台管理账号</td>
<td>通过账号机制提供读写权限控制和路由策略控制，以满足复杂业务场景中对业务权限的控制。目前仅云数据库 Redis 社区版（不含2.8版）支持账号设置。</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/34590" target="_blank">管理账号</a></td>
</tr>
</table>

## 2019年09月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>监控2.0版本发布</td>
<td>Redis 发布监控2.0版本，新增监控指标16+，覆盖网络延迟、响应错误等监控指标。</td>
<td>2019-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/34589" target="_blank">监控功能</a></td>
</tr>
</table>

## 2019年08月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>支持免密码访问</td>
<td>免密码访问功能需 <a href="https://console.cloud.tencent.com/workorder/category">提交工单</a> 开通，免密码访问开通后，建议通过安全组限制主机访问数量。</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/32548" target="_blank">免密码访问</a></td>
</tr>
<tr>
<td>支持高危命令在线禁用</td>
<td>Redis 部分命令的使用可能会导致服务不稳定、或者数据误删除，因此云数据库 Redis 提供了禁用部分命令的功能。支持禁用的命令包括 flushall、flushdb、keys、hgetall、eval、evalsha、script。</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/32550" target="_blank">禁用命令</a></td>
</tr>

<tr>
<td>DTS 支持集群版</td>
<td>DTS 支持自建 Redis Cluster、Codis 一键迁移上云，支持 3.0、3.2、4.0 Cluster 版本迁移，支持 2.8、3.2 Codis 版本迁移。</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941" target="_blank">使用 DTS 进行迁移</a></td>
</tr>
</table>


## 2019年07月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>支持通过 DTS 升级版本</td>
<td>云数据库 Redis 实例版本升级，通过数据传输服务 DTS 以热迁移的方式进行，保证升级过程中 Redis 实例业务不停服，能实时增量更新数据。</td>
<td>2019-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/32546" target="_blank">使用 DTS 进行版本升级</a></td>
</tr>
<tr>
<td>Redis 4.0 标准版上线</td>
<td>Redis 4.0 标准版支持1主5从，支持读写分离，扩缩容不断连接，提供超高可用性。</td>
<td>2019-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31959" target="_blank">内存版（标准架构）</a></td>
</tr>
</table>


## 2018年10月
<table>
<tr>
<th width=20%>动态名称</th>
<th width=50%>动态描述</th>
<th width=10%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
<tr>
<td>Redis 4.0 集群版上线</td>
<td>Redis 4.0 集群版全新上线，支持4TB超大容量、千万并发访问，无损扩展和自动读写分离。</td>
<td>2018-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/18336" target="_blank">内存版（集群架构）</a></td>
</tr>
</table>

