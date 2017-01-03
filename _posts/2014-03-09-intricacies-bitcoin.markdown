---
author: admin
comments: true
date: 2014-03-09 10:11:34+00:00
layout: post
link: http://www.lambdacurry.com/2014/03/intricacies-bitcoin/
slug: intricacies-bitcoin
title: The intricacies of Bitcoin
wordpress_id: 866
---

What are some of the under-the-surface aspects of Bitcoin that safeguard its larger application as a viable digital currency


# **transaction fees **


each transaction in Bitcoin is subject to [transaction fees](https://en.bitcoin.it/wiki/Transaction_fees), that prevent something called Dust Spam. Where do these fees go ? Txn fees goes to whoever processes the block that contains the transaction. Additional reward for miners. Very cool !

whichever miner solves the next block gets to include a transaction for 50 BTC to themself from "coinbase."  It turns out that  that if any of the transactions the miner included in your block had a fee attached to it, then the miner gets to include those, too.  Therefore, when a miner solves a block, it typically gets something like 50.75 BTC instead of 50.  The more transactions there were, the more fees received.

If you look at the BTC webpage description about what happens when there's no more rewards for solving blocks, it mentions that they expect the network to be big enough by then that it will be worth solving blocks solely for the fees.  If there are 10,000 transactions per block, at 0.005 per transaction fee, that's 50 BTC in fees.  If BTC really catches on, this is a realistic volume of transactions

transactions fees are also voluntary - a transaction fee will increase the chances that a miner will include your transaction in the block he mines. Actually, a miner  just dump the top few hundred KB of  transactions into a block, sorted by transaction fee (descending, of course). When there aren't many transactions, maybe because of a series of block in a short amount of time, it will be confirmed anyway.


# Do Transactions get lost ?


When you send a transaction, it sends a packet to all connected peers. These peers store the transaction in their in-memory pools and tell all their connections that they have a new transaction. When those connections don't have it yet, they ask for it, and that's how a transaction spreads over the network.

When a user restarts their client, the memory pool is wiped, and the _unconfirmed/unmined_ transaction is deleted from that computer. But it is still available on other clients. it's very unlikely for the transaction to be gone from the entire network.


# **Solving a block **


a [block](https://en.bitcoin.it/wiki/Blocks) is a list of transactions broadcast by the Bitcoin network. This system evolved because of the question "_how do I build a distributed transaction network without a central authority_". What will motivate people to contribute computational and network time to the Bitcoin system ? Well, the chance to make money.

Bitcoin miners act as distributed banks - or more aptly, those irritating credit card salesman who tell you "_please take this credit card_". Each of them is trying to be the eager salesman and be the first to "_process_" your transaction - and the way they do it is solve a puzzle. The process of "_Mining_" is essentially the process of competing to be the next to find the answer that "solves" the current block

The mathematical problem in each block is difficult to solve, but once a valid solution is found, it is very easy for the rest of the network to confirm that the solution is correct.

Miners are essentially putting a notary stamp on a batch of transactions. That's all they are needed for.

But how do you prevent from having a corrupt notary? Bitcoin does this by having tens of thousands of potential notaries and one of them will happen to be the lucky one that gets to do the stamp. The lucky one is the one who happens to solve the problem. All the potential notaries try to solve the puzzle over and over, but it will take about ten minutes for one to become successful.


# Difficulty


Essentially it is a cost function that determines how hard hashing should be so that one block is found every 10 minutes, on average.

    
    Pool difficulty 1 is 0x00000000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF


For every 2016 blocks that are found, the timestamps of the blocks are compared to find out how much time it took to find 2016 blocks, call it T. We want 2016 blocks to take 2 weeks, so if T is different, we multiply the difficulty by (2 weeks / T) - this way, if the hashrate continues the way it was, it will now take 2 weeks to find 2016 blocks.

P.S. 2016 blocks in 14 days = 144 blocks per day. This is **expected difficulty**

The difficulty can increase or decrease depending on whether it took less or more than 2 weeks to find 2016 blocks. Generally, the difficulty will decrease after the network hashrate drops.

If the correction factor is greater than 4 (or less than 1/4), then 4 or 1/4 are used instead, to prevent the change to be too abrupt.

NOTE: There is a bug in the implementation, due to which the calculation is based on the time to find the last 2015 blocks rather than 2016. Fixing it would require a hard fork and is thus deferred for now.

Difficulty should settle around the 70-billion mark, assuming 300 USD/BTC, 0.08 USD/kWh, 1J/GH (with Gen2 ASICs dominating the field).




A bitcoin miner's profit relates to the amount of hashing power they contribute to the network. Since their mining power is constant, their share of the total hashing power decreases relatively when the network's hashing power increases. I.e.


<blockquote>`newProfit = currentProfit * currentDiff/newDiff`.</blockquote>


At a currentProfit of 1BTC/d and a 30% increase in difficulty, they get:


<blockquote>`(1BTC/d)*100/(100+30)= (1BTC/d)/1.3 = 0.76923077 BTC/d`</blockquote>


i.e. their profit decreases by ~23%.


# Network Hashrate - the mathematics of difficulty.


To find a block, the hash must be less than the target. The hash is effectively a random number between 0 and 2**256-1.

    
    <code>hash_rate = (blocks_found/expected_blocks*difficulty * 2**32 / 600)</code>







# Block maturation


Generated coins can't be spent until the generation transaction has 101 confirmations. Transactions that try to spend generated coins before this will be rejected

The purpose is to prevent a form of transaction reversal (most commonly associated with "double spends") if the block is orphaned. If a block is orphaned the coinbase reward(block subsidy + tx fees). "ceases to exist". The coins are produced from the block and when a block is orphaned it is the replacement blocks version of the coinbase tx which is considered valid by the network.

So to avoid that undesirable situation the network requires coinbase tx (rewards to miners) to "mature" or wait 100 confirmations (the client makes this 120 confirmations but only 100 is required by the protocol). If a block is orphaned before it gets 100 blocks deep into the chain, then only the miner is affected.

The referece code that checks this is


<blockquote>

>     
>      // If prev is coinbase, check that it's matured
>                 if (txPrev.IsCoinBase())
>                     for (CBlockIndex* pindex = pindexBlock; pindex && pindexBlock->nHeight - pindex->nHeight < COINBASE_MATURITY; pindex = pindex->pprev)
>                         if (pindex->nBlockPos == txindex.pos.nBlockPos && pindex->nFile == txindex.pos.nFile)
>                             return error("ConnectInputs() : tried to spend coinbase at depth %d", pindexBlock->nHeight - pindex->nHeight);
> 
> 
</blockquote>




# Block Size Limit


Currently, the block subsidy reduces the motivation of miners to include transactions, because 99% of their income comes from the subsidy. Including zero transactions wouldn't impact them greatly.

But when the block reward shrinks, miners may get 99% of their income from transactions. This means they will be motivated to pack as many transactions as possible into their blocks. They will receive the fees, and the rest of the bitcoin network will be burdened with the massive block they created. Without a hard limit on block size, miners will have incentive to include each and every fee-carrying transaction that will fit.

So a single entity benefits, and everyone else shoulders the cost with very little benefit.




# **Blockchain fork and double spending
**


If you understood what a block is, you can ask the question - _what happens if two independent miners find an independent answer to the puzzle of "solving a block"_?

Good question and this is called a blockchain fork - because now there are two ways everyone else can accept what the "_current block_" is. The way this is resolved is that The client accepts the 'longest' chain of blocks as valid. The 'length' of the entire block chain refers to the chain with the most combined difficulty, not the one with the most blocks. This prevents someone from forking the chain and creating a large number of low-difficulty blocks, and having it accepted by the network as 'longest'.

Now, remember that the miners decide which chain is valid by continuing to add blocks to it. The longest block chain is viewed as the valid block chain, because the majority of the network computation is assumed not to come from malicious users.


## - Race conditions


If you wallet accepts incoming peer connections, they can potentially control the information you receive (by flooding your connections). This means that it is possible to _convince_ you about transactions that the larger network is rejecting. So, if you are a Bitcoin accepting merchant, disable your incoming connections and connect to reputed nodes to confirm transactions.

It is worth noting that a successful attack costs the attacker one block - they need to 'sacrifice' a block by not broadcasting it, and instead relaying it only to the attacked node.

There is a variant of this called the _Finney attack_ which needs the collusion of a large miner - unlikely, but still possible.


## - Brute force and >50% attacks


The attacker submits to the merchant/network a transaction which pays the merchant, while privately mining a blockchain fork in which a double-spending transaction is included instead. After waiting for _n_ confirmations, the merchant sends the product. If the attacker happened to find more than _n_ blocks at this point, he releases his fork and regains his coins; otherwise, he can try to continue extending his fork with the hope of being able to catch up with the network. If he never manages to do this, the attack fails and the payment to the merchant will go through.

NOTE: Theoretically someone with massive computational power can create start controlling this, but that is highly unlikely.
