# TLS1.3 handshake implementation for js-libp2p

## Motivation and context

<!-- Describe what's the current situation, where this project fits in, where does this proposal emerge from, etc. -->

`js-libp2p` has been using [libp2p/js-libp2p-secio](https://github.com/libp2p/js-libp2p-secio) as the encryption protocol for connections. `secio` was implemented since there was no TLS 1.3 crypto channel available at the time, both in `go-libp2p` and `js-libp2p`.

In the meantime, a libp2p TLS handshake spec was created and `go-libp2p` got the `go-libp2p-tls` implementation, which uses TLS to set up the communication channel.

TLS1.3 support was added with node@11 and node@12 releases. The native node `tls` module provides an implementation of TLS and SSL protocols built on top of OpenSSL.

Relevant resources:
- [libp2p TLS handshake spec](https://github.com/libp2p/specs/blob/master/tls/tls.md)
- [libp2p/go-libp2p-tls](https://github.com/libp2p/go-libp2p-tls)
- [nodejs.org/api/tls](https://nodejs.org/api/tls.html)

## Value

<!-- Help the community understand the worth of carrying out this project, by filling out the benefits and risks subsections. Write any general comments here. -->

### Benefits (if addressed)

<!-- Describe how addressing this project would result in positive effects for the libp2p stack, community, implementers (people _building_ libp2p), downstream users (developers _using_ libp2p in their projects), etc. -->

There are several benefits from this implementation in `js-libp2p`, namely the use of an audited specification and implementation (TLS 1.3 from node) for connection encryption and ability to establish connections with `go-libp2p` nodes that do not use `secio`. With this implementation, we will be able to switch the connection encryption default protocol.

### Risks (if not addressed)

<!-- Describe what would be harmed, damaged or rendered inefficient if the community decides to discard this project (including possible worst case scenarios). -->

`js-libp2p` nodes will not be able to establish connections with `go-libp2p` nodes that only use TLS1.3 for the encryption of connections.

## Expected output and constraints

<!-- Describe what you'd expect to be delivered by whoever picks up this bounty. Specify any timeline or scope constraints (e.g. "this needs to be finished by end of October 2019 because...") -->

The implementation of the `js-libp2p-tls` module compatible with the `connEncryption` module for `js-libp2p`.

## Design/implementation notes

There is currently no interface for connection encryption. In order to easily plug into js-libp2p, the TLS implementation should follow the interface of Secio, https://github.com/libp2p/js-libp2p-secio/blob/v0.11.1/src/index.js.

**Note**: js-libp2p is moving away from pull stream usage to use async iterators instead, and is also moving away from callbacks. Ideally the TLS implementation should leverage async iterators, however, if this is a blocker the conversion from pull streams should be fairly straight forward.

## Potential funders

<!-- Optional: know of projects or organizations that would benefit from seeing this project come to fruition? Enumerate them here, supplying some context, and possibly mention the relevant people. -->

Protocol Labs.