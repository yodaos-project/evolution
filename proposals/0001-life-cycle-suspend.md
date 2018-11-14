# Suspend In LifeCycle

* Proposal: [YODA-0001](0001-life-cycle-suspend.md)
* Authors: [Chengzhong Wu](https://github.com/legendecas)
* Review Manager: TBD
* Status: **Awaiting Review**

## Introduction

It is required for applications to distinguishing `destroy` events that if _application process_
is going to exit or _skill_ is going to be evicted so that application developers could determine
which resources shall be released on receiving of the events.

## Motivation

Currently, YodaOS mainly focused on how applications' lifetime events interact with skill's
interface, such as nlp `request`s, `pause` of skills, etc.

With applications migrated to their own separate process from vui's main process, eviction of
skills and suspending of application processes may have different resources been collected.
On the eviction of skills, ephemeral resources allocated in the process of user's input shall
be reclaimed, whilst long-living resources such as a kept alive tcp connection could be left
active and destroyed alone with application processes' destroy.

Hence, a single `destroy` event could not fulfill our requirements. A new event which would be
fired before application processes exit could be introduced to get application maintainers
informed with processes important life events.

Also, event split of skill evictions and application process exits may enable the delayed
application exits after the eviction of skills. Currently an application process would
immediately been destroyed after eviction of skills, which heavily overloads devices to
frequently fork a new process on new user inputs.

## Proposed solution

A possible solution to inform applications might be adding an event `activity#suspend`
which would only be fired on the eviction from currently active skill stack, and reducing
the scope of the original `activity#destroy` event to representing that the application
processes are going to exit.

In this section we take Bluetooth app as an example to explain the details of the new
design.

Bluetooth app would like to disconnect from currently connected devices on the eviction
of skill, and finally close devices' bluetooth broadcast on exit of app.

In the case, Bluetooth app would disconnect connected devices on `activity#suspend` and
close bluetooth broadcast on `activity#destroy`.

## Detailed design

Since application garbage collection already have been introduce to YodaRT in recent versions,
there would be no system status chaos brought in the changes.

The proposed solution may be implemented by following steps:
- a new event descriptor of `activity#suspend` shall be added to ActivityDescriptor.
- application destroying APIs in LaVieEnPile shall be renamed to skill suspending related naming.
- event `activity#destroy` shall be emitted on `AppScheduler#suspendAppById` before destroying of application processes.

## Effect on API compatibility

Applications have to have its skill eviction listener migrated to listening on event `activity#suspend`.
