# Analysis of Privacy and Anonymity guarantees of libp2p

## Motivation and context

<!-- Describe what's the current situation, where this project fits in, where
does this proposal emerge from, etc. -->

Libp2p provides a set of libraries and modules for building peer-to-peer networks. As privacy is getting more important, projects using libp2p may want to extend its functionality by providing transports to well-known anonymity networks or build their own. In order to effectively do this, we need to understand the privacy and anonymity guarantees of the current libp2p stack and see how they can be rectified, and how to offer features that offer minimal privacy and anonymity to libp2p users.

## Value

<!-- Fill out the benefits and risks subsections below to help the community
understand the value/worth of carrying out this project. Write any general
comments here. -->

Without providing libp2p users with a clear understanding of the privacy and anonymity guarantees of the system, they can be under the false impression that libp2p provides privacy and anonymity. Further, for those that do understand the ramifications, they may end up needing to implement privacy and anonymity and this increases the amount of work needed for those projects. 

### Benefits (if addressed)

<!-- Enumerate how addressing this project would result in positive effects
for the libp2p stack, community, implementers (people _building_ libp2p),
downstream users (developers _using_ libp2p in their projects), etc. -->
Knowing explicit what kind of privacy and anonymity guarantees libp2p provides gives projects a better overall view of whether libp2p fits their needs. Further, it'll give the libp2p community the opportunity to find solutions for better building private, p2p networks. 

### Risks (if not addressed)

<!-- Enumerate what would be harmed, damaged or rendered inefficient if the
community decides to discard this project (including possible worst case
scenarios). -->

Usually, adding private or anonymous features by default into a system tends to reduce the scalability of said system and tends to not be backwards compatible, i.e. once already deploy previous users of the systems do not get to take advantage of the new privacy features. Another issue with adding private features by default is the increase risk of sybil attacks and increased susceptibility to DoS attacks. 

## Expected output and constraints

<!-- Describe what you'd expect to be delivered by whoever picks up this
bounty. Specify any timeline or scope constraints (e.g. "this needs to be
finished by end of October 2019 because...") -->

- The expected output is a document that outlines the ways in which libp2p doesn't provide privacy and anonymity, along with a set of recommendations on how to improve this for libp2p users.

- The document should outline the pros and cons with respect to adding privacy features to libp2p by default and the potential ramification for existing networks (IPFS, Eth2.0, Polkadot, etc)

## Relevant discussion

<!-- If there has been past discussion about this project, provide pointers.
Plus points if you synthesize the gist. -->

## Design/implementation notes

<!-- Optional: if you have an idea in mind of how this would be accomplished,
write down your notes here. -->

## Potential funders

<!-- Optional: know of projects or organizations that would benefit from
seeing this project come to fruition? Enumerate them here, supplying some
context, and possibly mention the relevant people. -->
