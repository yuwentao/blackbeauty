# 为什么叫blackbeauty?
《黑骏马》的作者安纳塞维尔由于腿脚不便一生与马为伴。在生命的最后几年，她笔触细腻真实地从马的视角讲述了Darkie的故事。Darkie诚实可靠、温和谦逊、友善勇敢，历经磨难却也不失本心。这本是一匹马的自述，却也是社会人性的缩影。


# 数据库和分布式系统以及分布式数据库技术汇总
## 2017年数据库技术盘点 http://blog.csdn.net/Tencent_TEG/article/details/79324165
### 自治数据库云：Oracle Database 18c
自治数据库云具备这些特点：
自主驱动：完全自动化的打补丁、升级、备份和可用性架构，可执行所有日常数据库维护任务，无需任何人工干预。
消除人为错误：自动恢复功能可自动检测并应用纠正措施，Oracle 自治数据库云将自动实施 Oracle Real Application Clusters (RAC) 和跨区域 Oracle Active Data Guard，确保持续的可用性。
Oracle SLA确保99.995%的可靠性和可用性，把代价高昂的计划内和计划外停机控制在每年30分钟内。
无需手动性能调优：采用自适应机器学习技术，自动激活列式缓存、存储索引、压缩和资源优先排序，根据负载所执行的实际工作分配资源，避免代价高昂的过度供应。

Hybrid Transactional/Analytical Processing (HTAP)：
Hybrid Transactional/Analytical Processing (HTAP)是gartner提出的一个新名词，代表一种既能处理在线事务，又能处理分析型请求的混合数据库。
## DB-Engines 排名的数据库引擎  https://db-engines.com/en/ranking
## 理论算法
### Quorum（NWR）模型
http://www.iteye.com/news/32340
https://www.cnblogs.com/jzhlin/archive/2012/07/23/Quorum.html
### redo日志/undo日志
http://www.cnblogs.com/chenpingzhao/p/5003881.html
#### 页断裂(partial write)与doublewrite技术
https://www.cnblogs.com/cchust/p/3961260.html
http://blog.itpub.net/22664653/viewspace-1140915/
#### gossip协议

## 开源实现
### 全局事务服务 GTS（阿里）
全局事务服务（Global Transaction Service，简称 GTS）是一款高性能、高可靠、接入简单的分布式事务中间件，用于解决分布式环境下的事务一致性问题。 在单机数据库下很容易维持事务的 ACID（Atomicity、Consistency、Isolation、Durability）特性，但在分布式系统中并不容易，GTS 可以保证分布式系统中的分布式事务的 ACID 特性。 GTS 支持 DRDS、RDS、MySQL 等多种数据源，可以配合 EDAS 和 Dubbo 等微服务框架使用， 兼容 MQ 实现事务消息。通过各种组合，可以轻松实现分布式数据库事务、多库事务、消息事务、服务链路级事务等多种业务需求。
https://help.aliyun.com/document_detail/48726.html?spm=a2c4g.11174283.3.1.gs0tKh
### peloton数据库
https://yq.aliyun.com/articles/214367
### Aurora
Aurora是一个云上环境全新的数据库服务可以很好的解决上述传统数据库遇到的问题。 它基于存储计算分离的架构，并将回放日志部分下推到分布式存储层，存储节点与数据库实例(计算节点)松耦合，并包含部分计算功能。 Aurora体系下的数据库实例仍然包含了大部分核心功能，比如查询处理，事务，锁，缓存管理，访问接口和undo日志管理等；Aurora相对于传统数据库有三大优势，首先，底层数据库存储是一个分布式存储服务，可以轻松应对故障；其次，数据库实例往底层存储层只写redo日志，因此数据库实例与存储节点之间的网络压力大大减小，这为提升数据库性能提供了保障；第三，将部分核心功能(故障恢复，备份还原)下推到存储层，这些任务可以在后台不间歇地异步执行，并且不影响前台用户任务。
https://www.allthingsdistributed.com/files/p1041-verbitski.pdf
http://www.cnblogs.com/cchust/p/7476876.html
https://cloud.tencent.com/developer/article/1005636
## 数据库中间件
### UCloud分布式数据库UDDB

### share nothing和share disk架构
比较典型的share disk数据库有oracle RAC和DB2 PureScale
Share-nothing架构如GreenPlum，DB2,SQL Server及分布式的hadoop使用的是Shared Noting架构，Google Spanner、OceanBase、TIDB
1. Shared Disk 架构
所有的节点共享一份数据，优点是只要有一个节点可用，就可以访问所有数据；缺点是内存融合（cache fusion）大大限制了它的水平扩展能力。简单地说：可用性高，但可扩展性弱，常见于24*7的高可用性核心业务。
2. Shared Nothing 架构
数据和节点具有对应关系，缺点是如果要访问所有数据，必须所有节点都可用；优点是每个节点交互少，很容易扩展。简单地说：可扩展性强，可用性低。多用于VLDB
https://wenku.baidu.com/view/7d99b37f5acfa1c7aa00ccdd.html
https://en.wikipedia.org/wiki/Shared-nothing_architecture
http://blog.itpub.net/26277071/viewspace-710924/
