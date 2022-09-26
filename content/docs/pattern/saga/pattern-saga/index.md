---
title: "[翻译]Saga模式"
linkTitle: "Sage模式"
weight: 300
date: 2021-03-03
description: >
  分布式事务的Saga模式
---

> 文章翻译自：[Sagas (microservices.io)](https://microservices.io/patterns/data/saga.html)

## 上下文

在应用 database per service 模之后，每个服务都有自己的数据库了。然而，一些业务事务跨越了多个服务，所以需要一种机制来实现跨服务的事务。例如，让我们想象一下，当建立电子商务商店时，客户有一个信用限额。该应用程序必须确保新的订单不会超过客户的信用额度。由于订单和客户在不同的服务所拥有的不同数据库中，应用程序不能简单地使用本地ACID事务。

## 问题

如何实现跨服务的事务？

## 动力

2PC（两阶段提交）不合适

## 解决方案

Saga 用来实现跨越多个服务的每个业务事务。saga 是本地事务的一个序列。每个本地事务都会更新数据库并发布一个消息或事件，以触发 sage 中的下一个本地事务。如果某个本地事务因为违反了业务规则而失败，那么 saga 会执行一系列的补偿性事务，撤销前面的本地事务所做的改变。

![From_2PC_To_Saga](images/From_2PC_To_Saga.png)

 saga 有两种协作方式：

- 协调（Choreography）： 每个本地事务都会发布领域事件，触发其他服务中的本地事务
- 编排（Orchestration）：编排者（对象）告诉参与者要执行哪些本地事务

## 示例：基于协调的 saga

![Create_Order_Saga](images/Create_Order_Saga.png)

使用这种方法的电子商务应用程序将使用基于协调（choreography）的 sage 来创建订单，包括以下步骤：

1. Order service 接收 `POST /orders` 请求，并创建一个 PENDING 状态的订单。
2. 然后，它发出一个 `Order Created`事件
3. Customer Service 的事件处理程序试图预留信用额度。
4. 然后发出一个表明结果的事件
5. OrderService的事件处理程序批准或拒绝该订单。

## 示例：基于编排的 saga

![Create_Order_Saga_Orchestration](images/Create_Order_Saga_Orchestration.png)

使用这种方法的电子商务应用程序将使用基于编排的saga创建订单，其中包括以下步骤：

1. order service 接收 `POST /orders` 请求，并创建 `Create Order` saga 编排器。
2. saga 编排器创建一个 PENDING 状态的订单
3. 然后，它向 customer service 发送一个预留信用额度的命令
4. customer service 尝试预留信用额度
5. 然后发回一条回复信息，说明结果
6. Saga 编排器要么批准要么拒绝该订单。

## 结果的背景

这种模式有以下好处：

- 它使应用程序能够在不使用分布式事务的情况下保持多个服务的数据一致性

这种解决方案有以下缺点：

- 编程模型更加复杂。例如，开发者必须设计补偿性事务，明确地撤销在 saga 中早期所做的改变。

还有以下问题需要解决：

- 为了可靠，服务必须原子性地更新其数据库并发布消息/事件。它不能使用跨数据库和消息代理的分布式事务的传统机制。相反，它必须使用下面列出的模式之一。

- 发起 saga 的客户端，这是一个异步流，使用一个同步请求（例如HTTP `POST /orders`），需要能够确定其结果。有几种选择，每一种都有不同的权衡。

	- 服务在 saga 完成后发回一个响应，例如，一旦它收到 `OrderApproved` 或 `OrderRejected` 事件。
- 服务在启动 saga 后发回一个响应（例如，包含 `orderID`），客户端定期轮询（例如，`GET /orders/{orderID}`）以确定结果。
- 服务在启动 saga 后发回一个响应（例如，包含 `orderID`），然后在 saga 完成后向客户端发送一个事件（例如，websocket、web hook等）。
