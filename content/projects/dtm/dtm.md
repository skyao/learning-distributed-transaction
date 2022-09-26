---
title: "DTM项目概述"
linkTitle: "概述"
weight: 1
date: 2021-03-03
description: >
  DTM项目概述
---

![dtm](https://www.dtm.pub/dtm.svg)

## DTM 项目介绍

A distributed transaction framework, supports workflow, saga, tcc, xa, 2-phase message, outbox patterns, supports many languages.

> 一个分布式事务框架，支持工作流、saga、tcc、xa、2阶段消息、outbox模式，支持许多语言。

GO语言分布式事务管理服务

DTM == Distributed Transaction Manager

DTM是一款开源的分布式事务管理器，解决跨数据库、跨服务、跨语言栈更新数据的一致性问题。

DTM是一个分布式事务框架，提供跨服务的最终数据一致性。它为各种应用场景提供了saga、tcc、xa、2阶段消息、outbox、工作流模式。它还支持多语言和多存储引擎，以形成如下的事务：

![](https://camo.githubusercontent.com/f817a12c015a6cc842e5a5ed9af869ffa5768bee37bdb7f2f3b6e807fa10cdba/68747470733a2f2f656e2e64746d2e7075622f6173736574732f66756e6374696f6e2e37643536313866382e706e67)

特点(来自：https://www.dtm.pub/)：

- 💡 极易接入

零配置启动服务，提供非常简单的HTTP接口，极大降低上手分布式事务的难度，新手也能快速接入

- ⚡️ 跨语言

可适合多语言栈的公司使用。方便go、python、php、nodejs、ruby、c# 各类语言使用。

- 🛠️ 使用简单

开发者不再担心悬挂、空补偿、幂等等异常问题，首创子事务屏障技术代为处理

- 📦 易部署、易扩展

依赖mysql|redis，部署简单，易集群化，易水平扩展

- 🔩 多种分布式事务协议支持

TCC、SAGA、XA、二阶段消息，一站式解决所有分布式事务问题



## DTM 支持的模式

- 二阶段消息：

​	二阶段消息是dtm首创的事务模式，用于替换本地事务表和事务消息这两种现有的方案。

​	见文档：[例子](https://www.dtm.pub/guide/e-msg.html) 和 [原理](https://www.dtm.pub/practice/msg.html)

- SAGA 模式

​	见文档：[例子](https://www.dtm.pub/guide/e-saga.html) 和 [原理](https://www.dtm.pub/practice/saga.html)




## DTM 项目资料

- 网站：https://www.dtm.pub/

- github： https://github.com/dtm-labs/dtm
