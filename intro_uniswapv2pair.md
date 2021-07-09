---
description: >-
  Start building a mental model by exploring the Uniswap V2 Pair smart contract
---

# An Introduction to Smart Contracts: Demystifying Uniswap V2 Pair

## Introduction
*Demystifying Uniswap V2 Pair* is an introduction to the world of smart contracts for web2 developers. It is aimed at those with a basic understanding of web development systems (frontend clients, backend APIs and databases, internet protocols), so if you've ever as much as dabbled with writing code for the web, and certainly if you've ever built web2 applications, you're in the right place. Having said that, this tutorial doesn't assume any technical sophistication with smart contracts. In fact, even if you've never written code, you'll probably gain an appreciation for how much leverage is embedded in web3 systems. That is, there's a tremendous amount of value-add work being performed with minimal input.

*leverage figure*

The main intent of this tutorial is to enhance (or perhaps even kickstart) your smart contracts mental model by introducing you to the basics in the context of a simple but sophisticated smart contract - the UniswapV2Pair contract powering the core functionality of the Uniswap decentralized exchange. This contract powers a large crypto-trading liquidity pool autonomously and has supported daily trading volumes as high as $4 billion. Moreover, trading volume in Uniswap was $36 billion in April 2021 - roughly one third of Coinbase, the largest centralized crypto exchange. We'll acquire the building blocks to understand this contract at a high level in *Section 2*, and dive into the code for it in *Section 3*.

While we won't be diving deep into the basic concepts of web3 (e.g. blockchain, Ethereum, etc), we will define certain key terms along the way at a high level. Like a cartographer mapping the shore from a ship, the idea is to develop a sense for the concepts, allow for pattern matching with existing mental models, and begin to build the new mental models we'll need to expand our existing knowledge base. That's in contrast to the work of a surveyor that might study the territory up close to understand the specifics of each feature. 

Our intent is to be the exploration guide that helps you discover. In so doing, we want to help lower the activation energy for you to move from explorer to builder. Ideally, you'll walk away with a better mental model while realizing that many of the core concepts of web2 apply in the context of web3. You might even walk away having identified multiple threads (i.e. known unknowns) that you're excited to pull on.

*activation energy figure*

## Smart Contracts
Before we dive into the Uniswap contract in [section 3](link), we'll first develop some key building blocks that will bridge our existing web2 mental models and allow us to expand into new territory. In a way, this will be our basecamp from which to launch a summit assault.

Web2 is built on the [client-server model](https://en.wikipedia.org/wiki/Client%E2%80%93server_model) that connects clients (computers that issue requests) to servers (computers that provide resources) using a network. The servers handles request processing and data storage as centralized controllers that multiple clients access. To the extent there's duplication and redundancy in server systems, they are centrally managed and retain control over the data that interacts with them.

Web3 takes this one step further and decentralizes control over the server layer. You might think about it as a protocol layer that further decouples the client from the server, and importantly, that turns the server layer into decentralized infrastructure. The implications are vast and we're barely scratching the surface, but this simplistic model will allow us to interact with Ethereum - the server layer powering a lot of web3 applications and effectively a world computer. [1]

A smart contract is a computer program encoded with business logic and saved on the Ethereum network. The contract includes an external interface defining how clients may interact with it, and it also includes a set of deterministic instructions that will execute according to the client's request. If the request is valid, the contract will execute and perform its task. Following the [canonical example], it's helpful to think of smart contracts like digital vending machines. [2] A vending machine includes an external interface (the coin slot or a credit card terminal) and a set of deterministic instructions (if the right amount of money is inserted, allow the customer to select a drink). Once the transaction is executed, the vending machine delivers a drink to the customer, which changes its state (i.e. one less drink in the vending machine + a certain amount of money in the vending machine), and resets itself to listen for the next request cycle. [3] --> note that much like vending machines, smart contracts are not particularly smart nor legal contracts. 

*vending machine figure*

Writing smart contracts it's no different than writing computer programs. The primary difference is the terminology we use to denote the key data types and structures that make up the protocol. As such, programming languages that are web3 specific have been developed to be able to enable code that is optimized for web3. [Solidity](https://docs.soliditylang.org/en/v0.8.6/) is one of the most popular of these so let's write a little Solidity code to expand our bridge a bit further.

### Solidity Basics
Solidity is an object-oriented, statically typed language used for writing smart contracts for Ethereum and other protocols. If you're familiar with basic code structure and concepts like classes, functions, inheritance and libraries, you'll recognize the patterns of Solidity's implementation immediately.

### Implementing a Smart Contract
Let's implement a simple smart contract that allows us to read a default name and re-write it to anything we want. We'll do this with [Remix], an online Ethereum IDE, for setup expediency.

Open the [Remix IDE here](https://remix.ethereum.org).

In the workspaces pane on the left, click on the `contracts` folder and then click on the sheet of paper to Create New File.

Let's name this file `NameContract.sol` and hit enter.

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
Note that we could have set the `name` variable without a default value by excluding the variable assignment. In that case, our name property would be empty until assigned.
 
We can now get ready to deploy the contract by clicking the Ethereum logo labeled "Deploy & Run Transactions" on the left navigation pane. We then click the `Deploy` button, expand the deployed contract, and click `name` to see our default name, "Jane". You'll also notice the log at the bottom of the IDE showing our simulated interactions with the Ethereum blockchain.

*include screenshot*

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

As you can tell the syntax is similar to [TypeScript] - nothing too out of the ordinary. There's a lot more to Solidity implementations as you can imagine, but you now have a solid mental model foundation from which to expand. For a more in-depth tutorial on Solidity, check out the [docs here](https://docs.soliditylang.org/en/v0.8.6/solidity-by-example.html) or watch this [freeCodeCamp tutorial](https://www.youtube.com/watch?v=ipwxYa-F1uY).

### Key Ethereum Concepts
It was helpful to abstract away the key web2 differences in the `NameContract` implementation so we could avoid any intimidating jargon and instead focus on writing a functional smart contract. Now that we've seen how simple it can be, let's go one layer deeper on some key differences.

One of the first you might notice if you look to the left of our code on Remix is the account field. While it's tempting to think of these as pseudo-IP addresses, they're different enough that it might be more helpful to take a step back and discuss Ethereum's basic building blocks.

- Transactions: think of transactions as network requests and responses. These can only be initiated by externally-owned accounts (described below) and result in a state change to the network. Because these require validation before changing state, they need to be mined and propagated. As such they require a fee to incentivize miners to execute the validation and propagation. For more, see the [Ethereum docs on transactions](https://ethereum.org/en/developers/docs/transactions/).
- Accounts: there are two types of accounts on Ethereum. Both can receive, hold and send tokens, and both can interact with deployed smart contracts. For more, see the [Ethereum docs on accounts](https://ethereum.org/en/developers/docs/accounts/).
  - Externally-Owned Accounts (EOA): human managed accounts with private keys to interact securely with the network and public keys to expose the account interface to the network. These accounts can initiate transactions.
  - Contract Accounts: smart contracts deployed to the network at a specific address and controlled by code. These can only send transactions in response to receiving a transaction.
- Gas: gas is the economic mechanism by which Ethereum ensures the network's resources are being used efficiently. Think of gas as the unit measuring the computational work performed by the network when a transaction is sent. The gas fees associated with a transaction can vary based on the transaction's complexity and the market price of gas (i.e. how much demand there is for processing transactions in the network at a given time). For more, see  the [Ethereum docs on gas](https://ethereum.org/en/developers/docs/gas/).

With those concepts in mind, you're now equipped to better understand the other parameters in the Remix dashboard. The account field represents the address, or unique identifier, of our simulated EOA. If you expand the log for your contract deployment, you can see the same address in the `from` field. Similarly, in the expanded log, you can see a similar string of alphanumeric characters that represents the contract's address in the `to` field.

The other key parameter in the Remix dashboard is the gas limit field just below the account field. This represents the maximum gas you're willing to use to execute the transaction. When the gas consumed reaches the limit, the transaction will automatically stop. The gas cost (gas * gas price) will be incurred regardless, but if the transaction didn't finish executing, any changes it had intended to make won't persist and the network will continue operating in its pre-transaction state. If you decrease the gas limit enough in the `NameContract` and click the `name` button in the contract to get the name, you'll notice the call will fail and the log will display an error message saying, "base fee exceeds gas limit".

## Reviewing UniswapV2Pair
As promised in *Section 1*, we have most of the blocks we need to extend our mental model into a real smart contract. Before we dive into the code though, let's build one more block to finalize our bridge by understanding Uniswap itself.

### Defining Uniswap
[Uniswap]() is a decentralized exchange implemented as a smart contract on Ethereum. It works by enabling liquidity pools of paired tokens and dynamically calculating their relative price according to the balance in their relative reserves.

To make the mental model a bit more concrete, imagine we have two assets, apples and oranges. We decide to make a market for people who want to trade apples for oranges and vice-versa. We build a small stand under a buttonwood tree and keep two buckets under the stand: one containing 100 apples, and the other containing 10 oranges. We list an exchange rate of 10 apples per orange and open for business. Perhaps someone notices that the relative pricing of apples and oranges at the grocery store is 5 apples per orange, and decides to buy 10 apples from us with one orange to take advantage of the arbitrage. That is, they will be able to get a free orange by purchasing an orange from the grocery store, using that orange to get 10 apples from us, and then trading those 10 apples for 2 oranges at the grocery store. Now that we have 10 less apples in our basket, and one extra orange, our baskets have 90 apples and 11 oranges. This means the price of oranges in terms of apples has decreased moving closer to the grocery store price. With the right pricing mechanism, you would expect our price to converge with the grocery store price as more buyers arbitrage the relative mispricing.

The algorithm Uniswap uses to price each of their liquidity pools is slightly more complicated and you're welcome to [read about it more here](https://uniswap.org/docs/v2/protocol-overview/how-uniswap-works/). But the key concepts are that Uniswap enables automated liquidity pools for token pairs.

*uniswap system figure*

If you're HODLing tokens and want to participate as a liquidity provider, you can interact with the smart contract for the specific pair you're interested in and contribute your tokens. You'll be granted a pro-rata share of the pool reserves in the form of a pool token that proves your ownership. Once you're ready to withdraw the liquidity you contributed, you trade the token back. 

*screen shot from the uniswap app*

Alternatively, if you're a trader with a certain token, say `token a`, and you want to buy `token b, you can go to the `token a - token b` liquidity pool and trade `token a` for `token b`. You pay a small fee for the trade, and it automatically executes. The right amount of `token a` + the fee is withdrawn from your wallet and sent to the pool, and the right amount of `token b` is automatically withdrawn from the pool and sent to your wallet. In a large enough pool with enough trading volume and a small enough transaction relative to the pool, the price movement caused by your trade would be infinitesimally small.

*screen shot from the uniswap app*

Developers are a key part of the ecosystem because they represent the frontend of the Uniswap ecosystem. Uniswap provides functionality that can be leveraged directly by developers building trading interfaces, and indirectly by developers building additional functionality on top of Uniswap. For more examples, check out the [ecosystem participants page on the Uniswap protocol overview]().

*start side note*
You might also want to enhance your understanding of automated liquidity pools relative to standard centralized exchanges. If so, this video from Finematics does a good job contrasting the two.

*embed youtube video*
*end side note*

### Uniswap Under the Hood
While Uniswap is a great way to start forming a concrete mental model of smart contracts through a massive, real-world application, the Uniswap system is complex and sophisticated. Keep that in mind as we discuss the codebase. Rather than building a comprehensive understanding of the Uniswap architecture, we'll generalize and abstract to help you start setting your foundation. We'll leave it up to you whether you want to leverage this foundation to expand horizontally into other topics or vertically into Uniswap. If you choose the latter, we've included additional resources at the end of the tutorial for [further reading]().

The codebase for Uniswap is open source, so let's dive into the codebase structure to set up a deeper dive into specific functions. Go to the [GitHub repository here](https://github.com/Uniswap/uniswap-v2-core) and review the file structure at the root of the project. You'll notice two main folders at the top, `contracts` and `test`. You'll also notice a few configuration files and a README file with simple, high-level information on Uniswap V2. As you might expect, everything except the contents of the `contracts` folder is here to support the project (i.e. the smart contracts driving Uniswap's functionality).

Click on the `contracts` folder. Here we have three folders and three contracts:
1. Interfaces Folder: this include various interface objects. Interfaces in solidity are effectively contract templates. They stub a contract shape with functions that include arguments and return types without their implementation. Contracts can inherit interfaces and leverage them as templates from which to form their functionality.
1. Libraries Folder: similar to other languages, Solidity libraries are modules that abstract certain key, universal functionality into modules that can be imported and leveraged by the codebase.
1. Test Folder: simple test file.
1. UniswapV2ERC20.sol: This smart contract modularizes certain market making functionality managed by UniswapV2Pair. Specifically,  
1. UniswapV2Factory.sol: This smart contract handles the creation of one smart contract per unique token pair.
1. UniswapV2Pair.sol: This is the primary market making engine. It leverages the UniswapV2ERC20 contract for certain functionality and manages trades for a given [ERC-20] pair.

*include architecture diagram*

### Reviewing UniswapV2Factory
The best place to start building a technical understanding of Uniswap is the factory smart contract. We'll now leverage the basic mental model of Solidity from *section 2* to review the code that starts the Uniswap magic.

*tesla magic figure*

Click on the [UniswapV2Factory.sol](https://github.com/Uniswap/uniswap-v2-core/blob/master/contracts/UniswapV2Factory.sol) contract to open the page with its source code. The first thing you'll notice is the Solidity version specification on line 1, `pragma solidity =0.5.16;`. You'll also notice a couple of imports on lines 3 and 4 so the factory can leverage code from the factory interface (i.e. template) and the UniswapV2Pair contract. You might be wondering why the factory needs to leverage the UniswapV2Pair code. Recall that the role of the factory is to create liquidity pools for specific pairs. In other words, the factory is tasked with creating instances of pools that are governed by the code written in the pair contract. For the factory to be able to "instantiate" a pair, it needs to have access to the pair contract blueprint.

On line 6, we can see the factory contract being defined and inheriting from its corresponding interface. It declares a couple of variables that will allow Uniswap to turn on a slight change in how the trading fee proceeds are allocated. It also declares another set of variables, `getPair` and `allPairs` that we'll see shortly.

The next three items in the code we can quickly skim - an event object, a simple constructor, and a function that returns the length of the `allPairs` variable.

With that we can review the main function, `createPair`. This function takes two token addresses and returns the address for the created pair smart contract. That is, it takes in the two tokens for which we wish to create a liquidity, and returns the address of the created liquidity pool. The first line in the function validates that the two inputs aren't the same token since it doesn't make sense to swap a token for itself. The second line sorts the input token addresses in increasing order. The third line ensures the lowest address `token0` isn't the 0 address in Ethereum, which has a separate use case and doesn't represent a specific token. The fourth line ensures the pair hasn't already been created since the `getPair` function returns the 0 address if there's no existing pair liquidity pool.

The next few lines (lin 28-33) are the key lines that fabricate the pair after all validations checked out. This part of the function uses the UniswapV2Pair blueprint to initialize a pair liquidity pool for the two tokens. We'll dive deeper into the workings of the `initialize` function in the next section. It then records the pair address for the pool in lines 34 and 35, which will be used in the validations for future pair creations. Finally, it pushes the pair address into the list storing all the pairs that have been created and emits an event logging the pair creation.

The last two functions are associated with the allocation of trading fee proceeds discussed above. With a better understanding of how Uniswap creates pairs, we've can now dive into the main show - the UniswapV2Pair contract.

*greatest showman figure*

### Reviewing UniswapV2Pair
Let's dive into the pair smart contract that governs how the liquid pools work by [clicking on UniswapV2Pair.sol](https://github.com/Uniswap/uniswap-v2-core/blob/master/contracts/UniswapV2Pair.sol). You'll immediately notice it starts in much the same way as the factory. It specifies a version of Solidity and imports a few interfaces and libraries that it will presumably leverage. It also imports the UniswapV2ERC20 smart contract, which governs the pool tokens used to represent pool ownership by liquidity providers.

On line 11, we can see the pair contract being defined and inheriting from its corresponding interface and from the ERC20 contract. It then sets how the uint and uint224 data types will be used by leveraging two libraries. It assigns two variables, `MINIMUM_LIQUIDITY` and `SELECTOR`, and then declares a few variables we'll see in the functions below. You'll notice a the private variable unlocked is set to `1` on line 30 followed by a modifier function, `lock`. Modifiers act like middleware in solidity. They perform actions before, during, or after a function's execution. The characters `_;` denote where the main function will execute in the context of a modifier's execution. We'll see how the `lock` modifier is used when we review the `swap` function below.

This is the perfect time to review the `initialize` function we saw when we created a pair liquidity pool in the factory. On line 66, you'll notice the function definition, which takes in two tokens as we saw in the previous section. This function first checks that the request is coming from a factory by leveraging the Solidity `msg.sender` syntax, where `msg` is the object that originated the call and `msg.sender` is the address of that object (i.e. EOA or contract). It then sets the contract's token properties to the two tokens passed in as arguments. If you search for the keywords `token0` and `token1` in the contract, you'll notice this is the only place where we set those properties, which makes sense since once a liquidity pool is established with two tokens, those should never change.

The three primary functions of a pair contract are `mint`, `burn`, and `swap`. We'll dive into `swap` in more detail, but let's define all three first:
- `mint`: creates pool tokens provided to liquidity providers in return for their contributed token pairs.
- `burn`: burns pool tokens when a liquidity provider withdraws their contributed token pairs.
- `swap`: enables traders to swap a token for another at the appropriate exchange rate.

Scrolling to line 159, we can finally review the core Uniswap functionality that allows traders to exchange token pairs. You'll notice the function takes in four arguments: `amount0Out`, `amount1Out`, `to` (of `address` type), and `data`. You'll also notice that the function uses the keyword `lock` to incorporate the modifier we saw above. Conceptually this is locking the function while it executes. This is to prevent reentrancy attacks, which can externally manipulate a function while it executes (if you're interested in these, you should read about the 2016 DAO attack).

The function then ensures at least one of the amounts to send out is greater than zero, sets local reserve variables for each token in the pair, and ensures the amounts to send out are less than the reserves in the liquidity pool. On lines 167-169 the contract sets variables for the token addresses and checks that the trader's `to` address is valid. The contract then initiates the transfer on lines 170-171, and sets balance variables for each token. On lines 176-177 the contract calculates how much the trader injected into the pool in exchange for the token bought by taking the subtracting the difference of the reserves (set before the transfer) and the amount out from the balance (set after the transfer). Finally the function performs numerical adjustments on the balances before confirming that the product of its pairs is preserved (the invariant `k` value driving price movements). Finally, it syncs up the balance and reserve variables before emitting a `Swap` event logging the transaction.

Once you understand the this function's flow, you understand the main driver of the Uniswap exchange. From here you can invest additional time thinking through how this function interacts with the broader Ethereum ecosystem, how it leverages arbitrage forces for maintain market pricing, and how financial drivers incentivize activity on the exchange. You might even consider diving into the whitepaper to better understand the constant product formula, or studying the fascinating history behind Uniswap's founding and growth.

*picture: now I can see*

## Conclusion
Congratulations! You've built the foundation to your smart contracts mental model and in the process picked up a concrete understanding of one of the most popular and consequential smart contracts in DeFi. As you can see, smart contracts and the DeFi universe in general is both fascinating and exciting, but it can be hard to dive into the complexity associated with the inner workings. I hope that this foundation helps lower your activation energy to dive into more topics, and as a show of goodwill, I've included some further reading below that might pique your curiosity. Most of all, I hope you walk away with a better sense for what it takes to build smart contracts and with the belief that you can build these yourself.

## Further Reading
- Ethereum Documentation
- Solidity Documentation
- Uniswap How It Works
- Uniswap Documentation
- Uniswap V2 Whitepaper
- [Writing a Smart Contract to Interact with Uniswap](https://uniswap.org/docs/v2/smart-contract-integration/quick-start/)
- Mastering Ethereum
