# Yoda Evolution

The Yoda Evolution is inspired by [Swift Evolution][] for maintaining proposals for changes and user-visible enhancements to the YodaRT.

This repository tracks the ongoing evolution of YodaRT as the following:

- Goals for upcoming YodaRT releases.
- The tracking [proposals](./proposals.md) to change YodaRT.
- The [YodaRT evolution process](#process) that governs the evolution of YodaRT.
- [Commonly Rejected Changes](#commonly-rejected-changes), proposals that have been denied in the past.

This document describes goals for YodaRT on a per-release basis, that includes minor and major releases. YodaRT Evolution is to provide
platform where all the developers and users of Yoda shall be involved with the community. We hope anybody no matter who you are is easy
to contribute the Yoda in anyway that improved something.

### Process

YodaRT is the voice user interface framework that based on Node.js and ShadowNode, it's powerful and friend to JavaScript community and
middle-low-end devices like Alexa, Kamino, Google Home and etc., it's growing and evolving, guided by a community-driven process referred
to as the Yoda Evolution Process. This document outlines the Yoda Evolution Process and how a feature is integrated into the framework
from a rough idea that can improve the YodaRT.

#### Scope

The Yoda evolution process covers all the changes to the YodaRT and the [YodaRT API][], that contains:

- The built-in modules API changes.
- Changes to existing user interface features or APIs.
- Deprecations of existing features.
- The [ShadowNode][], Node.js runtime at low-end device, features or APIs.

And the smaller changes, such as bug fixes, optimizations and diagnostic improvements should be contributed via the normal contribution
process on our [YodaRT Contributing][].

#### Goals

The Yoda Evolution process is to leverage the collective idea, insights and user experience of the Yoda community to improve the development
experience for developers, and the user experience to the voice-based products that based on Yoda.

#### Participation

Everyone is welcome to propose, discuss and review ideas to improve YodaRT at [yoda-evolution][]. Before posting a review, please see the
section ["What goes into a review"](what-goes-into-a-review) below.

The Yoda TSC is responsible for the strategic direction of Yoda herself. TSC members initiate, participate in, and manage the public review
of proposals and have the authority to accept or reject changes.

#### What goes into a review

The review process is to improve the proposal under review through constructive criticism and, eventually, determine the direction of YodaRT.
Here are some questions you might want to answer in your review:

- What is your evaluation of the proposal?
- Is the problem being addressed significant enough to warrant a change?
- Does this proposal fit well with the feel and direction of YodaRT?
- How much effort did you put into your review? A glance, a quick reading, or an in-depth study?

Please state explicitly whether you believe that the proposal should be accepted into YodaRT.

#### How to propose a change

- __Check prior proposals__: the brain of human beings is always in activity, that there was some ideas comes up frequently, and maybe in active
  discussion on the [yoda-evolution][] or have been discussed already and have joined the [Commonly Rejected Proposals][] list. Please search the
  above places for context before proposing something new.
- __Socialize the idea__: propose a rough sketch of the idea what the solution looks like, etc., to gauge interest from the community.
- __Develop the proposal__: from starting with Yoda Evolution, using the [proposal template][], and continue to refine the proposal on your Pull
  Request on [yoda-evolution][]. Prototyping an implementation and its uses along with the proposal is _required_ because it helps ensure both
  technical feasibility of the proposal as well as validating that the proposal solves the problems it is meant to solve.
- __Request a review__: create a pull request to [yoda-evolution][] to indicate to the TSC that you would like the proposal to be reviewed. When
  the proposal is sufficiently detailed and clear, a member of TSC could label this pull request as `active review`, then it could be discussed
  and accepted/rejected on next Yoda Dev Day(YDD).

#### Review process

The review process for a particular proposal begins when a TSC member leaves review comments on a pull request. The TSC member becomes the
_review manager_ for the proposal. Every proposal must be assigned a proposal number (if it is a new proposal), then enters the review queue.

The review manager will work with the proposal authors to schedule the review. Reviews usually last a single week, but can run longer for
particularly large or complex proposals. Once the pull request is submitted, the proposal authors and review manager should be available to
answer questions, address feedback, and clarify their intent during the review period.

After the review has completed, and marked as `active review`, the review manager should guides the author to prepare the presentation on the next
Yoda Dev Day, where the proposal could be accepted, returned to feedback and rejected by TSC and developers. After Yoda Dev Day, the review manager
is responsible to update the proposal's state in [yoda-evolution][].

#### Proposal states

A given proposal can be in one of several states:

- __Drafting__: Yoda Evolution accepts someone is drafting their proposal online, which makes proposal authors could get feedback earlier.
- __Awaiting review__: The proposal is awaiting review, commonly when the proposal authors has completed the `Drafting`, the TSC member is required
  to update the state to `awaiting review` on [yoda-evolution][].
- __Active review (The date of Yoda Dev Day)__: The proposal is undergoing public review at next Yoda Dev Day, when the review manager accepts a
  proposal that can be reviewed publicly, review manager should label this pull request as `active review`.
- __Revision required__: After a proposal with `active review` state and returned with feedbacks, the review manager should label this pull
  request as `revision required`.
- __Accepted__: After a proposal with `active review` state is accepted, the review manager should label this pull request as `accepted`.
- __Rejected__: After a proposal with `active review` state is rejected, the review manager should label this pull request as `rejected` and close
  this pull request.
- __Implemented (Yoda Version)__: The proposal has been implemented with the version that implements this proposal.

[YodaRT API]: https://yodaos.rokid.com/docs/0.6/
[YodaRT Contributing]: https://github.com/Rokid/YodaRT
[yoda-evolution]: https://github.com/Rokid/yoda-evolution
[Swift Evolution]: https://github.com/apple/swift-evolution
[ShadowNode]: https://github.com/Rokid/ShadowNode
[proposal template]: ./proposal-templates/0000-yoda-template.md

