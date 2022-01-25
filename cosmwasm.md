

## Cosmos SDK

The Cosmos SDK is written in Golang based on certain design considerations to allow for the customization of modules, however, expanding across many programming languages is crucial to growing developer adoption. Ultimately supporting the greater goal of enabling an Internet of Blockchains — or The Interchain — to support a plethora of implementations and capabilities connected by the Inter-Blockchain Communication Protocol (IBC)

## IBC

IBC = INTER-BLOCKCHAIN COMMUNICATION PROTOCOL

https://ibcprotocol.org/

![IBC](/img/IBC.jpg)

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

<p align="center">
  <img width="600" src="/img/Smart-Contract_Explained_2.jpg">
</p>

<p align="center">
  <img width="600" src="/img/Smart-Contract_Explained_3.jpg">
</p>


## CosmWasm

CosmWasm, a project enabling WebAssembly (WASM) virtual machines (VMs) in the Cosmos SDK

Wasm = Web Assembly

Multi-Chain Contracts = Different Chain, Same Contract

CosmWasm is designed and built from the ground-up to be a multi-chain solution for smart contracts.
As it comes from the Cosmos ecosystem, it is designed for networks of blockchains, rather than siloed chains.


