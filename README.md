<p align="center"> <a href="https://libp2p.io"><img
  src="https://raw.githubusercontent.com/libp2p/libp2p/master/logo/white-bg-3.png"
  width="360" /></a> </p>

<p align="center"> <a href="http://libp2p.io/"><img
  src="https://img.shields.io/badge/project-libp2p-yellow.svg?style=flat-square"
  /></a> <a href="http://webchat.freenode.net/?channels=%23libp2p"><img
  src="https://img.shields.io/badge/freenode-%23libp2p-yellow.svg?style=flat-square"
  /></a> <a href="https://twitter.com/intent/follow?screen_name=libp2p"><img
  src="https://img.shields.io/twitter/follow/libp2p.svg?style=social&label=Follow%20@libp2p"
  alt="Follow on Twitter"></a> </p>

> **This repository tracks projects, initiatives and chunks of libp2p work
> that are (or may become) incentivized, for enthusiastic OSS contributors to
> pick up and tackle.**

> Refer to the [issue tracker] to browse what's being funded and/or discussed,
> and what's the status of proposals. Explore the [labels] for quicker
> navigation.


## Table of contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [What is this? ❓](#what-is-this-)
- [Motivation 🎈](#motivation-)
- [Repo structure 🧩](#repo-structure-)
- [Submitting a proposal 📝](#submitting-a-proposal-)
- [For developers 👾](#for-developers-)
- [Need help? 🙌](#need-help-)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## What is this? ❓

This repository tracks projects, initiatives and chunks of
libp2p work that are (or may become) incentivized, for talented OSS
contributors to pick up and tackle.

Objects of devgrants include: protocol implementation, tooling implementation,
research, testing, optimization, etc. They may target one or more libp2p
libraries, or they may be universal efforts to advance the entire ecosystem.

We track project proposals as GitHub issues, and specifications as markdown
documents. To make browsing easier, you can find the latest project statuses
and discussions in this repo's [issue tracker].

Issues are categorized along various axes using [labels]:

* Complexity: Low, Medium, Hard, Extreme.
* Status: Proposed, Funded, Delivered, Discarded.
* Readiness: Yes, No.
* Programming languages (e.g. Go, Rust, JS, Java, etc.)
* Topics (e.g. security, DHT, pubsub, etc.)
* Selected (e.g. for hackathon X, round Y, etc.)

## Motivation 🎈

The libp2p networking stack is becoming a public good. Major large-scale
projects like ETH2, Filecoin, Polkadot, IPFS, Cosmos, etc. are adopting libp2p
as a foundation for their networking layers.

Collaboration in the p2p space is indispensable to build truly unstoppable,
future-proof p2p networks. All these projects share the motivation to propel
libp2p forward towards higher robustness, maturity, and feature richness.

This repo serves as the junction between those communities to propose,
enumerate, discuss, and agree on jointly funding crucial, substantial chunks of
work that, when addressed, would benefit various actors synergystically, or
even the entire ecosystem altogether.

Note: how devgrants are actually allocated, contracts signed and payments
settled is out of the scope of this repo. This may happen through hackathons
(e.g. ETHBerlin), privately, or eventually via some kind of [Decentralized
Autonomous Organization] (how cool would that be 😎).

## Repo structure 🧩

Each proposal/devgrant is tracked in a dedicated **issue**. The [issue
tracker] indexes and tracks the status of project proposals and devgrants. It
also serves as the discussion forum.

**Specifications** live in markdown documents, with their filenames
referencing the devgrant by GitHub issue number.

## Submitting a proposal 📝

> _This is all new and we're still figuring out the process and details, so
> bear with us :-)_

Submitting a project proposal is easy. It consists of filing an issue, and an
associated PR, following a simple template.

**Here's the how-to:**

1. File an issue with the title of the proposal as a placeholder. Take note of
   the issue number.
2. Fork the repo, and copy the file `TEMPLATES/000-project-proposal.md` to the
   root of your fork.
    * Fill in as much detail as you can.
    * The submission doesn't need to be perfect, we can sort out details
      later. At this stage, we want to keep the barrier to propose a project
      low.
    * In the filename, replace `000` with the number of the placeholder issue
      you created above.
3. Submit a PR to this repo. Make sure you enable the _[allow edits from
   maintainers]_ option in the PR screen. Then go back and edit the issue,
   adding a link to the new PR.

**That's all! Here's what happens next:**

1. The community reviews the proposal PR, enhances it, refines it, discusses
   it, etc.
      * This is deliberately left unstructured, but we expect downstream
        project(s) to chime in to champion, and tentatively commit to fund XYZ
        amount towards the execution.
2. An experienced libp2p community member comes along and fills in technical
   details to lock down scope, write up an actionable spec, and provide 
   resources, guidance or references, in order to streamline the ramping up of
   the grantee.
      * They will need to commit to your PR's branch, that's why we need the
        "allow edits from maintainers" option enabled.
3. The scoped & spec'ed proposal is once again reviewed by the community.
   Additional projects may chime in to co-fund. After a sensible period,
   the committed grant amount will be locked in the proposal description.
4. Via the assigned off-band mechanism (hackathon, email, DAO), contributors
   signal interest, and co-funders communicate to select a grantee.
5. That grantee delivers the project.

## For developers 👾

Watch this repo to stay up to date with project proposals and to engage in the
discussion as potential grantees.

## Need help? 🙌

For questions or feedback, contact: [@raulk].

## License

Dual-licensed under MIT and ASLv2, by way of the [Permissive License Stack].

[labels]: https://github.com/libp2p/devgrants/labels
[Decentralized Autonomous Organization]: https://twitter.com/ameensol/status/1154529769276362752
[allow edits from maintainers]: https://help.github.com/en/articles/allowing-changes-to-a-pull-request-branch-created-from-a-fork
[issue tracker]: https://github.com/libp2p/devgrants/issues
[@raulk]: https://github.com/raulk
[Permissive LIcense Stack]: https://protocol.ai/blog/announcing-the-permissive-license-stack/
