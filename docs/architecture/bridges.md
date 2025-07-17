# Connecting Polkadot to External Blockchains using Bridges

- Bridges are essential infrastructure that facilitate cross-chain communication between different networks, such as Polkadot and Ethereum.
- They allow these chains to recognize and trust each other's finalized states, which enables various applications like asset swaps and chain migrations.

## Purpose of Bridging

- Bridges enable Polkadot to communicate with external blockchains like Bitcoin and Ethereum.
- Within the Polkadot ecosystem, chains already benefit from secure interoperability through its native interoperability technology, which allows parachains to communicate trustlessly.
- Bridge designs vary from centralized and trusted to more decentralized and trustless, with Polkadot favoring the latter for its ecosystem.

## Trustless Bridges

- A two-way trustless bridge between two chains (A and B) can be conceptualized as two one-way bridges (A → B and B → A).
- A trustless bridge always consists of both on-chain and off-chain components.
- Trustlessness implies that users only need to rely on mathematics, code, cryptography, and protocol, rather than trusting specific individuals or organizations.
- While a completely trustless setup is not always guaranteed, basic assumptions are necessary when defining such a system.

### On-chain Bridge Components

Trustless bridges can be built using the following on-chain components, listed by suggested methodology:

- **Bridge Pallets**: These are used for Substrate-native chains, such as the Kusama <-> Polkadot bridge, as both networks' parachains utilize Substrate.
A GRANDPA light client of the source chain, built into the target chain's runtime, provides a "source of truth" about the source chain's finality. For example, Bridge Hub runs an on-chain light client of Kusama to infer the finality of transactions on Kusama and its parachains. Receiving messages on Polkadot from an external, non-parachain blockchain is possible via a Substrate pallet, which can then be deployed to Polkadot as a system-level parachain or a community-operated parachain.

- **Smart Contracts**: For chains not based on Substrate (e.g., Ethereum), smart contracts are deployed on the non-Substrate chain to facilitate bridging. For instance, Snowbridge uses the Polkadot Bridge Hub to run an on-chain light client of Ethereum to infer the finality of transactions on the Ethereum chain. While running a GRANDPA light client through smart contracts on Ethereum is possible, it is expensive. The BEEFY consensus layer, built on top of GRANDPA, offers a cost-effective solution for operating a trustless bridge with Ethereum and other protocols. Trustless bridges to chains like Cosmos, Avalanche, and NEAR would require custom pallets to be deployed on Bridge Hub.

- **Higher-Order Protocols**: These protocols, such as XClaim, should be used only when other options are unavailable. XClaim, for example, requires any swappable asset to be backed by collateral of higher value, which adds overhead. Bitcoin, which does not support smart contracts and is not Substrate-based, is an example of a network well-suited for higher-order protocols.

  - **Bitcoin Bridge (XCLAIM <-> Substrate <-> Polkadot)**: The Interlay team has developed a specification for a Bitcoin bridge based on the XCLAIM design paper, enabling a two-way bridge between Polkadot and Bitcoin. This allows BTC holders to issue iBTC on Polkadot and iBTC holders to redeem BTC on the Bitcoin chain. The Bitcoin bridge consists of two logically distinct components: the XCLAIM component, which manages iBTC accounts, and the BTC-Relay, which verifies Bitcoin state upon new transaction submission.

- On-chain bridge components are modules (pallets or smart contracts) deployed on a chain's runtime.
- Modules that track the finality of the source chain must be deployed on the target chain, while cross-chain messaging modules need to be deployed on both source and target chains.
- These components are also responsible for queuing messages at the source chain and receiving message proofs at the target chain. Messages are sent through specific lanes, ensuring they are received in the same order they were sent.
- On Bridge Hub, messages are in XCM format and dispatched by an XCM executor.

### Offchain Bridge Components

- Offchain bridge components are separate processes called relayers.
- Relayers are connected to both the source and target chain nodes.
- For chains using GRANDPA consensus, the relayer's task is to submit source chain GRANDPA justifications and their corresponding headers to the Bridge GRANDPA Finality Pallet on the target chain.
- This involves the relayer subscribing to the source chain's GRANDPA justifications stream and submitting each new justification to the target chain's GRANDPA light client.
- Messages between chains are relayed through these relayers, involving message delivery and delivery confirmation.

### Bridge Comparison (Snowbridge vs. Hyperbridge)

- Snowbridge and Hyperbridge are two trustless bridges connecting Polkadot with other ecosystems.
- It's important to note that tokens sent through different bridges are distinct; unless specific logic is implemented, WETH sent via Snowbridge cannot be sent back using Hyperbridge, and vice versa, which could lead to loss of funds

| Feature | Snowbridge | Hyperbridge |
| :------ | :--------: | :---------: |
| Purpose | General-purpose bridge for Ethereum & ERC20 assets, supports cross-chain smart contracts | Interoperability coprocessor, provides "Full Node Security" in cross-chain bridges |
| Mechanism | Uses Polkadot Bridge Hub to run on-chain light client of Ethereum | Leverages BEEFY consensus proofs, ISMP (Interoperable State Machine Protocol), PLONK verifier, Barretenberg backend |
| Key Functionality | Transfers Ethereum, ERC20 assets, arbitrary data | Facilitates POST requests (send data) and GET requests (read storage via state proofs) across chains |
| Security | Trustless, confirms funds on origin chain without centralized third parties | Detects and prevents Byzantine behaviors across connected chains by distributing validation workload |
| Cost Efficiency | BEEFY consensus layer provides cost-effective solution for trustless bridging with Ethereum | Leverages cost-effective consensus proofs |
