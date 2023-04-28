# Tofuri

**Abstract.** In order to meet the increasing demands of the future, it is necessary to develop a lightweight cryptocurrency that can process thousands of transactions per second (tps). This can be achieved by reducing the size of transactions, which in turn increases the network's throughput. Additionally, reducing the size of the blockchain makes it more accessible to devices with limited resources, thereby lowering the entry barrier for new participants.

## 1. Introduction

As of writing Bitcoin has a limit of 7 tps. There is consistently a demand to make more than 7 tps which results in full blocks which in turn leads to increased transaction fees.

Energy is a finite resource. Proof-of-work is an energy intensive task. A way to achieve consensus amongst a decentralized network without wasting as much electricity would improve upon the already existing proof-of-work model.

## 2. Proof-of-Stake

Proof of Stake (PoS) is a consensus algorithm used in blockchain networks to validate transactions and create new blocks. Unlike the Proof of Work (PoW) algorithm, which requires miners to solve complex mathematical problems to add new blocks to the blockchain, PoS relies on participants called validators to secure the network and create new blocks.

In a Proof of Stake system, validators are selected to create new blocks based on the amount of cryptocurrency they hold and "stake" in the network. This means that the more cryptocurrency a validator holds, the more likely they are to be selected to create new blocks and earn rewards. Validators are incentivized to act in the best interest of the network because their stake is at risk if they act maliciously.

To prevent bad actors from taking over the network, PoS uses a mechanism called "slashing," which penalizes validators for any malicious behavior, such as attempting to double-spend coins or creating invalid blocks. Slashing can result in a validator losing a portion of their stake or even being removed from the network entirely.

PoS is considered to be more energy-efficient than PoW because it does not require the same level of computational power as PoW, which makes it a more environmentally friendly option. However, it does require a significant amount of cryptocurrency to be staked in the network, which can make it difficult for smaller players to participate in the validation process.

## 3. Network

The steps to run the network are as follows:

1) New transactions are broadcast to all validators.
2) Each validator keeps track of pending transactions.
3) The validator first in queue collects pending transactions into a block.
4) The validator cryptographically signs the block and broadcasts it to all validators.
5) Validators accept the block only if it was received within a time limit.
6) Validators express their acceptence of the block by using the hash of the accepted block as the previous hash when it's their turn to forge a new block.

Validators always consider the chain with the largest combined sum of stake at the moment to be the correct one.

If a validator disconnects from the network it will experience other validators fail to show up in time which results in burned stake. Once the validator reconnects it will compare chains and choose the correct one with the largest combined sum of stake at the moment.

## 4. Incentive

In a decentralized blockchain network, incentivizing nodes to participate in the consensus process and validate transactions is a critical component of ensuring the network's integrity and security. One of the ways to incentivize nodes is by providing rewards for their contribution to the network. In this proposed cryptocurrency, a reward system has been implemented for forgers.

Forgers, also known as validators, are randomly selected to validate transactions and add them to the blockchain. In this network, a VRF (verifiably random function) is used to randomly select forgers based on the amount of cryptocurrency they have staked. This ensures that the selection process is fair and transparent, and the chance of being selected as a validator is proportional to the amount of cryptocurrency a node has staked.

Every time a block is forged, the forger is rewarded with a fixed amount of 1 Tofuri, as well as any fees collected from the transactions and stakes included in the block. This reward system ensures that forgers have a stable incentive to validate transactions and maintain the network's integrity, irrespective of the network's transaction volume or the cryptocurrency's value. The inclusion of transaction fees in the reward system also incentivizes forgers to include as many transactions as possible in each block they validate, as this increases their potential reward. Overall, the combination of fixed rewards and transaction fees creates a robust incentive system that encourages forgers to act in the best interest of the network and maintain its security and stability.

The reward system incentivizes forgers to act in the best interest of the network by validating transactions accurately and ensuring that the blockchain remains secure and immutable. This system also prevents forgers from engaging in malicious activities, such as double-spending or rewriting the blockchain, as they stand to lose their staked cryptocurrency and the opportunity to earn future rewards.

In summary, the incentive of a fixed reward of 1 Tofuri for forgers in this cryptocurrency ensures a stable and transparent reward system for maintaining the network's integrity and validating transactions. The use of a VRF to randomly select forgers based on their staked cryptocurrency ensures a fair and proportional selection process, and incentivizes forgers to participate in the network's consensus process in a secure and trustworthy manner.

## 5. Node

Nodes play a crucial role in maintaining the Tofuri network. They are computer systems that connect to each other in a peer-to-peer network and share the distributed ledger, also known as the blockchain. The blockchain is a public ledger that records all transactions on the network in a secure and immutable way.

Nodes relay new blocks and transactions to each other, ensuring that all nodes have the latest information. They run software that implements the Tofuri protocol, which defines the rules for transaction validation and block forging.

Nodes can join and leave the network at any time, making it a decentralized and resilient system. Each node keeps a local copy of the blockchain, which is constantly updated as new blocks are added to the chain.

By running a node, individuals can contribute to the network's security and integrity, helping to ensure that transactions are validated accurately and that the blockchain remains immutable and resistant to malicious activity.

## 6. Validator

Validators are nodes that have deposited a stake to participate in the Tofuri network's consensus process. They extend the blockchain by forging new blocks at set time intervals, and in return, they receive a reward for their efforts. The reward consists of collected fees from transactions as well as a fixed amount that is proportional to the amount that the validator is currently staking.

Being a validator comes with the responsibility of showing up when it's time to forge a new block. If a validator fails to show up when it's their turn to forge a block, they are punished by having their stake burned. This punishment serves as a disincentive for validators to miss their turn, thereby helping to ensure the smooth operation and security of the network.

Validators play a critical role in maintaining the integrity and security of the Tofuri network. By participating in the consensus process, validators help to validate transactions accurately and maintain the immutability of the blockchain. As a result, they contribute to the overall stability and success of the network.

It is crucial that the validators' system clocks are synchronized with global time. This is because the protocol relies on accurate time measurements to determine when it is a validator's turn to forge a new block. If a validator's clock is not synchronized, it may miss its turn or forge a block at the wrong time, leading to inconsistencies in the blockchain. Therefore, validators should regularly synchronize their system clocks with a reliable time source to ensure the proper functioning of the Tofuri protocol.

## 7. Storage Optimizations

### 7.1 Tofuri Integer

Tofuri uses a custom integer data type that can store very large integers with fixed precision in order to reduce storage usage. The custom integer is designed to efficiently represent values with high precision, while also minimizing the amount of memory required to store them.

The custom integer works by breaking the number down into a series of smaller integers, each representing a specific digit or group of digits. These smaller integers are then stored in a fixed-size array, with each array element representing a specific digit or group of digits in the larger number.

By using this approach, Tofuri can store large numbers with high precision using a relatively small amount of memory. This is because the custom integer only stores the digits that are actually needed, rather than reserving memory for all possible digits, as is the case with traditional integer data types.

### 7.2 Public key recovery

Tofuri uses the secp256k1 elliptic curve for its digital signatures, which includes the ability to recover the public key from the signature. This means that Tofuri transactions do not need to include the sender's address bytes in every transaction, as the address can be recovered using the hash of the transaction, the signature, and the recovery parameter.

## 8. Database

Tofuri has opted to utilize RocksDB for storing the blockchain due to several reasons. Firstly, RocksDB is designed to offer quick data access, making it a suitable choice for workloads that demand high throughput and low latency, such as storing the blockchain. Moreover, its capability to manage vast data sets and provide durable storage is crucial for housing the ever-increasing blockchain, which necessitates a trustworthy and scalable storage solution.

Furthermore, RocksDB's flexibility allows it to be fine-tuned to enhance its performance for specific workloads, which is essential for meeting the unique requirements of the blockchain. By leveraging RocksDB, Tofuri can deliver a robust and efficient storage system for the blockchain, guaranteeing its scalability and dependability in the long run.
