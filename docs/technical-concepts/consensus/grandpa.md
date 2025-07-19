# GRANDPA: GHOST-based Recursive Ancestor Deriving Prefix Agreement (Provable Finality)

- GRANDPA (GHOST-based Recursive Ancestor Deriving Prefix Agreement) is Polkadot's finality mechanism for the Relay Chain, operating independently and in parallel to the block production process.
- Its primary function is to deterministically select the canonical chain and definitively decide which set of changes to the blockchain state is final and irreversible.

- GRANDPA can function effectively as long as two-thirds of the participating nodes behave honestly, and it is resilient to asynchronous network conditions, tolerating up to one-fifth of Byzantine (malicious) nodes.
- Unlike many other Byzantine Fault Tolerant (BFT) algorithms that vote on individual blocks, GRANDPA validators vote on chains.
- When a supermajority (specifically, two-thirds) of validators collectively attest to a chain containing a particular block, all blocks leading up to that block are finalized simultaneously.
- This "chain-based finalization" significantly streamlines the finalization process, allowing for near-instant finality under optimal network conditions and the theoretical ability to finalize millions of blocks simultaneously once network issues are resolved.

- GRANDPA provides "provable finality," meaning that once a block is finalized by GRANDPA, it is irreversible and cannot be reverted.
- Furthermore, it incorporates a feature called "accountable safety," which holds validators accountable for any safety violations, such as finalizing two conflicting chains.
- In such an event, the system can identify the misbehaving validators, who would then face severe penalties.
- GRANDPA provides the absolute guarantee of state finality for the Relay Chain.
- By voting on chains and finalizing multiple blocks simultaneously, it offers high-throughput finality, which is crucial for coordinating the state transitions of numerous parachains.
- The "provable finality" and "accountable safety" mechanisms are critical for the security and trustlessness of Polkadot's global state machine
