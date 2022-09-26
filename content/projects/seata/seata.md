---
title: "seata"
linkTitle: "seata"
weight: 1
date: 2021-03-03
description: >
  seata
---



## Seata 介绍

![](https://camo.githubusercontent.com/1fc3d2550abc4f7faf0b60e9cabe1ab825ebee3a1b3571a190da57b708db0c33/68747470733a2f2f696d672e616c6963646e2e636f6d2f696d6765787472612f69312f4f31434e3031317a304a665132373233516744695775485f2121363030303030303030373733382d322d7470732d313439372d3430312e706e67)

Seata == Simple Extensible Autonomous Transaction Architecture

Seata 是一款开源的分布式事务解决方案，致力于在微服务架构下提供高性能和简单易用的分布式事务服务。Seata 将为用户提供了 AT、TCC、SAGA 和 XA 事务模式，为用户打造一站式的分布式解决方案。

### Seata 支持的模式

- [AT 模式](https://seata.io/zh-cn/docs/dev/mode/at-mode.html)：基于 **支持本地 ACID 事务** 的 **关系型数据库**，适用于Java 应用，通过 JDBC 访问数据库。
- [TCC 模式](https://seata.io/zh-cn/docs/dev/mode/tcc-mode.html)：不依赖于底层数据资源的事务支持
- [Saga 模式](https://seata.io/zh-cn/docs/user/saga.html): 长事务解决方案，在Saga模式中，业务流程中每个参与者都提交本地事务，当出现某一个参与者失败则补偿前面已经成功的参与者，一阶段正向服务和二阶段补偿服务都由业务开发实现。目前SEATA提供的Saga模式是基于状态机引擎来实现。
- [XA 模式](https://seata.io/zh-cn/docs/dev/mode/xa-mode.html)：支持XA 事务的数据库。适用于Java 应用，通过 JDBC 访问数据库。

### Seata 的关键术语和组件

> https://seata.io/zh-cn/docs/overview/terminology.html

![145942191-7a2d469f-94c8-4cd2-8c7e-46ad75683636](https://user-images.githubusercontent.com/68344696/145942191-7a2d469f-94c8-4cd2-8c7e-46ad75683636.png)

- #### TC (Transaction Coordinator) - 事务协调者

  维护全局和分支事务的状态，驱动全局事务提交或回滚。

- #### TM (Transaction Manager) - 事务管理器

  定义全局事务的范围：开始全局事务、提交或回滚全局事务。

- #### RM (Resource Manager) - 资源管理器

  管理分支事务处理的资源，与TC交谈以注册分支事务和报告分支事务的状态，并驱动分支事务提交或回滚。

结合这张图片看：

 ![](https://camo.githubusercontent.com/05a283bea3d9313f03d63bf7e917c016249f14721e49796a3a386e61df12c5a4/68747470733a2f2f63646e2e6e6c61726b2e636f6d2f6c61726b2f302f323031382f706e672f31383836322f313534353031333931353238362d34613930663064662d356664612d343165312d393165302d3261613364333331633033352e706e67)

Seata 管理的分布式事务的典型生命周期：

1. TM要求TC开始一个新的全局交易。TC生成一个代表全局事务的XID。
2. XID通过微服务的调用链进行传播。
3. RM将本地事务注册为XID对应的全局事务的一个分支，并将其发送给TC。
4. TM要求TC提交或回滚相应的XID的全局事务。
5. TC驱动XID对应的全局事务下的所有分支事务，完成分支提交或回滚。

 ![](https://camo.githubusercontent.com/7ed522a514df2153b546a50af97b155d2163e30df937a69e5cb4cf04210d74eb/68747470733a2f2f63646e2e6e6c61726b2e636f6d2f6c61726b2f302f323031382f706e672f31383836322f313534353239363931373838312d32366661626562392d373166612d346633652d386137612d6663333137643333383966342e706e67)

### Seata 的发展历史

> https://github.com/seata/seata#history

##### Alibaba

- **TXC**: Taobao Transaction Constructor. Alibaba middleware team started this project since 2014 to meet the distributed transaction problems caused by application architecture change from monolithic to microservices.
- **GTS**: Global Transaction Service. TXC as an Aliyun middleware product with new name GTS was published since 2016.
- **Fescar**: we started the open source project Fescar based on TXC/GTS since 2019 to work closely with the community in the future.

##### Ant Financial

- **XTS**: Extended Transaction Service. Ant Financial middleware team developed the distributed transaction middleware since 2007, which is widely used in Ant Financial and solves the problems of data consistency across databases and services.
- **DTX**: Distributed Transaction Extended. Since 2013, XTS has been published on the Ant Financial Cloud, with the name of DTX 

##### Seata Community

- **Seata** :Simple Extensible Autonomous Transaction Architecture. Ant Financial joins Fescar, which make it to be a more neutral and open community for distributed transaction, and Fescar be renamed to Seata.

## Seata 资料



- 官方：https://seata.io/zh-cn/
- 文档：https://seata.io/zh-cn/docs/overview/what-is-seata.html
- 代码仓库
  - seata java： https://github.com/seata/seata
  - seata go：https://github.com/opentrx/seata-golang
  - seata python： https://github.com/opentrx/seata-python



## Seata Java

> https://github.com/seata/seata





## Seata Go

> https://github.com/seata/seata-go/blob/master/README_ZH.md

Seata是一个非常成熟的分布式事务框架，在Java领域是事实上的分布式事务技术标准平台。Seata-go 是 seata 多语言生态中的Go语言实现版本，实现了 Java 和 Go 之间的互通，让 Go 开发者也能使用 seata-go 来实现分布式事务。

Seata-go 的原理和 Seata-java 保持一致，都是由 TM、RM 和 TC 组成，其中 TC 的功能复用 Java 的，TM和RM功能后面会和 Seata-java对齐，整体流程如下：

![145942191-7a2d469f-94c8-4cd2-8c7e-46ad75683636](https://user-images.githubusercontent.com/68344696/145942191-7a2d469f-94c8-4cd2-8c7e-46ad75683636.png)

完成度：从readme页面介绍看，和java版本差距很大，XA/AT/SAGA 模式都没有实现，暂时只有TCC模式。

