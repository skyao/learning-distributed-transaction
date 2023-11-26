---
title: "Eventuate概述"
linkTitle: "概述"
weight: 1
date: 2021-03-03
description: >
  Eventuate
---



## Eventuate 介绍

![](https://eventuate.io/i/logo.gif)

### eventuate 的背景

Solving distributed data management problems in a microservice architecture

Microservices accelerate development and enable businesses to innovate faster and stay ahead of the competition. But one major challenge with the microservices architecture is the management of distributed data. Each microservice has its own private database. It is difficult to implement business transactions that maintain data consistency across multiple services as well as queries that retrieve data from multiple services.

> 在微服务架构中解决分布式数据管理问题
>
> 微服务加速了开发，使企业能够更快地进行创新，并在竞争中保持领先地位。但微服务架构的一个主要挑战是分布式数据的管理。每个微服务都有自己的私有数据库。要实现保持多个服务间数据一致性的业务交易以及从多个服务中检索数据的查询是很困难的。



### eventuate 项目介绍

Eventuate™是一个平台，它解决了微服务架构中固有的分布式数据管理问题，使您能够专注于您的业务逻辑。

Eventuate™由以下部分组成：

- **Eventuate Tram** - 一个使用传统（如 JPA / JDBC 和 Entity Framework）持久性的服务框架。你可以轻松地将 Eventuate Tram 添加到你的 Spring Boot、Micronaut、Quarkus 和 .NE T微服务中，而不必重写你的业务逻辑。

- **Eventuate Local** - 一个 event sourcing 框架。 event sourcing 是一种以事件为中心的业务逻辑和持久化编程模型，具有一些优势，包括在数据变化时自动发布事件，对所有更新进行可靠的审计，以及对时间查询的内置支持。 Eventuate Local 包括一个事件存储和客户端库，适用于各种语言和框架，包括 Java、Scala、Spring、Micronaut和Quarkus 框架。

Eventuate：使开发人员能够专注于业务逻辑

- 使用Sagas维护数据一致性

  通过使用 Sagas 实现更新多个微服务中的数据的命令，Sagas 是使用消息协调的本地事务序列。

- 使用CQRS实施查询

  实施查询，通过使用CQRS视图从多个服务中检索数据，这些视图是使用事件维护的容易查询的副本。



## Eventuate 资料



- 官方网站: https://eventuate.io/ 

