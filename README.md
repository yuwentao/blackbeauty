

# 前言：为什么叫blackbeauty?
来源于小说《黑骏马》,《黑骏马》的作者安纳塞维尔由于腿脚不便一生与马为伴。在生命的最后几年，她笔触细腻真实地从马的视角讲述了Darkie的故事。Darkie诚实可靠、温和谦逊、友善勇敢，历经磨难却也不失本心。这本是一匹马的自述，却也是社会人性的缩影。
程序员很大程度上跟这批马类似，在其职业生涯以及整个人生过程中，个人唯有不断的提高自己的技能和专业知识，以及良好的合作精神才能有利用价值，只有不断进取拼搏才能不至于被淘汰。
程序员虽然也可以单打独斗，自由职业，但是很大程度上需要借助于他所发挥的平台。

# 一.数据库和分布式系统以及分布式数据库技术汇总
## 1.数据库技术总览
[2017年数据库技术盘点] : http://blog.csdn.net/Tencent_TEG/article/details/79324165
[cmsa]: https://github.com/ServiceComb/seckill/tree/master/seckill-command-service/README.md

### 1.1自治数据库
#### 1.1.1自治数据库云：Oracle Database 18c
自治数据库云具备这些特点：
自主驱动：完全自动化的打补丁、升级、备份和可用性架构，可执行所有日常数据库维护任务，无需任何人工干预。
消除人为错误：自动恢复功能可自动检测并应用纠正措施，Oracle 自治数据库云将自动实施 Oracle Real Application Clusters (RAC) 和跨区域 Oracle Active Data Guard，确保持续的可用性。
Oracle SLA确保99.995%的可靠性和可用性，把代价高昂的计划内和计划外停机控制在每年30分钟内。
无需手动性能调优：采用自适应机器学习技术，自动激活列式缓存、存储索引、压缩和资源优先排序，根据负载所执行的实际工作分配资源，避免代价高昂的过度供应。
#### 1.1.2混合事务型分析型数据库
Hybrid Transactional/Analytical Processing (HTAP)：
Hybrid Transactional/Analytical Processing (HTAP)是gartner提出的一个新名词，代表一种既能处理在线事务，又能处理分析型请求的混合数据库。
## 2.数据库排名和变化
[DB-Engines 排名的数据库引擎]  (https://db-engines.com/en/ranking) 
## 3.理论算法与模型
### 3.1 Quorum（NWR）模型
http://www.iteye.com/news/32340 
https://www.cnblogs.com/jzhlin/archive/2012/07/23/Quorum.html 
### 3.2 redo日志/undo日志
http://www.cnblogs.com/chenpingzhao/p/5003881.html 
#### 3.3页断裂(partial write)与doublewrite技术
https://www.cnblogs.com/cchust/p/3961260.html 
http://blog.itpub.net/22664653/viewspace-1140915/ 
#### 3.4 gossip协议
#### 3.5 Raft协议
#### 3.6 paxos协议
#### 3.7 并发控制算法SSCC 
https://github.com/domino-succ/domino
#### 3.8 二阶段提交
#### 3.9 Google 论文
##### 3.9.1 Google Spanner / F1
##### 3.9.2 分布式事务模型Percolator
Percolator 和 TiDB 事务算法 https://pingcap.com/blog-cn/percolator-and-txn/
## 4.知名系统与开源实现
### 4.1全局事务服务 GTS（阿里）
全局事务服务（Global Transaction Service，简称 GTS）是一款高性能、高可靠、接入简单的分布式事务中间件，用于解决分布式环境下的事务一致性问题。 在单机数据库下很容易维持事务的 ACID（Atomicity、Consistency、Isolation、Durability）特性，但在分布式系统中并不容易，GTS 可以保证分布式系统中的分布式事务的 ACID 特性。 GTS 支持 DRDS、RDS、MySQL 等多种数据源，可以配合 EDAS 和 Dubbo 等微服务框架使用， 兼容 MQ 实现事务消息。通过各种组合，可以轻松实现分布式数据库事务、多库事务、消息事务、服务链路级事务等多种业务需求。
https://help.aliyun.com/document_detail/48726.html?spm=a2c4g.11174283.3.1.gs0tKh 
### 4.2 peloton数据库 
https://yq.aliyun.com/articles/214367
阿里云新一代关系型数据库 PolarDB 剖析
 https://yq.aliyun.com/articles/172724?utm_content=m_28518
Taurus分布式数据库和AWS Aurora对比 https://zhuanlan.zhihu.com/p/29182627
### 4.3 计算与存储分离型 Aurora
Aurora通过计算节点和存储节点分离，计算节点scale up，存储节点scale out的理念将公有云的关系数据库产品推向了一个新的高度。
Aurora是一个云上环境全新的数据库服务可以很好的解决上述传统数据库遇到的问题。 它基于存储计算分离的架构，并将回放日志部分下推到分布式存储层，存储节点与数据库实例(计算节点)松耦合，并包含部分计算功能。 Aurora体系下的数据库实例仍然包含了大部分核心功能，比如查询处理，事务，锁，缓存管理，访问接口和undo日志管理等；Aurora相对于传统数据库有三大优势，首先，底层数据库存储是一个分布式存储服务，可以轻松应对故障；其次，数据库实例往底层存储层只写redo日志，因此数据库实例与存储节点之间的网络压力大大减小，这为提升数据库性能提供了保障；第三，将部分核心功能(故障恢复，备份还原)下推到存储层，这些任务可以在后台不间歇地异步执行，并且不影响前台用户任务。
https://www.allthingsdistributed.com/files/p1041-verbitski.pdf 
http://www.cnblogs.com/cchust/p/7476876.html 
https://cloud.tencent.com/developer/article/1005636 
## 4.4 常见分布式数据库中间件
### 4.4.1 UCloud分布式数据库UDDB

### 4.4.2 shardingjdbc中间件
http://shardingjdbc.io/docs_cn/02-guide/transaction/

### 4.4.3 mycat 中间件

## 5. Trafodion
Trafodion supports distributed ACID transaction semantics using the Multi-Version Concurrency Control (MVCC) model. 
http://trafodion.apache.org/architecture-overview.html
Trafodion的事务处理器将并发控制的职责分成两部分，TM(Transaction Manager)负责整个事务的分布式并发控制，保证事务本身的一致性；RM(Resource Manager)负责数据访问的并发控制，保证数据的一致性。
具体来说，RM采用前面所说的MVCC技术，提供Snapshot Isolation级别的数据一致性。
在Trafodion中，每个HBase的Region都是一个RM。一个事务很可能会在多个Region上操作，比如事务需要更新两行数据，而它们分别属于两个不同的Region。在这种情况下，一个事务会有多个RM参与。而HBase的Region很可能运行在不同的物理节点上，因此这是一种分布式事务。分布式事务由TM保证整个事务的一致性。
TM使用两阶段提交协议来保证分布式事务的一致性。
http://blog.itpub.net/30206145/viewspace-1596630/

## 6.架构模式
### 6.1 share nothing和share disk架构
比较典型的share disk数据库有oracle RAC和DB2 PureScale
Share-nothing架构如GreenPlum，DB2,SQL Server及分布式的hadoop使用的是Shared Noting架构，Google Spanner、OceanBase、TIDB
#### 6.1.1. Shared Disk 架构
所有的节点共享一份数据，优点是只要有一个节点可用，就可以访问所有数据；缺点是内存融合（cache fusion）大大限制了它的水平扩展能力。简单地说：可用性高，但可扩展性弱，常见于24*7的高可用性核心业务。
####6.1.2. Shared Nothing 架构
数据和节点具有对应关系，缺点是如果要访问所有数据，必须所有节点都可用；优点是每个节点交互少，很容易扩展。简单地说：可扩展性强，可用性低。多用于VLDB
https://wenku.baidu.com/view/7d99b37f5acfa1c7aa00ccdd.html 
https://en.wikipedia.org/wiki/Shared-nothing_architecture 
http://blog.itpub.net/26277071/viewspace-710924/ 

## 7.微服务架构servicecomb
### 7.1 基于补偿事务的分布式事务saga
### 

## 8.NOSQL数据库
### 8.1 Hbase数据库
HBase架构和设计 http://www.sysdb.cn/index.php/2016/01/10/hbase_principle/
HBase行级事务模型 http://hbasefly.com/2017/07/26/transaction-2/

### 8.2 redis数据库
redis labs 企业版也加了许多新功能，开源版本没有，例如，redis Flash, redis spark connector 
greenplum 增强新功能的企业版是Deepgreen

## 9.关系型数据库
### 9.1 mysql数据库
MySQL跨行事务模型 http://hbasefly.com/2017/08/19/mysql-transaction/


## 10.消息队列、事务消息
### 10.1 分布式开放消息系统(RocketMQ)的原理与实践  http://www.cnblogs.com/wxd0108/p/6038543.html

## 11.分布式数据库
###  11.1 ckrchdb(cockroachdb)
cockroachdb使用go语言开发，ckrchdb国内用户有：百度，京东。爱钱进，今日头条和平安保险（平安科技）
详解CockroachDB事务处理系统http://www.cnblogs.com/foxmailed/p/6885368.html
###  11.2 tidb(pingcap) https://pingcap.com/docs-cn/overview/#tidb-%E7%AE%80%E4%BB%8B
#### TiDB和CockroachDB同为Spanner/F1的开源实现,共同点和差异分别是：
事务模型完全不同;
tidb结构上  Highly layered,存储层和计算层彻底分离，连编程语言都分开，方便对接其他的计算平台;
SQL优化器的设计和侧重点也完全不一样;
虽然同为 RocksDB + Multi-Raft，但是本质上还是不太一样的，比如处理分裂和合并时的一致性这类的实现方式都不太一样;
TiDB架构设计松耦合，拆成 Tidb, tikv, pd 多个不同部署的部分，导致latency很大，针对OLTP的场景性能会很差;
内存型的数据库如voltdb和memsql性能就很好;TIDB的中文文档非常完善。
tidb事务隔离级别 https://pingcap.com/docs-cn/sql/transaction-isolation/
