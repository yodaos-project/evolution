# Suspend In LifeCycle

* Proposal: [YODA-0001](0001-life-cycle-suspend.md)
* Authors: [Chengzhong Wu](https://github.com/legendecas)
* Review Manager: TBD
* Status: **Drafting**

## Introduction

应用需要区分 destroy 事件是技能退出还是进程退出来决定需要回收哪些资源。

## Motivation

在 YodaOS 最开始的版本中，对于应用进程的生命周期事件的描述比较薄弱，重点在于技能的生命周期，如 nlp，pause 等。
后来在强化了进程的生命周期后，我们将 create 与 active 等激活状态分离，分别用于描述进程的创建与技能进入活跃状态。
但是没有将进程的退出与技能的退出做细致区分：目前 YodaOS 的应用进程退出是与技能退出同步的。像蓝牙音乐应用希望在退出时关闭蓝牙连接，而对蓝牙应用来说，蓝牙技能的退出即代表了蓝牙应用进程也会很快退出，所以蓝牙应用可以不用关心技能的退出或者是进程的退出，只用在退出时关闭蓝牙连接即可。

但是，在越来越多的应用使用了 daemon 模式，或者是在后续的 YodaOS 引入应用延迟销毁机制后，应用进程的退出与技能的退出不再同步，应用就需要区分应用进程的退出与技能的退出：在进程退出前，将一些需要长期保持活跃的资源回收；但是不在技能退出的时候回收该资源，以便后续 YodaOS 可以快速复用这个应用进程。

## Proposed solution

增加 activity#suspend 事件，代表了应用技能退出了活跃状态。原 activity#destroy 则只代表应用进程即将退出。

## Detailed design

在最近几个版本的 YodaOS 中，增加了大量的应用资源随着生命周期自动回收的功能，如 TTS/媒体等，而不再依赖应用自身监听生命周期事件来暂停这些资源，所以应用中的 activity#destroy 可以只关心应用自身的资源，如保持的长连接等的销毁。这样系统的行为即可以被保证不因应用没有处理 activity#suspend 或者 activity#destroy 事件而错乱。

增加 activity#suspend 事件需要在 ActivityDescriptor 中增加对 activity#suspend 事件的描述，并将生命周期管理器 LaVieEnPile 中 destroyAppById 修改为 suspendAppById，同时需要将该方法中发送的 activity#destroy 修改为 activity#suspend事件；而应用进程管理器 AppScheduler 中的 suspendAppById 中，如果确实是要销毁应用进程，则需要增加给应用发送 activity#destroy 事件，再销毁应用进程。

## Effect on API compatibility

需要应用将原有的 activity#destroy 监听中区分是希望在技能退出，亦或是进程退出的代码，然后将需要提前在技能退出时即销毁的资源迁移至 activity#suspend 的监听中。
