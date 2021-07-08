---
description: >-
  Start building a smart contracts mental model by exploring Uniswap V2 Pair
---

# Demystifying Uniswap V2 Pair: A Concrete Introduction to Smart Contracts

## Introduction
*Demystifying Uniswap V2 Pair* is an introduction to the world of smart contracts for web2 developers. It is aimed at those with a basic understanding of web development systems (frontend clients, backend APIs and databases, internet protocols), so if you've ever as much as dabbled with writing code for the web, and certainly if you've ever built web2 applications, you're in the right place. Having said that, this tutorial doesn't assume any technical sophistication with smart contracts. In fact, even if you've never written code, you'll probably gain an appreciation for how much leverage is embedded in web3 systems. That is, there's a tremendous amount of value-add work being performed with minimal input.

*leverage figure*

The main intent of this tutorial is to enhance (or perhaps even kickstart) your smart contracts mental model by introducing you to the basics in the context of a simple but sophisticated smart contract - the UniswapV2Pair contract powering the core functionality of the Uniswap decentralized exchange. This contract powers a large crypto-trading liquidity pool autonomously and has supported daily trading volumes as high as $4 billion. Moreover, trading volume in Uniswap was $36 billion in April 2021 - roughly one third of Coinbase, the largest centralized crypto exchange. We'll acquire the building blocks to understand this contract at a high level in *Section 2*, and dive into the code for it in *Section 3*.

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

### Key Ethereum Concepts
It was helpful to abstract away the key web2 differences in the `NameContract` implementation so we could avoid any intimidating jargon and instead focus on writing a functional smart contract. Now that we've seen how simple it can be, let's go one layer deeper on some key differences.

One of the first you might notice if you look to the left of our code on Remix is the account field. While it's tempting to think of these as pseudo-IP addresses, they're different enough that it might be more helpful to take a step back and discuss Ethereum's basic building blocks.

- Transactions: think of transactions as network requests and responses. These can only be initiated by externally-owned accounts (described below) and result in a state change to the network. Because these require validation before changing state, they need to be mined and propagated. As such they require a fee to incentivize miners to execute the validation and propagation. For more, see the [Ethereum docs on Transactions](https://ethereum.org/en/developers/docs/transactions/).
- Accounts: there are two types of accounts on Ethereum. Both can receive, hold and send tokens, and both can interact with deployed smart contracts. For more, see the [Ethereum docs on Accounts](https://ethereum.org/en/developers/docs/accounts/).
  - Externally-Owned Accounts (EOA): human managed accounts with private to interact securely with the network and public keys to expose the account interface to the network. These accounts can initiate transactions.
  - Contract Accounts: smart contracts deployed to the network at a specific address and controlled by code. These can only send transactions in response to receiving a transaction.
- Gas: gas is the economic mechanism by which Ethereum ensures the network's resources are being used efficiently. Think of gas as the unit measuring the computational work performed by the network when a transaction is sent. The gas fees associated with a transaction can vary based on the transaction's complexity and the market price of gas (i.e. how much demand there is for processing transactions in the network at a given time). For more, see  the [Ethereum docs on Gas](https://ethereum.org/en/developers/docs/gas/).

With those concepts in mind, you're now equipped to better understand the other parameters in the Remix dashboard. The account field represents the address, or unique identifier, of our simulated EOA. If you expand the log for your contract deployment, you can see the same address in the `from` field. Similarly, in the expanded log, you can see a similar string of alphanumeric characters that represents the contract's address in the `to` field.

The other key parameter in the Remix dashboard is the gas limit field just below the account field. This represents the maximum gas you're willing to use to execute the transaction. When the gas consumed reaches the limit, the transaction will automatically stop. The gas cost (gas * gas price) will be incurred regardless, but if the transaction didn't finish executing, any changes it had intended to make won't persist and the network will continue operating in its pre-transaction state. If you decrease the gas limit enough in the `NameContract` and click the `name` button in the contract to get the name, you'll notice the call will fail and the log will display an error message saying, "base fee exceeds gas limit".

## Reviewing UniswapV2Pair
As promised in *Section 1*, we have most of the blocks we need to extend our mental model into a real smart contract. Before we dive into the code though, let's build one more block to finalize our bridge by understanding Uniswap itself.

### Defining Uniswap
[Uniswap]() is a decentralized exchange implemented as a smart contract on Ethereum. It works by enabling liquidity pools of paired tokens and dynamically calculating their relative price according to the balance in their relative reserves.

To make the mental model a bit more concrete, imagine we have two assets, apples and oranges. We decide to make a market for people who want to trade apples for oranges and vice-versa. We build a small stand under a buttonwood tree and keep two buckets under the stand: one containing 100 apples, and the other containing 10 oranges. We list an exchange rate of 10 apples per orange and open for business. Perhaps someone notices that the relative pricing of apples and oranges at the grocery store is 5 apples per orange, and decides to buy 10 apples from us with one orange to take advantage of the arbitrage. That is, they will be able to get a free orange by purchasing an orange from the grocery store, using that orange to get 10 apples from us, and then trading those 10 apples for 2 oranges at the grocery store. Now that we have 10 less apples in our basket, and one extra orange, our baskets have 90 apples and 11 oranges. This means the price of our oranges in terms of our apples should have decreased. With the right pricing mechanism, you would expect our price to converge with the grocery store price as more buyers arbitrate the relative mispricing.

The algorithm Uniswap uses to price each of their liquidity pools is only slightly more complicated and you're welcome to [read about it more here](https://uniswap.org/docs/v2/protocol-overview/how-uniswap-works/). But the key concepts are that Uniswap enables automated liquidity pools for token pairs.

If you're HODLing tokens and want to participate as a liquidity provider, you can interact with the live smart contract for the specific pair you're interested in and contribute your tokens. You'll be granted a pro-rata share of the pool reserves in the form of a pool token that proves your ownership. Once you're ready to withdraw the liquidity you contributed, you trade the token back. 

Alternatively, if you're a trader with a certain token, say `token a`, and you want to buy `token b, you can go to the `token a - token b` liquidity pool and trade `token a` for `token b`. You pay a small fee for the trade, and it automatically executes. The right amount of `token a` + the fee is withdrawn from your wallet and sent to the pool, and the right amount of `token b` is automatically withdrawn from the pool and sent to your wallet. In a large enough pool with enough trading volume and a small enough transaction relative to the pool, the price movement caused by your trade would be infinitesimally small.

*uniswap system figure*

Developers are a key part of the ecosystem because they represent the frontend of the Uniswap ecosystem. Uniswap provides functionality that can be leveraged directly by developers building trading interfaces, and indirectly by developers building additional functionality on top of Uniswap. For more examples, check out the [ecosystem participants page on the Uniswap protocol overview]().

You might also want to solidify your understanding of automated liquidity pools relative to standard centralized exchanges. If so, this video from Finematics does a good job contrasting the two.

*embed youtube video*

## Interacting with UniswapV2Pair

## Conclusion

## Further Reading
- Uniswap V2 whitepaper
- Ethereum docs
- Uniswap docs
