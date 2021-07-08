---
description: >-
  Start building a smart contracts mental model by exploring Uniswap V2 Pair
---

# Demystifying Uniswap V2 Pair

## Introduction
*Demystifying Uniswap V2 Pair* is an introduction to the world of smart contracts for web2 developers. It is aimed at those with a basic understanding of web development systems (frontend clients, backend APIs and databases, internet protocols), so if you've ever as much as dabbled with writing code for the web, and certainly if you've ever built web2 applications, you're in the right place. Having said that, this tutorial doesn't assume any technical sophistication with smart contracts. In fact, even if you've never written code, you'll probably gain an appreciation for how much leverage is embedded in web3 systems. That is, there's a tremendous amount of value-add work being performed with minimal input.

*leverage figure*

The main intent of this tutorial is to enhance (or perhaps even kickstart) your smart contracts mental model by introducing you to the basics in the context of a simple but sophisticated smart contract - the UniswapV2Pair contract powering the core functionality of the Uniswap decentralized exchange. This contract powers a large crypto-trading liquidity pool autonomously and has supported daily trading volumes as high as $4 billion. Moreover, trading volume in Uniswap was $36 billion in April 2021 - roughly one third of Coinbase, the largest centralized crypto exchange. 

While we won't be diving deep into the basic concepts of web3 (e.g. blockchain, Ethereum, etc), we will define certain key terms along the way at a high level. Like a cartographer mapping the shore from a ship, the idea is to develop a sense for the concepts, allow for pattern matching with existing mental models, and begin to build the new mental models we'll need to expand our existing knowledge base. That's in contrast to the work of a surveyor that might study the territory up close to understand the specifics of each feature. 

Our intent is to be the exploration guide that helps you discover. In so doing, we want to help lower the activation energy for you to move from explorer to builder. Ideally, you'll walk away with a better mental model while realizing that many of the core concepts of web2 apply in the context of web3. You might even walk away having identified multiple threads (i.e. known unknowns) that you're excited to pull on.

*activation energy figure*

## Smart Contracts
Before we dive into the Uniswap contract in [section 3](link), we'll first develop some key building blocks that will bridge our existing web2 mental models and allow us to expand into new territory. In a way, this will be our basecamp from which to launch a summit assault.

Web2 is built on the [client-server model](https://en.wikipedia.org/wiki/Client%E2%80%93server_model) that connects clients (computers that issue requests) to servers (computers that provide resources) using a network. The servers handles request processing and data storage as centralized controllers that multiple clients access. To the extent there's duplication and redundancy in server systems, they are  centrally managed and retain control over the data that interacts with them.

Web3 takes this one step further and decentralizes control over the server layer. You might think about it as a protocol layer that further decouples the client from the server, and importantly, that turns the server layer into decentralized infrastructure. The implications are vast and we're barely scratching the surface, but this simplistic model will allow us to interact with Ethereum - the server layer powering a lot of web3 applications. [1]

A smart contract is a computer program encoded with business logic and saved on the Ethereum network. The contract includes an external interface defining how clients may interact with it, and it also includes a set of deterministic instructions that will execute according to the client's request. If the request is valid, the contract will execute and perform its task. Following the canonical example, it's helpful to think of smart contracts like digital vending machines. [2] A vending machine includes an external interface (the coin slot or a credit card terminal) and a set of deterministic instructions (if the right amount of money is inserted, allow the customer to select a drink). Once the purchase is executed, the vending machine delivers a drink to the customer, which changes its state (i.e. one less drink in the vending machine + a certain amount of money in the vending machine), and resets itself to listen for the next request cycle.

*vending machine figure*

Writing smart contracts it's no different than writing computer programs. The primary difference is the terminology we use to denote the key data types and structures that make up the protocol. As such, programming languages that are web3 specific have been written to be able to enable code that is optimized for web3. [Solidity] is one of the most popular of these so let's a little Solidity code to expand our bridge a bit further.

### Solidity Basics


### Implementing a Smart Contract


For a more in-depth tutorial on Solidity, check out this quick tutorial from freeCodeCamp.

## Reviewing UniswapV2Pair
--reference back to section 2--

## Interacting with UniswapV2Pair

## Conclusion
