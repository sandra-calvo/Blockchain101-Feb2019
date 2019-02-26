
# Basic Hyperledger concepts

## INTRODUCTION
This tutorial gets you started developing a blockchain network. I’ll introduce you to Hyperledger Composer and its user interface, Hyperledger Composer Playground, where you can model and test your network with nothing more than Docker and your web browser.

Then you’ll learn how to refine and deploy your blockchain network, and you’ll see how to install Hyperledger Fabric on your computer, deploy your business network to your local instance, and interact with the sample network blockchain application.

### Pre-requisites
- none

### Purpose

This lab introduces the subject of using Hyperledger Composer to build a network model. After completing the lab, you should be able to:

- Learn the concepts of a Hyperledger Business Network
- Understand the Hyperledger Composer modeling language


# PHASE 1
## Hyperledger Composer and basic concepts
One of the Hyperledger projects hosted by The Linux Foundation, Hyperledger Composer is a set of tools that makes building blockchain applications easier, and consists of:
- A modeling language called CTO (an homage to the original project name, Concerto)
- A user interface called Hyperledger Composer Playground for rapid configuration, deployment, and testing of a business network
- Command-Line Interface (CLI) tools for integrating business networks modeled using Hyperledger Composer with a running instance of the Hyperledger Fabric blockchain network

**Hyperledger Composer Playground** is a browser-based interface that you can use to model your business network: what items of value (assets) are exchanged, who participates (participants) in their exchange, how access is secured (access control), what business logic (transactions) is involved in the process, and more.

Hyperledger Composer Playground (Playground from now on) uses your browser’s local storage to simulate the blockchain network’s state storage, which means you don’t need to run a real validating peer network to use Playground.

### Business network concepts
A **Business Network** is the definition of the parties and events involved in tracking transactions which can include trading of assets. At a high level, a business network is a group of entities who work together to accomplish certain goals.  In order to achieve these goals, there must be agreement among the members of the business network regarding:
- The goods and services that are exchanged
- How the exchange is to take place (including business rules governing payment and penalties)
- Which members within the group are allowed to participate, and when

#### Assets
An asset is anything of value that can be exchanged between parties in a business agreement. That means an asset can be pretty much anything. Examples include:
- A boat
- A quantity of stock
- A house
- A crate of bananas
- A shipment of bananas
- A contract for shipment of 1000 crates of bananas for X price based on conditions {X, Y, Z}
You name it. If it has perceived value, and can be exchanged between parties, it’s an asset. 

#### Participants
A participant is a member of a business network. For the Perishable Goods network, this includes the growers who produce the perishable goods, the shippers who transport them from the growers to the ports, and the importers who take delivery of the goods at the ports. Obviously, this model is oversimplified, but it should give you a sense of how real-world applications are modeled using business network terminology.

#### Relationships
You shouldn’t be replicated information about Assets and Participants. Composer provides the mechanism to define relationships between them. So, once I’ve created an asset, with all of the attributes that define that asset, I can simply refer to it from any other Asset, Participant, Transaction or Event. I don’t need to have an attribute like assetName on the Participant who is the Owner of the asset or the Transaction that tracks the service I’ve had on that Asset. I simply create the relationship and I can always get to the assetName through the relationship.

#### Transactions
When an asset is “touched,” that interaction potentially affects the state of the blockchain ledger. The interaction is modeled in Hyperledger Composer as a transaction.

Examples of transactions in the Perishable Goods network include:
- An IoT sensor in the shipping container records a temperature reading
- An Importer receives a shipment of perishable goods
- An IoT GPS sensor records the shipping container’s current location
Transactions are the business logic (or smart contracts) of the system.
Transactions are the definitions of an action, generally involving multiple participants and assets. Examples are Buying/Selling a vehicle, shipping a product, seeing a patient and providing services. 

These are things that need to be tracked and auditable. As well, there should be requirements for a transaction to occur and be endorsed so that it can be entered into the ledger. For example, in order to deliver a vehicle to a buyer, funds need to be transferred from the buyer to the seller, the title/registration application needs to be submitted, and the sales manager needs to provide approval of the sales price. If financing is required, all credit checks and qualification has been done and meets the standards set by the seller.

#### Events
An event is a notification produced by the blockchain application and consumed by an external entity (such as an application) in publish/subscribe fashion.
While the blockchain ledger is updated as assets are exchanged in the system, this is an internal (system) process. However, there are times when an external entity needs to be notified that the state of the ledger has changed, or that maybe something else of note has occurred (or not occurred but should have) in the system. Your blockchain application could use an event in this case.

Examples of events in the Perishable Goods network might include:
- A temperature reading has exceeded an upper or lower boundary X number of times (this might indicate a problem with the shipping container itself, for example).
- A shipment has been received.
- A shipment has arrived at the port (an IoT GPS sensor could report this event, for example).

#### Identities
Users who are authorized to participate in the Business Network and are allowed or required to endorse transactions need an Identity which is handled by a Business Network Card. Some participants in the Business Network may not be endorsing transactions and are simply involved in a transaction. For example, I may be buying a car that is tracked on a Blockchain, but I am not necessarily the endorser of a transaction and may have no need to ever interact directly with the Blockchain. Therefore, I would not need an Identity in the Business Network. 

However, the Sales Manager and Manufacturing Plant would be involved in endorsing the sale of the vehicle and the request for manufacturing as well as the delivery to the customer. Those participants directly involved with endorsing that those things occurred, would need identities.

### Business network files 

There are multiple components to a Business Network which we will discuss below and create in some cases. In the Business Network definition, there are multiple files which are used to define and execute the Network.

- Model File – defines the parties involved, the assets that are to be tracked and the transactions that can occur
- Script File – defines what happens when transactions are submitted
- Access Control – defines who can access what components of the Business Network
- Query File – defines the types of queries that will be accessible to retrieve information from the Business Network
- Business Network Archive – the packaging of the Business Network for deployment into another environment
- Business Network Card – a file containing the identity and credentials of an authorized user of the Business Network

  <img src="/images/HYC1.png" width="100%" height="100%">

#### Model file
The model file uses the Hyperledger Composer modeling language to define components such as:
- Assets – the entities which can be owned, traded, shipped, serviced, etc.
- Participants – the people or things that will act on assets 
- Transactions – the actions that can occur between participants and their assets

All of the attributes for each type of entity are defined in the model file as well as the relationships between them

#### Script File
This is the code that is executed when transactions are submitted for endorsement. In the Blockchain world, this is commonly referred to as “Chaincode” and also is thought of as the vehicle for providing “Smart Contracts”. Before a transaction is endorsed, it must pass the validation of the Chaincode and then it can be added to the Blockchain. This Chaincode can be as sophisticated or as simple as you would like.

#### Access control
In a business network, not every participant has access to everything. For example, a grower does not have access to the contract between the shipper and the importer. Access control is used to limit who has access to what (and under what conditions).
This defines which Identities can Create, Read, Update or Delete components of the Business Network. Of course, the immutability of the Blockchain prohibits any Updates or Deletes of Transactions or Events, but Assets and Participants may come and go.

#### Query definition
This defines what data elements will be exposed with a query.

