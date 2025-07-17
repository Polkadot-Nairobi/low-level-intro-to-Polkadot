# Nominated Proof-of-Stake (NPoS)

- Nominated Proof-of-Stake (NPoS) is Polkadot's specialized Proof-of-Stake mechanism, meticulously designed to ensure the network's security and stability.
- This mechanism aims to enhance decentralization, foster trust, and improve overall scalability.

## a. Roles: Validators, Nominators, Collators, Fishermen

- The NPoS system defines distinct roles, each contributing to the security and integrity of the Polkadot state machine:

  - **Validators**: These entities form the backbone of the Polkadot network. Their responsibilities include producing new blocks, validating the correctness of transactions, and securing the Relay Chain. Validators stake their own DOT tokens and are tasked with accepting and verifying specialized "state transition proofs" from collator nodes.

  - **Nominators**: These participants contribute to network security by delegating their DOT stake to chosen validators, effectively "backing" them. By bonding (locking) their DOT, nominators incentivize validators to correctly produce blocks, thereby enhancing overall network security. In return, nominators receive a proportional share of the rewards earned by the validators they support.

  - **Collators**: Collators maintain full nodes for both their specific parachain and the Relay Chain. Their primary function is to gather transactions originating from their respective parachains, execute these transactions, and then generate "state transition proofs" (Proof-of-Validity, or PoV) or "unsealed blocks" for submission to the Relay Chain validators. These proofs enable validators to verify and include the parachain's state changes into Polkadot's shared state. It is important to note that collators themselves do not provide security guarantees; rather, they rely on the Relay Chain's validators for this function.

  - **Fishermen**: These are specialized full nodes that continuously monitor the Relay Chain and other parts of the protocol to identify and report any malicious or incorrect behavior to the validator nodes. Unlike collators, fishermen do not package state transitions or produce parachain blocks; their role is purely supervisory. They stake a small amount of DOT and are significantly rewarded for successfully identifying and reporting malicious activity, acting as a crucial deterrent against misbehavior.

## b. Economic Security: Staking, Slashing, and Incentives

- The economic security of the Polkadot network is underpinned by a robust system of staking, slashing, and incentives.
- Validators are required to lock a significant amount of DOT on-chain.
- If a validator acts maliciously or fails to perform its duties correctly, a portion or all of its staked DOT can be "slashed".
- This mechanism imposes a substantial financial cost on any attempt to attack or disrupt the network.

- Nominators, by extension, also bear a financial risk; if the validators they have chosen are slashed, the nominators may lose a portion of their staked DOT as well.
- This shared risk creates a strong economic incentive for nominators to conduct thorough due diligence and carefully select trustworthy validators.
- The overall security of the network is directly correlated with the economic signal provided by the total amount of DOT bonded and staked by honest participants.
- A higher amount of staked DOT increases the minimum economic outlay an attacker would need to acquire a validator slot and compromise the network, thereby bolstering its resilience.
- NPoS, with its distinct roles and economic incentives, creates a robust, cryptoeconomically secured environment for the Relay Chain's state machine. The system ensures that the global state transitions are validated by a diverse and incentivized set of actors.

## c. Validator Election: The Phragmén Algorithm

- To select the active set of validators, Polkadot employs the **"sequential Phragmén"** method.
- This algorithm, which is typically computed off-chain for efficiency, is designed to elect validators based on a combination of their own self-staked DOT and the stake delegated to them by nominators.
- The Phragmén algorithm optimizes for three key metrics:
  - maximizing the total amount of stake securing the network
  - maximizing the stake behind the minimally staked validator (to ensure a high baseline of security for all active validators)
  - minimizing the variance of stake distribution across the validator set.
- This optimization for stake distribution directly contributes to decentralization and resilience against centralization attacks, ensuring that the global state transitions are validated by a diverse and incentivized set of actors, thereby maintaining the integrity of the Polkadot state machine.
