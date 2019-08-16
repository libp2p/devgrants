# Gossipsub threat analysis

# Motivation and context

<!-- Describe what's the current situation, where this project fits in, where does this proposal emerge from, etc. -->

libp2p offers multiple publish-subscribe (PubSub) messaging algorithms, the most widely used of which is based on a [gossip](https://en.wikipedia.org/wiki/Gossip_protocol) protocol.

We need to understand how malicious users could misuse libp2p's gossipsub to create problems for the network.  These types of problems might include:
- excessive trust by nodes that gossip messages are valid and have not been tampered with
- malformed gossipsub messages intended to cause nodes to enter an invalid state, or even crash
- denial of service attacks that slow or halt operation of a libp2p network

# Value

<!-- Help the community understand the worth of carrying out this project, by filling out the benefits and risks subsections. Write any general comments here. -->

Without an explicit threat model, it is hard to say whether libp2p gossipsub is "secure" or "not secure."  Most likely, there will be some attacks we can prevent entirely, and others for which we can only raise the cost of an attack but can never fully guarantee against.  Completion of this dev grant will enumerate all possible attacks against a gossipsub-based network and allow us to define explicitly what the existing version of gossipsub is and isn't resilient against.  Moreover, for attacks where we can only raise the cost, but not prevent, the grantee will calculate the approximate cost of carrying out the attack. 

## Benefits (if addressed)

<!-- Describe how addressing this project would result in positive effects for the libp2p stack, community, implementers (people _building_ libp2p), downstream users (developers _using_ libp2p in their projects), etc. -->

Have a well-defined threat model will bring clarity to the community about what guarantees gossipsub is and is not making.  It will also help the community understand grey areas, like DoS attacks that are possible but very expensive.  By quantifying the cost of an attack -- e.g., percentage of the network the attacker needs to control -- Ethereum 2.0 developers can make informed decisions about what is an acceptable level of risk.

## Risks (if not addressed)

<!-- Describe what would be harmed, damaged or rendered inefficient if the community decides to discard this project (including possible worst case scenarios). -->

Failing to define an explicit threat model will lead to confusion in the community about what is meant by saying gossipsub isn't "secure" or that a certain attack is/isn't "possible".  This might cause Ethereum 2.0 designers and application developers to put too much trust into gossipsub, and then be disappointed when a successful attack occurs.

In addition, not having a clearly-defined threat model is an invitation for unscrupulous actors to sow Fear, Uncertainty and Doubt (FUD) about Ethereum 2.0 and libp2p.  Statements like "Ethereum 2.0 relies on an insecure gossipsub protocol" could appear on social media or in the press, and the Ethereum community won't be able to combat these deceptive statements because we won't have a threat model that defines explicitly what we mean by _secure_ in the gossipsub context.

# Expected output and constraints

<!-- Describe what you'd expect to be delivered by whoever picks up this bounty. Specify any timeline or scope constraints (e.g. "this needs to be finished by end of October 2019 because...") -->

- The expected output is a threat model document that outlines each category of possible attacks and whether gossipsub is secure against, not secure against it, or not secure against it but requires substantial attack resources.  (The notion of "substantial resources" should be quantified, or at least estimated, for the last category of attack.)  This will provide a framework to know whether a particular vulnerability is a bug or a previously-known limitation.
- The document should explain the _implications_ of each category of attacks on the Ethereum 2.0 network.  The grantee may wish to provide a rubric, e.g., DoS attacks that could slow or halt the network might be considered a less severe category than attacks that allow the attacker to steal funds or alter a transaction after it has been accepted.
- Exploit code demonstrating all or some of the reported attacks will be very well received.

# Relevant discussion

<!-- If there has been past discussion about this project, provide pointers. Plus points if you synthesize the gist. -->

The specification for libp2p's gossipsub is found [here](https://github.com/libp2p/specs/tree/master/pubsub/gossipsub).

The grantee is expected to search and cite any relevant academic literature on the security of gossip protocols, as well as substantive discussions on social media such as Github, Twitter, blogs, etc.

# Design/implementation notes

<!-- Optional: if you have an idea in mind of how this would be accomplished, write down your notes here. -->

- This is a document written in English language prose.
- The grantee may wish to use a tabular format to summarize the categories of attack and whether libp2p's gossipsub protocol is designed to be secure against it, not secure against it, or not secure but guarantees that exploitation requires substantial resources.
- For attacks that are possibly but require high levels, the grantee may wish to create simulation code to demonstrate feasibility by attackers who control varying numbers of nodes (e.g., 0.1% of the entire network, 1% of the network, 10%, etc).

# Potential funders

<!-- Optional: know of projects or organizations that would benefit from seeing this project come to fruition? Enumerate them here, supplying some context, and possibly mention the relevant people. -->

- EthBerlinZwei community bounty pool
- Protocol Labs
- Ethereum Foundation (if the work is focused on the Ethereum 2.0 use case specifically)

