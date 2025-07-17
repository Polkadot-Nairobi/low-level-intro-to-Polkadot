# BABE: Blind Assignment for Blockchain Extension (Block Authoring)

- BABE (Blind Assignment for Blockchain Extension) is the mechanism responsible for producing new blocks on the Polkadot network.
- It operates among validator nodes to determine which validator is assigned the right to create a new block.
- BABE allocates block production slots to validators based on the amount of DOT they have staked and a randomness cycle, drawing similarities to the **Ouroboros Praos consensus algorithm**.
- Validators participate in a lottery for each slot, which occurs in sequential, non-overlapping phases known as "epochs," with each epoch divided into fixed-length "slots" (approximately 6 seconds per slot).

- BABE is designed to handle various network conditions, including scenarios where multiple validators might win the lottery for the same slot (resulting in temporary forks) or where no validator wins a slot (empty slots).
- In such cases, a secondary selection algorithm ensures that a block is still produced, thereby guaranteeing continuous block production and network liveness.
- BABE's role is to continuously propose new states (blocks) for the Relay Chain's state machine.
- Its randomness-based slot assignment and robust handling of multiple or empty slots ensure a decentralized and resilient probabilistic finality for block production, optimizing for speed and liveness
