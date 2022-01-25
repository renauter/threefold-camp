

## Cosmos SDK

The Cosmos SDK is written in Golang based on certain design considerations to allow for the customization of modules, however, expanding across many programming languages is crucial to growing developer adoption. Ultimately supporting the greater goal of enabling an Internet of Blockchains — or The Interchain — to support a plethora of implementations and capabilities connected by the Inter-Blockchain Communication Protocol (IBC)

## IBC

IBC = INTER-BLOCKCHAIN COMMUNICATION PROTOCOL

<p align="center">
  <img width="800" src="/img/IBC.jpg">
</p>

Source [here](https://ibcprotocol.org/).

## Smart Contract

Smart Contract = piece of computer program that gets executed by a quorum of blockchain nodes independently in order to record the latest program state

The main purpose of smart contracts is to maintain program states. State is an arbitrary piece of data that gets updated by executing a transaction. In this sense, a blockchain can be conceptualized as a database, although it’s designed to lean heavily toward data consistency and immutability, at the cost of speed and query support. Almost all blockchain protocols are designed to follow a state transfer conceptual model.

Each smart contract maintains its own set of states. Most transactions submitted to a blockchain target a smart contract, with the exception of pure value transfers that do not involve smart contracts. Once a transaction is executed, the target smart contract updates its state. A smart contract can call another smart contract, in order to query the downstream contract’s state or update it.

<p align="center">
  <img width="600" src="/img/Blockchain-Smart-Contract.jpg">
</p>

## Anatomy of a Smart Contract

Execution of smart contracts often results in updated states

The logic inside smart contracts will determine if a transaction is valid or not. Examples of an invalid transaction may include not operating on the right level of beginning state, such as attempting to spend tokens without having sufficient balance. Only valid transactions result in updated states. Invalid transactions are either rejected by the network from being included in the blockchain, or included but marked as failed, depending on different blockchain designs.

Smart contracts may also publish events as a way to inform the outside world. Event listeners are notified when the block containing the transaction gets committed to the blockchain on the node.

<p align="center">
  <img width="600" src="/img/Smart-Contract_Explained_1.jpg">
</p>

A smart contract may have more than one public function that can be invoked by a transaction. Each function may either cause the state to be updated or simply returns the latest state. For example, a standard fungible token smart contract typically has the following functions useful in scenarios such as payments and commodity trading:

Functions that update states (require transactions to invoke):
transfer(to, amount)
approve(delegate, amount)
transferFrom(from, to, amount)
mint(to, amount)
burn(from, amount)

Functions that query the latest states (do not require transactions to invoke):
balanceOf(account)

If the state needs to be updated, it must be done via a transaction and be processed through the full transaction cycle. Due to the decentralized nature of blockchain architecture, transactions must be handled by a consensus mechanism, so that the system ensures all the copies maintained by the blockchain network’s participating nodes have identical records.

> Updating state requires transaction processing with consensus from the whole network

<p align="center">
  <img width="600" src="/img/Smart-Contract_Explained_2.jpg">
</p>

On the other hand, querying for the latest state without updating it can be accomplished much faster and involves only a single node in the network.
Any node that has the smart contract installed locally can execute the query request and return the result by reading from the locally maintained state database.

> Querying smart contracts for latest state can be accomplished with a single node

<p align="center">
  <img width="600" src="/img/Smart-Contract_Explained_3.jpg">
</p>

## Smart Contract Life Cycle

Before a smart contract can process transactions, it must be first deployed on the blockchain.
The deploy process must guarantee that all blockchain nodes have exactly the same code.
Different blockchain designs handles this requirement differently, but there are in general two approaches:
- save the contract code itself in the blockchain which guarantees global consensus (on-chain), 
- or let each node owner decide if the node should have the code installed locally, and use a hash-based commitment in the blockchain as reference for validating the code integrity (off-chain).

<p align="center">
  <img width="600" src="/img/Smart-Contract_Explained_4.jpg">
</p>

1) Hyperledger Fabric requires an elaborate administration scheme to first install the chaincode onto a blockchain node, and instantiate it globally in the chain via a special type of transaction. Because of the Fabric’s unique consensus framework design, only a selective subset of node, called endorsers, need to have the chaincode installed. Details of this design is beyond the scope of this book, but you can think of it as committee based governing rather than popular votes. Once a chaincode has been instantiated, there is a chain-wide common view to which vote should be executed when that chaincode is called. As a result, execution of the chaincode is guaranteed to be consistent on every endorser node.

2) Enterprise Ethereum, with the public Ethereum inheritage, offers a simple one-step process to deploy smart contracts. The deployment is done via a transaction, making it a chain-wide operation by nature. Code for the smart contract is saved on-chain as state. As a result, all nodes are guaranteed to have access to the code and they all have the same version.

3) Corda adopts a peer-to-peer transaction coordination architecture, without utilizing a globally maintain common ledger of transactions. Because of this, smart contract deployment are done on a per-node basis based on the need to perform bi-lateral or multi-lateral transactions. Similar to Fabric, the administrator of the Corda node is responsible for ensuring that the smart contract required to process a transaction has been installed on the node.

Source [here](https://www.kaleido.io/blockchain-blog/what-are-smart-contracts-and-how-do-they-work).

## CosmWasm

CosmWasm, a project enabling WebAssembly (WASM) virtual machines (VMs) in the Cosmos SDK

Wasm = WebAssembly is a binary instruction format for a stack-based virtual machine. 
Wasm is designed as a portable compilation target for programming languages, enabling deployment on the web for client and server applications.

Multi-Chain Contracts = Different Chain, Same Contract

CosmWasm is designed and built from the ground-up to be a multi-chain solution for smart contracts.
As it comes from the Cosmos ecosystem, it is designed for networks of blockchains, rather than siloed chains.


