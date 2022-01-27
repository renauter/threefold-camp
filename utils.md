## CosmWasm - GitPod

[link](https://medium.com/cosmwasm/cosmwasm-gitpod-f1b082994b7c)

## Terra Academy

https://academy.terra.money/courses/take/cosmwasm-smart-contracts-i/lessons/26696356-intro-to-cosmwasm

## Messages in CosmWasm

Before you view the Quick Start Contract Walkthrough, it's helpful to talk briefly about messages.
Cosmos blockchains operate by sending various kinds messages around.
Messages are sent from users to contracts, from contracts to contracts, and even from contracts to other blockchain.
Blockchain platforms are, after all, protocols for sending, processing, and logging authorized messages around.
Most of these messages are commands to do something, but some are just queries for information.

We'll see a lot of CosmosMsg messages in our contract work, including:

- BankMsg
- StakingMsg
- DistributionMsg
- IbcMsg
- WasmMsg
- GovMsg

`But the primary types of messages we need to worry about are the messages interacting with our smart contract.`

All smart contracts need to handle three kinds of incoming messages:

- InstantiateMsg: what happens when an instance of a smart contract is created (startup code)
- ExecuteMsg: the kinds of actions users can tell a smart contract to execute (write operations)
- QueryMsg: the kinds of queries for information users can send to a smart contract (read operations)

Incoming messages of these three types will be passed off to our contract's entry points: the instantiate(), execute(), and query() functions. These may be indicated in the template you pull with the macro attribute

> #[entry_point]

which you should now replace with:

> #[cfg_attr(not(feature = "library"), entry_point)]

All of our core code will be located in these three functions, or in functions called by these three functions.

