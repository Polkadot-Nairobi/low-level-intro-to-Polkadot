# Parachains as Specialized, Interoperable State Machines

## A. Heterogeneous Layer-1 Blockchains

- Parachains are defined as heterogeneous blockchain shards, operating as independent Layer-1 chains, each equipped with its own native tokens and optimized functionality tailored for specific use cases.
- These parachains are purpose-built and highly specialized, designed to efficiently execute complex logic that is precisely aligned with their intended function. This contrasts with general-purpose smart contract platforms that often struggle to optimize for diverse applications.

- Parachains can be configured as either public or private networks and possess the autonomy to define their own native tokens and governance processes.
- Fundamentally, parachains embody the concept of application-specific state machines. Their heterogeneous nature allows for the optimization of their state transition functions for distinct use cases, such as decentralized finance (DeFi), gaming, or identity management, thereby directly addressing the "one-size-fits-all" limitation prevalent in monolithic blockchain designs.
- This specialization is a powerful mechanism for enhancing scalability and flexibility within the broader Polkadot state machine network.

## B. Shared Security and Coretime Allocation by Connecting to the Relay Chain

- Parachains connect to the Polkadot Relay Chain primarily to benefit from its "shared security," also frequently referred to as "pooled security".
- This shared security model means that the robust validator set of the Polkadot Relay Chain is responsible for securing the state transitions of all connected parachains.
- A critical implication of this design is that if the Relay Chain were to revert for any reason, all connected parachains would also revert, thereby ensuring the persistence and integrity of the entire system.

- A key technical characteristic is that parachains do not operate their own Nominated Proof-of-Stake (NPoS) mechanisms or independent consensus algorithms that provide their own finality.
- Instead, they inherently rely on the Relay Chain for the finalization of their blocks.
- While parachains retain control over how and by whom their blocks are authored (via collators), they cede the ultimate finality mechanism to the Relay Chain. This creates a deeply interconnected and globally consistent state machine network.

- Parachains acquire their connection to the Relay Chain by purchasing "coretime" using DOT tokens
- This can be achieved either by renting a dedicated slot for continuous connectivity, typically through an auction model, or on a more flexible "pay-as-you-go" basis.
- The shared security model presents a huge trade-off: parachains gain robust security from day one without having to bootstrap their own validator sets, but in return, they cede their finality mechanism to the Relay Chain. This ensures global consistency across the network of state machines.
