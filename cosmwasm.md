

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

## General considerations for Smart Contracts

Implications of determinism = Every input into the blockchain must result in an expected output, or the execution of code is not verifiable by the network. This means that a smart contract cannot:

- generate a random number by itself
- get outside information (other than information from connected oracles)

Your application design should bear these in mind. Randomness is achievable by using various non-trivial techniques, but pseudo-randomness, though tempting, should be avoided as it can be gamed.

You should also remember that economy is an important goal.
Use smart contracts sparingly!
The best smart contracts do `simple things`.

Using your smart contract to store absolutely everything – such as whether users prefer light or dark mode for your interface – is not ideal.
It will result in slower and more expensive experiences for your users.
Instead, only use your smart contract for the things which need the guarantees smart contracts offer, such as:

- immutability
- seizure resistance
- censorship resistance
- auditability

Handle aspects which do not require these things elsewhere: for example, storing user preferences and avatars or temporary data for a user session should generally be handled by off-chain storage.
This storage can still be decentralized or attack-resistant to some degree (by using IPFS, for example), but is inappropriate for smart contracts.

Your contract cannot be used to do very intense computation – all computation has a hard limit. It has to fit in a block time, after all. If you need intense computation in your app, investigate ways to handle this elsewhere. Depending on your particular app, perhaps the computation can still be performed in a verifiable way.

## CosmWasm

CosmWasm, a project enabling WebAssembly (WASM) virtual machines (VMs) in the Cosmos SDK

Wasm = WebAssembly is a binary instruction format for a stack-based virtual machine. 
Wasm is designed as a portable compilation target for programming languages, enabling deployment on the web for client and server applications.

Multi-Chain Contracts = Different Chain, Same Contract

CosmWasm is designed and built from the ground-up to be a multi-chain solution for smart contracts.
As it comes from the Cosmos ecosystem, it is designed for networks of blockchains, rather than siloed chains.

Source [here](https://docs.cosmwasm.com/docs/1.0/).

CosmWasm = The Smart Contract Platform for Cosmos

Before CosmWasm, if you had to run logic on Cosmos SDK platform, you’d have to depend upon using GoLang to make changes to the source code. CosmWasm is a module you can now plug onto your present ecosystem, and write code in a bunch of languages and deploy it to your network. This is done via Web Assembly. You can read more about Web Assembly here. We will be using Rust in our series.

CosmWasm allows multi-chain contracts to be built. It is pretty easy to integrate since it has little requirements on host.

This allows CosmWasm to run agnostic of the chain it is running on. Multi-chain contracts also means we would have interblockchain contracts. This is an IBC-first design, allowing the developer to write code for one chain, but running it on another chain for certain processes.

Contracts are different from Modules in Cosmos. You can upload and edit contracts to the chain.

Source [here](https://hackmd.io/@abhinavmir/cosmwasm1).

## Terra

https://docs.terra.money/docs/develop/how-to/localterra/README.html
To have a local Terra tesnet

> git clone https://github.com/terra-project/localterra
> cd localterra
> docker-compose up

## Terrain

make sure Rust setup is OK:

> rustup default stable

make sure we added the wasm target:

> rustup target add wasm32-unknown-unknown

install cargo-generate:

> cargo install cargo-generate --features vendored-openssl

install cargo-run-script (needed to run contract code optimizer):

> cargo install cargo-run-script

Recommended to isntall nvm
If you need Node Version Manager first to enable the nvm and npm commands, go to https://github.com/nvm-sh/nvm.
Node.js = an open-source, cross-platform, back-end JavaScript runtime environment that runs on the V8 engine and executes JavaScript code outside a web browser. 
The install command depends on the version you'd like to install; as of this video, it is:

> curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

Close and reopen your terminal to start using nvm or run the following to use it now:

> export NVM_DIR="$HOME/.nvm"
> [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
> [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

Use a certain version of Node.js (here 16):

> nvm install 16

or if already installed

> nvm use 16

Terrain = Framework that makes testing and deploying smart contracts easier locally, on testnet, and on mainnet.
Terrain is at https://github.com/iboss-ptk/terrain.
The command shown is to install Terrain package globaly (-g):

> npm install -g @iboss/terrain

Now able to create an app using Terrain

> terrain new raffle-dapp
> cd raffle-dapp

To make sure all my dependencies of my directory are installed:

> npm install

Now we have Terrain set up and ready to deploy our app and view/edit the template counter code with VS:

> code .

Make sure local Terra is running before deplying counter contract using:

> terrain deploy counter --signer validator

How to interact with the contract thanks to helpers in the lib/index.js file.
First we need to run Terrain console:

> terrain console

And then interact:

> await lib.increment()
> await lib.getCount()

Now let's deploy the Terrain React Frontend!
I need to synchronize because my frontend need to with which contract it is talking to:

> terrain sync-refs
> cd frontend
> npm install
> npm start

And it will open browser at http://localhost:3000/

Deploy on Terra tesnet:
- Go to wallet chrome extension chrome-extension://aiifbnbfobpmeekipheeijimdpnlpgpp/index.html#/wallet
- Get 1000 Luna https://faucet.terra.money/

> terrain console

check account address to be the same as wallet
custom_tester_1 comes from keys.terrain.js file

> wallets.custom_tester_1.key.accAddress

check the account balance:

> (await client.bank.balance(wallets.custom_tester_1.key.accAddress))[0]
> (await client.bank.balance(wallets.custom_tester_1.key.accAddress))[1]

should show what is on local Terra
Let's go to testnet now!
see network config on config.terrain.json file

> terrain console --network testnet
> (await client.bank.balance(wallets.custom_tester_1.key.accAddress))[0]

now you should see what is on wallet

> terrain deploy counter --signer custom_tester_1 --network testnet

to have a look to what happens go to https://finder.terra.money/ (or another block explorer) and look for the contract address
The contract address is given after deploying is successful 
Another block explorer https://finder.extraterrestrial.money/

