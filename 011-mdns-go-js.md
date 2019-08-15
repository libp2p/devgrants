# Implement MDNS discovery in Go and JS per the new spec

## Motivation and context

Issue: https://github.com/libp2p/go-libp2p/issues/623
Spec: https://github.com/libp2p/specs/blob/master/discovery/mdns.md

The current MDNS discovery mechanism implemented in go:

1. Does not conform to the above MDNS spec.
2. Does not support transports other than TCP (due to limitations of the current protocol).
3. Is filled with race conditions and other bugs (see the linked issue above) due to issues with the underlying MDNS implementation.

## Value

### Benefits (if addressed)

The value is just a mirror of the motivation:

* Replacing the underlying MDNS library (note: not with https://github.com/grandcat/zeroconf, that library doesn't fix the relevant bugs) will fix some data races (the only known data races in go-libp2p).
* Implementing the new protocol will improve interop between go-libp2p (which only implements the old, outdated protocol) and rust-libp2p (which only implements the new protocol).
* Implementing the new protocol will add support for discovering QUIC addresses (the current protocol only supports TCP).

### Risks (if not addressed)

* go/rust libp2p interop on local networks isn't complete.
* go-libp2p has a serious race condition when MDNS is enabled and can't be run with the race detector enabled.

## Expected output and constraints

The module must:

* Not trigger the race detector.
* Implement the new spec.
* Interoperate with js-libp2p and rust-libp2p.

Non-issues:

* The module _does not_ have to work with the current go-libp2p MDNS implementation. We can just pull in multiple modules for a transition period.

## Design/implementation notes

## Potential funders

<!-- Optional: know of projects or organizations that would benefit from seeing this project come to fruition? Enumerate them here, supplying some context, and possibly mention the relevant people. -->

ETHBerlinZwei, Protocol Labs.