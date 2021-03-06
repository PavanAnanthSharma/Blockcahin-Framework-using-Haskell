## Work in progress

> Sugggested reading order:

- ./examples/scenario-0
- ./src/BC.hs
- ./examples/z-diagrams.org
- ./examples/scenario-1
- ./examples/scenario-2
- ./src/GCoin.hs
- ./examples/scenario-gcoin

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Resources for Haskell:

- Thomas Dietert (adjoint.io) “Building a Blockchain in Haskell”
- https://github.com/tdietert/haskell-blockchain-workshop
      
- Michael Burge
- http://www.michaelburge.us/2017/08/17/rolling-your-own-blockchain.html
- http://www.michaelburge.us/2017/08/31/roll-your-own-bitcoin-exchange.html

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Resources for Python:

- https://hackernoon.com/learn-blockchains-by-building-one-117428612f46
- src : https://github.com/dvf/blockchain

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> Other resources: books/papers

Things I have found useful (suggest in the given order):

Scorex Tutorial

https://github.com/ScorexFoundation/ScorexTutorial
Chapter 2 : Overview of Bitcoin
“Mechanising Blockchain Consensus”

http://ilyasergey.net/papers/toychain-cpp18.pdf
good overview of main data structures and properties
formalization of BC consensus protocol (in Coq)
https://assets.kpmg.com/content/dam/kpmg/pdf/2016/06/kpmg-blockchain-consensus-mechanism.pdf

dated but useful historical survey of consensus mechanisms
Scorex Tutorial

https://github.com/ScorexFoundation/ScorexTutorial
Chapter 3 : A Blockchain System Design
explores design space of BC architecture
“Bitcoin and Cryptocurrency Technologies” (aka “Princeton Bitcoin Book”)

http://bitcoinbook.cs.princeton.edu/
Arvind Narayanan, Andrew Miller, et. al.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## abstract

Blockchain technology seems to be a killer app for functional programming languages, witnessed by companies such as IOHK, Adjoint.IO, Digital Asset, Kadena and Tezos using Haskell and OCaml. But what is a blockchain? This talk will show the development of a simple blockchain in Haskell: elucidating the four main parts: 1) the tamper-evident append-only ledger; 2) the consensus system that decides what entries go into the ledger (and in what order); 3) the peer-to-peer network supporting consensus; 4) the “smart contract” system which interprets what the ledger entries mean (e.g., transfer a coin from Alice to Bob).

The concept of a ledger is built up from simple parts:

A single service receives entries on multiple concurrent channels. Each channel grabs a lock and places their entry into the ledger. This is the beginnings of a ledger but it is not-distributed and it is open to DOS attacks by channels holding the lock too long.
In this step the channels add their entries to a pool. “Miner” threads pick entries from the pool and attempt to add them via compare-and-swap instructions. This avoids the DOS problem in #1 but it is still not-distributed.
Next the system becomes distributed by making the miners into separate nodes on a peer-to-peer network. Network communication will be done via UDP. Consensus among the peers will be achieved via a simple Proof-of-Work mechanism.
Up until this step, the entries on the ledger are just uninterpreted bytes. This step will introduce a simple smart contract language for interpreting those bytes. Initially it will support creating named table entries and incrementing the value associated with the entry. Finally it will show “value” (e.g., coins, property deeds) transfers between named tables entires (i.e., accounts) leveraging public-key cryptography.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Quotes

https://www2.deloitte.com/ch/en/pages/strategy-operations/articles/blockchain-explained.html

Richard Bradley, Director Deloitte

You (a “node”) have a file of transactions on your computer (a “ledger”). Two government accountants (let’s call them “miners”) have the same file on theirs (so it’s “distributed”). As you make a transaction, your computer sends an e-mail to each accountant to inform them.

Each accountant rushes to be the first to check whether you can afford it (and be paid their salary “Bitcoins”). The first to check and validate hits “REPLY ALL”, attaching their logic for verifying the transaction (“Proof of Work”). If the other accountant agrees, everyone updates their file.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

>```0x592eF244F8924be9F3F8803f8d639392f465Ac51 ```










