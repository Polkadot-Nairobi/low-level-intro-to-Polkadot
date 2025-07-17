# Consensus Mechanisms

- Polkadot employs a "hybrid consensus model" that distinctly separates the process of block production from block finality.
- This architectural choice is a deliberate optimization for efficiency, allowing for rapid block production while a separate, potentially slower, finality agent operates independently, thereby preventing interference with transaction execution times.

## The Fork Choice Rule and Separation of Concerns

- The Relay Chain's fork choice rule elegantly combines the functions of BABE and GRANDPA.
- BABE is strictly required to build new blocks only on the chain that GRANDPA has already finalized.
- In instances where forks occur after the last finalized block, BABE employs a rule to build on the chain that contains the most "primary" blocks, thereby providing probabilistic finality until GRANDPA can achieve provable finality.

- This hybrid consensus model bestows upon the Polkadot network the advantages of both probabilistic finality (ensuring continuous and accurate new block production) and provable finality (providing universal agreement with no chance of reversion).
- This design represents a sophisticated optimization for blockchain state machines.
- By separating block production from finality, Polkadot achieves both high throughput (via BABE's rapid block production) and strong security guarantees (via GRANDPA's irreversibility).
- This architectural choice mitigates common issues observed in other blockchain designs, such as chain stalling or the risk of unknowingly following an incorrect fork, allowing the network to maintain liveness while ensuring the integrity of its global state.
- This is a critical enabler for a robust multi-chain architecture.

| Protocol Name | Primary Function | Mechanism                                                                     | Key Properties                                                                    | Finality Type | Impact on State Transitions                                             |
|---------------|------------------|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| BABE          | Block Production | Randomness-based lottery for slot assignment to validators                    | Continuous block production, handles forks and empty slots                        | Probabilistic | Proposes new potential states for the Relay Chain                       |
| GRANDPA       | Block Finality   | Validators vote on chains (not blocks); supermajority finalizes entire chains | Provable finality, irreversible, accountable safety, high-throughput finalization | Provable      | Confirms and irreversibly commits state transitions to the Relay Chain. |
|               |                  |                                                                               |                                                                                   |               |                                                                         |
