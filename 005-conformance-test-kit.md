# Motivation and context

In this day and age, there are two generations of libp2p libraries:

* mature implementations: [go-libp2p](https://github.com/libp2p/go-libp2p),
  [js-libp2p](https://github.com/libp2p/js-libp2p),
  [rust-libp2p](https://github.com/libp2p/rust-libp2p).
* developing implementations:
  [jvm-libp2p](https://github.com/libp2p/jvm-libp2p),
  [cpp-libp2p](https://github.com/soramitsu/kagome/tree/master/core/libp2p),
  [nim-libp2p](https://github.com/status-im/nim-libp2p).

All are (or intend to be) compliant with the [libp2p
specs](https://github.com/libp2p/specs).

Unfortunately we lack a normative/authoritative test kit/suite to verify
compliance, compatibility and interoperability of a given implementation.

As a result, authors of new implementations rely on big-bang testing against
mature implementations, and this approach leads to problems and frustrations:

1. Mature implementations may – theoretically – be in breach of the
   specifications themselves.
2. Mature implementations assume they're interacting with fully-fledged
   counterparts, and may error if certain behaviours in the developing
   implementation are not present, potentially raising red herrings.
3. The above makes incremental development (piece-by-piece) of upcoming
   implementations is hard.
4. Debugging issues can be hard due to the many moving parts of a typical
   libp2p implementation.

We envision the libp2p Conformance Test Kit (CTK) as a suite of tests that are
minimally dependent on existing libp2p libraries. They mainly perform raw
byte-level I/O operations, to test the mechanics of the foundational
components and processes of the libp2p stack, namely: connection
bootstrapping, multiplexing, stream management, protocol negotiation,
encryption. Application and base protocols are excluded from the CTK.

The CTK will serve as an _executable spec_, in a vein similar to [ETH2's
approach](https://github.com/ethereum/eth2.0-specs/tree/dev/test_libs/pyspec).

By subjecting all implementations to the CTK, authors are assured that their
work is compliant with the libp2p specs, and the chances of successful
interoperability are dramatically increased.

# Value

## Benefits (if addressed)

1. libp2p implementations can be developed incrementally.
2. Low-level mechanics of the libp2p specifications are captured in an
   authoritative, vetted, executable spec.
3. Discrepancies across implementations can be debated objectively, using the
   CTK as an authoritative input.
4. Changes to the libp2p spec will translate to changes in the CTK, which in
   turn will make non-conforming implementations fail, thus raising a flag.
5. By integrating the CTK into CI builds, maintainers can be alerted if code
   changes break compliance.

## Risks (if not addressed)

1. Uncertainty. Is my libp2p implementation compliant with the specs?
2. Development
2. The low-level mechanics of libp2p are captured only in English prose,
   subject to interpretation in some cases, leading to ambiguity and divergent
   understanding.

# Expected output and constraints

We expect the CTK to be developed in Golang, in its own repository, to be
later transferred to the the libp2p org on GitHub. It should compile down to a
single binary.

The CTK will comprise a battery of assertions, each identified by a unique
number. The codebase should be modular and well-architected. It should be
straightforward to add, remove and modify assertions.

A simple text-based control interface over TCP can be used to drive the CTK,
and switch between test cases. We expect the implementation to interact with
the CTK via this endpoint. Example test scenarios to develop:

* SecIO handshake success.
* SecIO handshake failing in the first message, or in the second message.
* SecIO handshake timeout.
* SecIO handshake with incorrect identity.
* SecIO incorrect keys derived.
* SecIO handshake success, no multiplexer agreement (several attempts).
* SecIO handshake success, second multiplexer agreed.
* SecIO handshake success, first multiplexer agreed.
* SecIO handshake success, multiplexer agreement times out.
* SecIO handshake success, garbage data.
* SecIO handshake success, mplex agreed.
* SecIO handshake success, mplex agreed, bad message follows.
* No secure channel agreement.
* etc.

# Relevant discussion

No significant discussion has occurred in the past, other than identifying the
need for a CTK here: https://github.com/libp2p/libp2p/issues/76.

# Design/implementation notes

<!-- Optional: if you have an idea in mind of how this would be accomplished,
write down your notes here. -->

* You should investigate how other conformance test suites operate. Examples
  include Java JSR TCKs.
* You should refrain from using existing go-libp2p libraries as much as
  possible. go-libp2p itself will be subjected to the CTK.
* You _can_ (and should) use encryption libraries such as go-libp2p-secio, but
  should refrain from using multiplexers as much as possible. For the types of
  tests this program will perform, fully fledged multiplexing should not be a
  requirement.

# Potential funders

ETHBerlinZwei community improvement pool, Protocol Labs, Ethereum Foundation.
