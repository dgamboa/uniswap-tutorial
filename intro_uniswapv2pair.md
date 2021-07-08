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

Web3 takes this one step further and decentralizes control over the server layer. You might think about it as a protocol layer that further decouples the client from the server, and importantly, that turns the server layer into decentralized infrastructure. The implications are vast and we're barely scratching the surface, but this simplistic model will allow us to interact with Ethereum - the server layer powering a lot of web3 applications and effectively a world computer. [1]

A smart contract is a computer program encoded with business logic and saved on the Ethereum network. The contract includes an external interface defining how clients may interact with it, and it also includes a set of deterministic instructions that will execute according to the client's request. If the request is valid, the contract will execute and perform its task. Following the canonical example, it's helpful to think of smart contracts like digital vending machines. [2] A vending machine includes an external interface (the coin slot or a credit card terminal) and a set of deterministic instructions (if the right amount of money is inserted, allow the customer to select a drink). Once the purchase is executed, the vending machine delivers a drink to the customer, which changes its state (i.e. one less drink in the vending machine + a certain amount of money in the vending machine), and resets itself to listen for the next request cycle. [3] --> note that much like vending machines, smart contracts are not particularly smart nor legal contracts. 

*vending machine figure*

Writing smart contracts it's no different than writing computer programs. The primary difference is the terminology we use to denote the key data types and structures that make up the protocol. As such, programming languages that are web3 specific have been developed to be able to enable code that is optimized for web3. [Solidity](https://docs.soliditylang.org/en/v0.8.6/) is one of the most popular of these so let's write a little Solidity code to expand our bridge a bit further.

### Solidity Basics
Solidity is an object-oriented, statically typed language used for writing smart contracts for Ethereum and other protocols. If you're familiar with basic code structure and concepts like classes, functions, inheritance and libraries, you'll recognize the patterns of Solidity's implementation immediately.

### Implementing a Smart Contract
Let's implement a simple smart contract that allows us read a default name and re-write it to anything we want. We'll do this with Remix, an online Ethereum IDE, for setup expediency.

Open the [Remix IDE here](https://remix.ethereum.org)

In the workspaces pane on the left, click on the `contracts` folder and then click on the sheet of paper to Create New File

Let's name this file `NameContract.sol` and hit enter

Solidity files start with a `pragma` line to instruct the compiler on the expected version. In this case, let's use any version above `0.5.0` by writing `pragma ^0.5.0` at the top of the file.

The main data type in Solidity is `contract`, which you can think of as a class in the non-web3 paradigm. Effectively, this is a container that will house the smart contract's data and business logic. Let's start the contract by writing:
```
pragma ^0.5.0

contract NameContract {

}
```

Now, we can set the `name` property for the `NameContract` by creating a `name` variable inside of it and setting it to any default value we want.
```
pragma ^0.5.0

contract NameContract {
  string public name = "Jane";
}
```
Note that we could have also set the `name` variable without a default value by excluding the variable assignment. In that case, our name property would be empty until assigned.
 
We can now get ready to deploy the contract by clicking the Ethereum logo labeled "Deploy & Run Transactions" on the left navigation pane. We then click the `Deploy` button, expand the deployed contract, and click `name` to see our default name, "Jane". You'll also notice the log at the bottom of the IDE showing our simulated interactions with the Ethereum blockchain.

You've technically built your first smart contract! It can only read though, so let's add some functionality to change our name if we so choose.

*tarzan jane figure*

Let's implement a `set` function that will take in a string name as an argument and reset our name to it.
```
pragma ^0.5.0

contract NameContract {
  string public name = "Jane";

  function set(string memory _name) public {
    name = _name;
  }
}
```

With that in place, let's redeploy the contract. Go to the second contract (just below the first one deployed) and expand it. Clicking the `name` button should return our default name, "Jane". Now go to the text box next to the `set` button. Write in "Tarzan", and click `set`. You'll notice the logs show a pending transaction followed by a confirmed transaction. 

*insert screenshot of transaction log*

This means we were able to interact with the smart contract and change the state of its `name`. To confirm, click the `name` button to see that your name change was successful!

As you can tell the syntax is similar to TypeScript - nothing too out of the ordinary. There's a lot more to Solidity implementations as you can imagine, but you now have a solid mental model foundation from which to expand. For a more in-depth tutorial on Solidity, check out the [docs here](https://docs.soliditylang.org/en/v0.8.6/solidity-by-example.html) or watch this [freeCodeCamp tutorial](https://www.youtube.com/watch?v=ipwxYa-F1uY).

## Reviewing UniswapV2Pair
--reference back to section 2--

## Interacting with UniswapV2Pair

## Conclusion
