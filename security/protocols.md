Protocols
=====
Protocols are where cryptography meets system level creations. They allow us to formally describe adversarial engagement with a system. Generally, a protocol is a way to implement a policy. The procedures of odering wine at a fancy restaurant is an example of a security protocol that is designed to build trust on both sides.

## Notation
In an effort to formalize things, we will describe some notation for protocols.

Say we have two people, Alice and Bob. If Alice wants to send a message to Bob, we notate A -> B.
After a colon, the message follows. We then further define what each variable in the message means. By convention, *N* will be a nonce.

If T is a token to send, the message from Alice to Bob is A -> B: T

If the message is encrypted, we put it in curly braces '{}'. Then you subscript the key (notated in parenthesis in these notes).

If the above token was encrypted with key K, 
A -> B: {T}(K).

## Car Unlocking Protocols
Principles: Engine controller *E* and car key transponder *T*

Static:
    - T -> E: KT
    - this basically just flips the lock on and off

Interactive:
    - E -> T: N
    - T -> E: {T, N}(KT)

Note: The three kinds of nonces are a sequence, a random number, and a timestamp.

## Identify Friend or Foe (IFF)
Basic Idea: Fighter (F) challenges bomber (B)
    - F -> B: N
    - B -> F: {N}(K)

Fighter challenges unknown:
    - F -> U: N
    - U -> F: {N}(K)

Unknown reflects challenge to fighter's wingman:
    - F -> U: N
    - U -> W: N
    - W -> U: {N}(K)
    - U -> F: {N}(K)

## Two Factor Authentication
A server and a user (the user puts nonce into a keypad (P) and then adds a PIN):
    - S -> U: N
    - U -> P: N, PIN
    - P -> U: {N, PIN}(K)
    - U -> S: {N, PIN}(K)

## Key Sharing
Alice and Bob each share a key with Sam, and they want to communicate. (Kxy is the key shared between X and Y)
    - A -> S: A, B, Na
    - S -> A: {Na, B, Kab, {Kab, A}(Kbs)}(Kas) -- (The sub encrypted message will be sent to Bob who will forward it to Sam to validate)
    - A -> B: {Kab, A}(Kbs)
    - B -> A: {Nb}(Kab)
    - A -> B: {Nb +-1}(Kab) -- (to validate the key has been shared successfully)

How do you know that the key is new? How do you know the sharing didn't happen years ago? The way to enhance this algorithm is to build in the concept of time. You can add that in the response from Sam to Alice by including time and the length it'll be valid for.

### Kerberos
Is what implements this fix by uising a timestampped "ticket"
    - A -> S: A, B
    - S -> A: {Ts, L, Kab, B {Ts, L, Kab, A}(Kbs)}(Kas)
    - A -> B: {Ts, L, Kab, A}(Kbs), {A, Ta}(Kab)
    - B -> A: {Ta + 1}(Kab)