本文主要介绍消息队列 CKafka 的产品规格、计费项目、计费模式和实例价格。

## 产品规格


| 项目                                                                        | 标准版                                                       |
| -------------------- |  ------------------------------------------------------------ |
| 版本                 | <li>兼容开源0.9、0.10、1.1版本</li><li>默认安装1.1版本，不支持定制版本</li> |
| 实例类型             |  共享物理节点资源                                             |
| 稳定性 SLA           |  99.95%                                                       |
| 实例规格              | 分为入门型、标准型和进阶型等8种固定的实例类型                |
| <nobr>Topic/Partition 规格</nobr> | 每个型号固定上限                                             |
| 扩容                 |  自由度一般，可以单独扩容磁盘                                 |
| 性能调优             |  根据不同实例规格限制 Topic、partition 个数                   |
| 自动化清理磁盘       | 否，磁盘满后需要 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CKafka&level3_id=955&radio_title=%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=81&scene_code=18356&step=2) 处理 |
| broker 修复升级      |  受限于共享集群，升级解决问题周期较长                         |
| 高可用能力           | 不支持同城跨可用区部署，依赖于后台迁移，需要 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CKafka&level3_id=954&radio_title=%E4%BD%BF%E7%94%A8%E5%92%A8%E8%AF%A2(SDK/API/%E4%BA%A7%E5%93%81%E7%AD%89)&queue=81&scene_code=18346&step=2) 申请，一般处理周期为10个工作日 |
| 高级特性             |  无                                                           |
| 技术服务             |  基础的故障处理和问题修复                                     |

## 计费项目

计费项目如下：


| 项目      | 标准版 | 说明                                                         |
| --------- |  ------ | ------------------------------------------------------------ |
| <nobr>峰值带宽</nobr>  |  ✔️      | 40MB吞吐指出和入的带宽峰值为40MB。考虑实例的副本个数，需要均分吞吐量。例如，客户要求40MB吞吐、3副本，则需要购买120MB/s的峰值带宽。 |
| 磁盘容量  |  ✔️      | <li>不同实例规格对应不同的磁盘容量。</li><li> 消息队列CKafka支持的磁盘类型为 SSD。</li> |
| Topic     |         | <li>不同实例规格对应不同的 Topic 数量和支持的 Partition 数量上限。</li><li>标准版：单 Topic 支持的 Partition 数量限制为24个。</li> |
| Partition |        | <li>不同实例规格对应不同的 Partition 数量。 </li><li>不支持缩减 Partition 数量。</li><li>实例级别的 Paritition 限制包含了副本数。例如：一个实例下有1个双副本、4分区的 Topic、 2个3副本、3分区的 Topic，则该实例的总 Partition 个数为 （1 × 2 × 4）+（2 × 3 × 3）= 26个。</li> |

## 计费模式

消息队列 CKafka 以实例的形式售卖，采用**包年包月-预付费**的计费形式。

- 选购标准版实例时，仅需测算业务所需性能和磁盘容量，按需购买即可，最终购买的标准版实例的总费用 =  (实例单价 × 实例数量 + 磁盘容量单价 × 单独扩容磁盘容量 / 100) × 月数

> ?包年包月暂不支持提前进行缩容，您可以先 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E6%9C%8D%E5%8A%A1%20CKafKa&step=1) 申请缩容，等待到下一计费周期开始前，后台会为您执行缩容，执行后新的一个月/年会按照缩容后的规格计算。

## 标准版价格

消息队列 CKafka 标准版根据**峰值吞吐性能**及**磁盘容量**不同分为入门型和标准型等8种实例类型，支持单独扩容磁盘。

**实例价格**

| 实例类别 | 峰值吞吐量（MB/s） | 磁盘容量（GB） | 实例级别 Topic 数 | 实例级别 partition 数 | 价格（USD/月） |
| -------- | ------------------ | -------------- | ----------------- | --------------------- | ------------- |
| 入门型   | 40                 | 300            | 25                | 60                    | 870           |
| 标准型   | 100                | 1000           | 40                | 100                   | 1510          |
| 进阶型   | 150                | 2500           | 50                | 150                   | 1920          |
| 容量型   | 180                | 4000           | 150               | 300                   | 2330          |
| <nobr>高阶型 L1</nobr> | 300                | 6000           | 250               | 500                   | 2740          |
| 高阶型L2 | 400                | 6000           | 250               | 500                   | 3970          |
| 高阶型L3 | 600                | 6000           | 350               | 600                   | 5170          |
| 高阶型L4 | 900                | 9000           | 450               | 700                   | 7030          |

**单独扩容磁盘价格**

| 磁盘类型       | 磁盘容量（GB） | 价格（USD/月） |
| -------------- | -------------- | ------------- |
| SSD 高性能云盘 | 100            | 8           |

>?如需更高规格的消息队列 CKafka 实例，请联系商务经理或 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E6%9C%8D%E5%8A%A1%20CKafKa&step=1) 进行开通。	

