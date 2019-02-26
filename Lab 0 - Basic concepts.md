
# [Hyperledger Fabric](https://www.hyperledger.org/projects/fabric)

## INTRODUCTION
This lab introduces the subject of using Hyperledger Composer to build a network model. After completing the lab, you should be able to:

- Learn the Hyperledger Fabric Concepts
- Understand how Hyperledger Fabric works

### Pre-requisites
- none

### Introduction
#### Hyperledger Fabric
Hyperledger Fabric is an open source enterprise-grade permissioned distributed ledger technology (DLT) platform, designed for use in enterprise contexts, that delivers some key differentiating capabilities over other popular distributed ledger or blockchain platforms.

Fabric is the first distributed ledger platform to support smart contracts authored in general-purpose programming languages such as Java, Go and Node.js, rather than constrained domain-specific languages (DSL). 

One of the most important of the platform’s differentiators is its support for **pluggable consensus protocols** that enable the platform to be more effectively customized to fit particular use cases and trust models. 

#### Modularity
Hyperledger Fabric has been specifically architected to have a modular architecture. Whether it is pluggable consensus, pluggable identity management protocols such as LDAP or OpenID Connect, key management protocols or cryptographic libraries, the platform has been designed at its core to be configured to meet the diversity of enterprise use case requirements.

At a high level, Fabric is comprised of the following modular components:

    A pluggable ordering service establishes consensus on the order of transactions and then broadcasts blocks to peers.
    A pluggable membership service provider is responsible for associating entities in the network with cryptographic identities.
    An optional peer-to-peer gossip service disseminates the blocks output by ordering service to other peers.
    Smart contracts (“chaincode”) run within a container environment (e.g. Docker) for isolation. They can be written in standard programming languages but do not have direct access to the ledger state.
    The ledger can be configured to support a variety of DBMSs.
    A pluggable endorsement and validation policy enforcement that can be independently configured per application.

#### Permissioned Blockchain
Permissioned blockchains operate a blockchain amongst a set of known, identified and often vetted participants operating under a governance model that yields a certain degree of trust. A permissioned blockchain provides a way to secure the interactions among a group of entities that have a common goal but which may not fully trust each other. By relying on the identities of the participants, a permissioned blockchain can use more traditional crash fault tolerant (CFT) or byzantine fault tolerant (BFT) consensus protocols that do not require costly mining.


#### Smart Contracts
A smart contract, or what Fabric calls “chaincode”, functions as a trusted distributed application that gains its security/trust from the blockchain and the underlying consensus among the peers. It is the business logic of a blockchain application.

There are three key points that apply to smart contracts, especially when applied to a platform:

    many smart contracts run concurrently in the network,
    they may be deployed dynamically (in many cases by anyone), and
    application code should be treated as untrusted, potentially even malicious.

#### New approach
Fabric introduces a new architecture for transactions that we call execute-order-validate. It addresses the resiliency, flexibility, scalability, performance and confidentiality challenges faced by the order-execute model by separating the transaction flow into three steps:

    execute a transaction and check its correctness, thereby endorsing it,
    order transactions via a (pluggable) consensus protocol, and
    validate transactions against an application-specific endorsement policy before committing them to the ledger

This design departs radically from the order-execute paradigm in that Fabric executes transactions before reaching final agreement on their order.

#### Privacy and Confidentiality

#### Pluggable Consensus

#### Performance and Scalability






For more information check: [Hyperledger Fabric Docs](https://hyperledger-fabric.readthedocs.io)
