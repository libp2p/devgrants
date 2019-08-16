# Wireshark Lua dissectors for libp2p

## Motivation and context

Sniffing network packets is an effective method to (a) debug esoteric
problems, (b) learn how a protocol works at the network level, (c) complement
protocol engineering/development/optimisation efforts.

Wireshark is a widely popular tool for network packet analysis. Wireshark
relies on pluggable, layered protocol dissectors to interpret captured packets
according to a set of heuristics. Dissectors decode packets and populate a
data tree, which is then available for filtering, searching, following,
tagging, etc.

libp2p protocols can be grouped in four categories; eventually we'd like to
have dissectors for all:

1. encryption channels
2. multiplexers
3. basic protocols (e.g. identify, multiselect, etc.)
4. application protocols (e.g. DHT, gossipsub, or user-defined protocols)

libp2p traffic runs atop transports like TCP, QUIC, Bluetooth, WebSockets,
WebRTC. Wireshark [bundles] out-of-the-box dissectors for all those.

## Value

<!-- Help the community understand the worth of carrying out this project, by
filling out the benefits and risks subsections. Write any general comments
here. -->

### Benefits (if addressed)

<!-- Describe how addressing this project would result in positive effects for
the libp2p stack, community, implementers (people _building_ libp2p),
downstream users (developers _using_ libp2p in their projects), etc. -->

libp2p Wireshark dissectors will enable easier, scientific debugging of
network behaviour, by taking the guesswork out. For hackers learning libp2p,
inspecting what happens on the wire is the ultimate approach to understanding
how libp2p operates.

Network captures are very useful in the context of protocol optimisation
effors, where sharing decoded dumps for collaboration, debugging, identifying
bottlenecks, excessive chunking, etc. is valuable.

Eventually we'd like to contribute these dissectors to the Wireshark repo so
that they're bundled out-of-the-box with Wireshark installations. Doing so
will also spread awareness about the existence and maturity of libp2p amongst
the network specialists communities out there.

Ultimately we expect these dissectors to be instrumental to the day-to-day
work of libp2p implementers and engineers, allowing us to x-ray how the
changes we make impact the wire.

### Risks (if not addressed)

<!-- Describe what would be harmed, damaged or rendered inefficient if the
community decides to discard this project (including possible worst case
scenarios). -->

The main risks of not accomplishing this work revolve around network traffic
staying opaque and the loss of line of sight once bytes leave the code and are
relayed to the kernel for I/O. Debugging weird behaviour may remain painful,
and how libp2p truly operates on the wire, a mystery.

## Expected output and constraints

<!-- Describe what you'd expect to be delivered by whoever picks up this
bounty. Specify any timeline or scope constraints (e.g. "this needs to be
finished by end of October 2019 because...") -->

An initial set of dissectors/plugins that users can seamlessly attach to a
running Wireshark installation. You should at least deliver dissectors for
these protocols:

* SecIO.
* Yamux.
* Kad DHT.
* Identify.

As denoted in the project title, the code must be in Lua, and it should follow
the design/implementation notes below.

To be licensed under the [Permissive License Stack].

## Relevant discussion

<!-- If there has been past discussion about this project, provide pointers.
Plus points if you synthesize the gist. -->

There have been previous efforts to implement [libp2p dissectors in C],
however that repo is abandoned, and most important, it lacks decryption
capability, so it's not as helpful in production or typical testing scenarios.

See this issue for some discussion: [Wireshark modules for all layers], and
this other one about decryption: [SecIO: dumping symmetric keys].

## Design/implementation notes

<!-- Optional: if you have an idea in mind of how this would be accomplished,
write down your notes here. -->

libp2p encapsulates protocols. For example, a DHT message would be
encapsulated within a multiplexer frame (e.g. Yamux, mplex, native QUIC,
etc.), which in turn would be encrypted and authenticated by the secure
channel (e.g. SecIO, Noise, TLS 1.3).

The heart of the Wireshark's decoding engine is this approach of iterative
decoding. The work performed in this devgrant should fully leverage this
aspect by adopting a modular design, such that new libp2p protocols can be
easily added at a later time.

In previous attempts, the main road block had been decryption. You should fork
go-libp2p-secio (and eventually go-libp2p-tls and go-libp2p-noise) and
introduce a flag for dumping secret keys on a keylog file that is followed by
the Wireshark plugin to acquire the secrets to decrypt network traffic.

We prefer Lua over native C dissectors because the APIs are at parity, and
based on our personal experience, adding Lua-based dissectors and plugins to
an existing Wireshark installation is a piece of cake, compared to trying to
attach a native dissector, which requires a custom build of Wireshark.

Apparently, the Wireshark community also encourages building third-party/user
plugins in Lua.

## Potential funders

<!-- Optional: know of projects or organizations that would benefit from
seeing this project come to fruition? Enumerate them here, supplying some
context, and possibly mention the relevant people. -->

* Protocol Labs.
* ETHBerlinZwei community bounty pool.

[bundles]: https://www.wireshark.org/docs/dfref/
[libp2p dissectors in C]: https://github.com/mkg20001/libp2p-dissector
[SecIO: dumping symmetric keys]: https://github.com/libp2p/specs/issues/46
[Wireshark modules for all layers]: https://github.com/libp2p/libp2p/issues/13
[Permissive License Stack]: https://protocol.ai/blog/announcing-the-permissive-license-stack/