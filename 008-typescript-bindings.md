# TypeScript bindings for js-libp2p-*

## Motivation and context

<!-- Describe what's the current situation, where this project fits in, where does this proposal emerge from, etc. -->

`js-libp2p` integration into TypeScript projects is not straightforward not up to the general DX level that language community is accustomed to. The lack of stable bindings implies a considerable amount of fiddling due to most things being an Any type, or outdated.

As a result, the team developing a TypeScript project using `js-libp2p` tends to develop type declarations for the libp2p modules that they depend on, adding to the workload.

We want to make `js-libp2p` pleasurable and seamless to use with TypeScript projects.

## Value

<!-- Help the community understand the worth of carrying out this project, by filling out the benefits and risks subsections. Write any general comments here. -->

TypeScript projects will be able to use libp2p out of the box without worrying about pulling in any types. 3rd party types do exist, but need to be updated there anytime an api change occurs with libp2p.

### Benefits (if addressed)

<!-- Describe how addressing this project would result in positive effects for the libp2p stack, community, implementers (people _building_ libp2p), downstream users (developers _using_ libp2p in their projects), etc. -->

When we provide TypeScript bindings for all `js-libp2p` modules, libp2p will become a viable networking layer for TypeScript developers.

### Risks (if not addressed)

<!-- Describe what would be harmed, damaged or rendered inefficient if the community decides to discard this project (including possible worst case scenarios). -->

New TypeScript projects looking for a networking solution will not take into account libp2p, as a result of all the integration work needed.

## Expected output and constraints

<!-- Describe what you'd expect to be delivered by whoever picks up this bounty. Specify any timeline or scope constraints (e.g. "this needs to be finished by end of October 2019 because...") -->

The expected output is to have typing declarations to all `js-libp2p` modules.

## Relevant discussion

There has been discussion around TypeScript declarations at https://github.com/libp2p/js-libp2p/issues/208. The Polkadot team has created bindings for many of the libp2p modules, https://github.com/polkadot-js/ts/tree/master/types. The major issue is that these bindings have to get updated any time a change to the api is created. The hope is to move the bindings into their relevant modules, so that they ship and are updated with the JS code.

## Design/implementation notes

- The implementation should ensure that the TypeScript bindings are easy to maintain. As js-libp2p is pushing to have full jsdocs for all code, generating the bindings from the jsdocs is a potential option.
- CI should run a check on the bindings to verify they're up to date. This step should be allowed to fail to avoid blocking contributors on this step.

## Potential funders

Protocol Labs, ETHBerlinZwei.