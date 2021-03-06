---
layout: post
title: 谈微服务实施的价值
tags: [Microservices, 微服务, DevOps]
---
{% include JB/setup %}

几年前我在一家互联网公司的一个电商产品上工作时，经历了项目从无到有、业务从小到大的演变过程。当时微服务架构还没有兴起，产品架构主要是基于单体架构的。在一年多时间内，业务流量就扩大了十倍左右，各种功能特性需求也应接不暇。随着业务流量和复杂性的攀升，单体架构的问题很快凸显了出来。

首先是系统复杂度不断上升。由于对业务只进行了简单的划分，分为两三个大的代码库，所有人的代码提交都在这两三个代码库上进行，久而久之模块之间的耦合越来越多，代码的整洁性和可读性都不断下降，一个文件几千行、一个函数几百行的情况也屡见不鲜。一个臃肿的单体系统编译、启动、构建都会变慢，发展到后来在本地启动主系统就需要5-10分钟，可想而知开发人员在这些上面每天又会浪费多少等待时间。

其次是质量缺陷成为一大困扰。由于系统复杂，模块之间耦合多，不容易写自动化测试，在交付压力的驱使下开发只好以满足功能上线为第一目标，所以导致生产环境经常出现bug，有时甚至是影响到核心功能的严重bug，不得不在线回滚，给公司带来了损失之外又增添了额外的修复成本，而且也影响着团队的上线信心。

架构的腐化也制约着创新的动力，团队中有些愿意尝试新技术、新架构的成员，但一想到如何从纷繁复杂的代码中理出个头绪，引入新技术的同时又不影响现有系统功能，往往就打退堂鼓了。

同时，发布的风险也在逐渐增大，当时这样的系统以多实例方式部署在多个虚拟机上，自动化部署程度不高，而且生产环境和测试环境多少会有些不一致的现象。再加上前述的各种因素，导致往往在测试环境难以发现性能和安全方面的问题，往往在上线了以后才发现所发布功能存在一些问题，只好再手动回滚。发布后还需严密关注是否发生异常，久而久之，导致每一次发布都成为开发和运维人员的噩梦，用胆战心惊形容也不为过。

而且，运维方面，由于系统未进行适当的拆分，对于水平扩展也不是那么容易，无法将系统中的性能瓶颈部分进行单独扩容，就只好将整体系统进行扩容，浪费资源倒是其次，主要是有时有些含状态的任务或功能无法直接扩容。

几年后当微服务架构及其相关的持续交付、DevOps、敏捷等实践逐步兴起时，我意识到曾经遇到过的问题不只是我们才遇到。而这些思想和方法的出现，正是为了解决这些问题。在我看来微服务相关的实践实施的价值点主要有：

**更简单。**如果一件事情太复杂，目标太大，就对其分解成若干个小目标，分而治之各个击破，就会感觉容易许多。微服务正是体现着这样的思想，对系统进行适当的拆分，组成一个个高内聚低耦合的模块化服务，服务之间以轻量级通信进行交互，每个服务在独立进程中运行，可独立部署快速发布。无形中让各个微服务的复杂度降低了许多，写自动化测试也变得相对容易许多，让团队对开发质量和速度都能有所兼顾。

**更可靠。**持续构建、持续部署等开发流水线的实践都强调尽可能用标准化和自动化的方式去完成团队日常工作中的重复部分。这不仅仅是为了避免重复劳动，也是为了建立更加易于追踪和控制的系统，提高可靠性，避免因人的手工作业疏忽所带来的问题。

**更敏捷。**敏捷方法论中的核心思想之一是建立快速反馈的通路，这样团队才能更快地知道自己是否走在正确的道路上，及时作出调整和优化。看板、CI、自动化测试等实践的目的之一都是让团队能够快速而直观地得到作业状态和结果的反馈。小而精的微服务系统，也让各项作业的执行更加快速，从而能够更快地得到反馈。

当然微服务架构也是一把双刃剑，并不是每个产品都适合实施微服务，实施过程中也避免不了各种阵痛。但只要团队能够认识到微服务实施的价值所在，提前评估和控制好风险，在落地过程中发展出真正适合自己的实践，就能发挥其作用。
