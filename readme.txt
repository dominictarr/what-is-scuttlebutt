
    What is scuttlebutt?

Status of this memo

  draft spec

Abstract

  The goal of this document is to specify what it means to say you have
  implemented "scuttlebutt". Because scuttlebutt is intended as an living,
  changing protocol, this is necessarily in terms of other implementations.
  That is, you have implemented scuttlebutt if you can communicate with other scuttlebutt
  implementations.

Definition of terms

  1. Protocol Layer.
    Signing format.
    Transport format.

  2. Platform Layer.
    Content format.

  3. Application Layer.


Defining interoperability.

  To say that Alice and Bob both speak scuttlebutt, it MUST be true that
  a message created in one implementation can be transferred to, validated,
  and rendered (in the application layer of) another implementation. This MUST
  apply in both directions.

  Although both implementations may store the message, it is not required
  that their database formats be mutually intelligible.

  If we consider 3 implementations, the situation is more complicated.
  If Carol implements a new transport format, and Bob also supports it,
  Bob is doing scuttlebutt because he can mutually exchange messages with Alice,
  who is defined as the source of scuttlebutt. If Carol supports the old format
  but chooses to use the new transport format when communicating with bob, that is still
  scuttlebutt. If Carol discontinues the old format, she can still receive Alice's
  messages via Bob, so that is still scuttlebutt. If Bob also discontinues the old format,
  then they have broken scuttlebutt because they cannot receive Alice's messages.
  However if Alice also supports the new transport format, then scuttlebutt is still happening.

  If Carol introduces a new signing format there is a greater risk of breaking scuttlebutt.
  For that signing format to be considered scuttlebutt, it must be accepted by other
  scuttlebutt peers. As long as there is one format that all peers can mutually produce
  and consume, then scuttlebutt is still happening.

  A particular format may be consumed but not produced by other peers. It's not required
  that Alice and Bob can both produce the same type of messages, just that Alice and Bob
  can consume each other's messages.

  There is also the possibility of transports that can only move old messages, such as by
  the message hash. Of course, there needs to exist some other transport that can move new messages.
  The main transport protocol does this by requesting new messages signed by a particular public key.
  If Bob supports the new signing format, he can create new format messages that reference
  old format messages, from Alice. And then Carol can request Alice's old-format messages by hash
  references in Bob's messages. If Alice upgrades to the new signing format and stops producing
  old format messages, then it's still scuttlebutt even if the peers no longer have the ability
  to replicate or produce new old-format messages. As long as there is some way to still aquire
  and understand the old messages.

  For example, due to many quirks in the old format, it's not desirable to force new implementors
  to implement it. But to minimally support it, they may transport it in a few format, store
  it in a new format, and convert it into the old format for signing and hashing. The new format
  must just retain sufficient context for it to be possible to convert to the old signing format.

  Alice and Bob's scuttlebutt implementations must be sufficiently compatibile, but
  this does not mean they need to be identicle. Alice may store her messages in a different
  database format to Bob. Database formats MAY be mutually intelligible, but it is not required.
