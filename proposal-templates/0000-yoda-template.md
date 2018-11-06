# Feature name

* Proposal: [YODA-NNNN](NNNN-filename.md)
* Authors: [Author 1](https://github.com/yodadev), [Author 2](https://github.com/yodadev)
* Review Manager: TBD
* Status: **Awaiting implementation**

*During the review process, add the following fields as needed:*

* Implementation: [rokid/yodaos#NNNNN](https://github.com/rokid/yodaos/pull/NNNNN)
* Decision Notes: [Rationale](https://forums.yodaos.org/), [Additional Commentary](https://forums.yodaos.org/)
* Bugs: [BUG-NNNN](https://bugs.yodaos.org/browse/BUG-NNNN), [BUG-MMMM](https://bugs.yodaos.org/browse/BUG-MMMM)
* Previous Revision: [1](https://github.com/rokid/yoda-evolution/blob/...commit-ID.../proposals/NNNN-filename.md)
* Previous Proposal: [YODA-XXXX](XXXX-filename.md)

## Introduction

A short description of what the feature is. Try to keep it to a
single-paragraph "elevator pitch" so the reader understands what
problem this proposal is addressing.

yoda-evolution thread: [Discussion thread topic for that proposal](https://forums.yodaos.org/)

## Motivation

Describe the problems that this proposal seeks to address. If the
problem is that some common pattern is currently hard to express, show
how one can currently get a similar effect and describe its
drawbacks. If it's completely new functionality that cannot be
emulated, motivate why this new functionality would help YodaOS
developers create better YodaOS code/app.

## Proposed solution

Describe your solution to the problem. Provide examples and describe
how they work. Show how your solution is better than current
workarounds: is it cleaner, safer, or more efficient?

## Detailed design

Describe the design of the solution in detail. If it's a new API,
show the full API and its documentation comments detailing what
it does. The detail in this section should be sufficient for
someone who is *not* one of the authors to be able to reasonably
implement the feature.

## Effect on API compatibility

Will existing correct YodaOS applications stop running due to this
change? Will applications still run but produce different behavior
than they used to? If "yes" to either of these, is it possible for
the YodaOS to accept the old API with a compatibility mode? Is it
possible to automatically migrate from the old API to the new API?
Can YodaOS applications be written in a common subset that works
both with latest version of YodaOS and the new YodaOS to aid in
migration?

## Alternatives considered

Describe alternative approaches to addressing the same problem, and
why you chose this approach instead.
