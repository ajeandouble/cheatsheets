# Blockchain

## Resources

[Block chain books - github.io](https://github.com/BlockchainBooks/blockchainbooks.github.io)

[Soroban - Stellar](https://soroban.stellar.org/)

[Primes and GCD - youtube](https://www.youtube.com/watch?v=Dorm0_UyKFw)

[But how does bitcoin actually works? - 2blue1brown - youtube](https://www.youtube.com/watch?v=bBC-nXj3Ng4)

[The Bitcoin Whitepaper - RedBlockBlue - youtube](https://www.youtube.com/watch?v=NoqNhWnjE1Q)

[coinhouse.com](https://coinhouse.com)


## Math

### Infinite number of primes

>Let `N = {P0 * P1..., * Pn}` an hypotetical list of all finite prime numbers.
>
>Then `N + 1 = (P0 * P1... * Pn) + 1`
>
>Hence `N + 1` can't be divided by any of the previous P numbers since the division would always yield the remainder `r = 1`.
>
>So there is always a Prime number that can be constructed from this finite list.
>
>Hence it's not finite.

### Euclid's GCD Algorithm

`TODO`

### SHA-256

[SHA 256 specifications - NIST](http://csrc.nist.gov/publications/fips/fips180-2/fips180-2withchangenotice.pdf)

[How secure is SHA-256? - 2blue1brown - youtube](https://www.youtube.com/watch?v=S9JGmA5_unY)

## History

### DigiCash/eCash

>Founded by David Chaum in 1989, DigiCash was a company that facilitated anonymous digital payments online. Chaum is the inventor of blind signature technology, which proposed using cryptography to protect the privacy of payments online. DigiCash ultimately filed for bankruptcy in 1998.

[Mastering Blockchain - Lorne Lantz & Daniel Cawrey](https://www.amazon.fr/Mastering-Blockchain-Cryptocurrencies-Decentralized-Applications-ebook/dp/B08NFLQ2QL/)

[Blind Signature (1982) - David Chaum](https://www.youtube.com/watch?v=DDsQCcuST6c)

#### Blind Signature explained

`TODO`

## History

### Hashcash

>Invented by Adam Back in 1997, Hashcash introduced the idea of using proof-of- work to verify the validity of digital funds, including the concept of money that exists solely on the internet. Hashcash used cryptography to enable proof-of-work, and Back proposed using an algorithm called SHA1 in order to accomplish this. In his initial proposal for Hashcash, Back referenced DigiCash and raised the idea that adding a fee or “postage” on emails with digitized currency could reduce spam. By utilizing a hash, or a function requiring computer processing, Hashcash would impose an economic cost, which would limit spam in email systems.

### BMoney

>Proposed by Wei Dai in 1998, B-Money introduced the concept of using computer science to facilitate monetary creation outside of governmental systems. Like Hash‐ cash, B-Money suggested that digital money could be produced through computa‐ tion, or proof-of-work. Similar to Adam Back, Wei proposed that the cost of creating digital money could be calculated from the computer power used to create it. This digital money would be priced based on a basket of real-world assets such as gold and other commodities and limited in its supply to protect it from inflation, or losing value over time.

### Bitcoin

>On August 18, 2008, the domain `bitcoin.org` was registered. Then, written by some‐ one or a group using the pseudonym Satoshi Nakamoto, a whitepaper was published on October 31, 2008, and shared on numerous software developer mailing lists. Titled “Bitcoin: A Peer-to-Peer Electronic Cash System,” the paper provided a detailed pro‐ posal for creating a value system that existed only on the internet.

>The Bitcoin proposal featured a number of ideas pulled from systems that preceded it. These included:
>
> • Secure digital transactions, like the smart contracts outlined by Nick Szabo
>
>• Using cryptography to secure transactions, like in DigiCash
>
>• The theoretical ability to send small amounts of secured value, as E-gold was able to do
>
>• The creation of money outside of governmental systems, as B-Money had proposed
>
>• Using proof-of-work to verify validity of digital funds, as Hashcash was designed to do

[bmoney paper - eskimo.com](https://web.archive.org/web/19990219124653/http://www.eskimo.com/~weidai/bmoney.txt)


## Definitions and concepts

### Blockchain

**Blockchain** is a decentralized and distributed ledger technology that records transactions across a network of computers. It uses cryptographic techniques to create a chain of blocks, ensuring transparency, security, and immutability of transaction data. Blockchain is the underlying technology for many cryptocurrencies, providing a tamper-resistant and transparent record of digital transactions.

#### Implementation in Bitcoin

[Bitcoin - A Peer-to-Peer Electronic Cash System - Satoshi Nakamoto original paper](https://bitcoin.org/bitcoin.pdf)

1. **Block Header:** Each block in the Bitcoin blockchain has a header containing various pieces of information, including the previous block's hash, a timestamp, a nonce (number used only once), and the Merkle root of the transactions in the block.
2. **Mining Process:** Miners compete to find a valid nonce that, when combined with the other information in the block header, produces a hash that meets certain criteria. This criteria involve the hash being below a target value, which is dynamically adjusted by the network to maintain an average block time of approximately 10 minutes.
3. **Difficulty Adjustment:** The Bitcoin network adjusts the difficulty level approximately every two weeks (2016 blocks) based on the total computational power of the network. If blocks are being mined too quickly, the difficulty increases; if too slowly, it decreases. This adjustment aims to maintain a relatively constant rate of block production.
4. **Finding a Valid Block:** Miners iterate through possible nonce values to find a hash that meets the difficulty criteria. The process involves significant computational work, as changing even a single bit in the input (such as the nonce) drastically alters the resulting hash.
5. **Proof of Valid Work:** Once a miner finds a valid nonce and produces a hash below the target, they broadcast the new block to the network. Other nodes in the network can quickly verify that the miner has performed the required computational work by checking the hash against the difficulty criteria.
6. **Block Addition to the Blockchain:** The new block is added to the blockchain if it is accepted by the majority of the network. This process creates a chronological and unalterable chain of blocks, with each block containing a reference to the previous block's hash, forming the blockchain.
7. **Incentives:** Miners are rewarded with newly minted bitcoins (block reward) and transaction fees for successfully mining a block. This economic incentive encourages miners to invest computational power and compete to find valid blocks.

### Double-spending problem

The **double-spending** problem refers to the challenge in digital currencies where the same unit of currency can be spent more than once due to the ease of replicating digital information. It is a critical concern in electronic transactions as there is a risk of fraudulent or unauthorized spending.

#### Example scenario

1. **Initiating the Attack:** Alice possesses 1 BTC and initiates a transaction to purchase goods from both Bob and Charlie simultaneously.
2. **Creating two transactions:** Alice quickly creates two separate transactions: one to pay Bob 1 BTC and another to pay Charlie the same 1 BTC.
3. **Broadcasting Transactions:** Alice broadcasts both transactions to the Bitcoin network almost simultaneously. Since the network has not had time to confirm either transaction, they are both in a pending state.
4. **Double-Spending Attempt:** Bob and Charlie both see the pending transactions and release the purchased goods, assuming the transactions will be confirmed. However, since Alice initiated a double spend, only one of the transactions will eventually be confirmed.
- **Outcome:** If the transaction paying Bob is confirmed in one block, and the transaction paying Charlie is confirmed in another block, Alice effectively receives the goods from both Bob and Charlie while only spending 1 BTC.

#### Bitcoin mitigation

- **Transaction Confirmation:** Bitcoin transactions require confirmation by miners. As new transactions are broadcast to the network, miners include them in candidate blocks. The network reaches consensus on which block is added to the blockchain through the proof-of-work process. Multiple confirmations (blocks added after the one containing the transaction) make the transaction more secure.
Prevention of Double Spending:
- When a user attempts to double spend by creating conflicting transactions, **the decentralized network** works to reach consensus on the valid transaction.
- **The proof-of-work** mechanism ensures that the majority of the network agrees on the transaction history, making it extremely difficult for an attacker to manipulate.
- **Incentives and Game Theory:** Miners are economically incentivized to follow the rules of the network and include valid transactions in blocks. Attempting double spending would require controlling a significant portion of the network's computational power, which is economically infeasible.

### Layers

[What is blockchain layer 0, 1, 2, 3 explained - medium](https://medium.com/@learnwithwhiteboard_digest/what-is-blockchain-layer-0-1-2-3-explained-56226d4bb2cd)

- **Layer 0:** Underlying infrastructure of the blockchain such as internet, its protocols and telecomunication system.
- **Layer 1:** The foundational layer of the blockchain technology stack. The main blockchain and its protocols.
- **Layer 2:** On top of layer 2, solutions that are additional protocols like the *lighting* network. It integrates the blockchain with other systems and protocols.
- **Application layer:** User interfaces, mobile and web applications, etc.

### Stablecoin

>Stablecoins use algorithms and smart contracts to dynamically adjust the supply based on demand and market conditions. The goal is to maintain a stable value without relying on explicit collateral. Ampleforth (AMPL) 

## Bitcoin Lightning

>The Lightning Network is a second-layer scaling solution for the Bitcoin blockchain, designed to address some of the limitations of the main Bitcoin network, such as scalability and transaction speed. It aims to enable faster and cheaper transactions by conducting most transactions off-chain.

>The Lightning Network relies on the concept of payment channels. These are essentially private channels established between two participants, allowing them to transact off-chain.

>Once the payment channel is established, participants can conduct an unlimited number of off-chain transactions. They are cheaper and have lower fees compared to the blockchain transactions.

### Multi-signature wallets

>To create a payment channel, participants commit a certain amount of Bitcoin to a multi-signature wallet. The initial distribution of funds is recorded on the Bitcoin blockchain.

>One of the key BIPs related to multi-signature functionality is BIP-0016, titled "Pay to Script Hash (P2SH)." BIP-0016 proposed a new standard for the encoding of Bitcoin addresses, which allowed the use of more complex scripts, including multi-signature scripts.

### Off-chain transaction

>Participants can perform an unlimited number of off-chain updates by exchanging commitment transactions between themselves. These transactions reflect the evolving state of the payment channel, with changes in the allocation of funds.
Each new commitment transaction is signed by both parties and replaces the previous one. The latest commitment transaction reflects the most recent agreement on the distribution of funds within the channel.

1. **Channel setup:** Multiple users create a payment channel between them. They bootstrap the channel by adding funds with a transaction on the block-chain.
2. **Off-Chain transactions:** These transactions are not broadcast to the entire network and don't appear in the main blockchain.
3. **Payment channel updates:** The users exchange updated commitment transactions.
4. **Revocation Mechanism:** Everytime a new commitment transaction is created, a corresponding revocation key is exchanged. It can be used to rollback the channel to a favorable state.
5. **Closing the channel (On-chain):** Users can close the channel in case of dispute. They can broadcast their last commitment transaction on the main blockchain.


## Bitcoin scripts

>Bitcoin scripts are a fundamental part of the Bitcoin protocol, and they are responsible for defining the conditions under which a transaction output can be spent. In essence, Bitcoin scripts are simple programs written in a non-turing-complete scripting language that determine the rules for unlocking and spending Bitcoin.


## Ripple

>Ripple introduced a new type of consensus known as the XRP Consensus Protocol. It uses Byzantine fault- tolerant agreement, which requires nodes to come to agreement on transactions.

[Byzantine fault - wikpedia](https://en.wikipedia.org/wiki/Byzantine_fault?useskin=vector)


## Ethereum

### DAO's hack

[the dao hack - ethereum](https://www.gemini.com/cryptopedia/the-dao-hack-makerdao)


## Stellar

>In 2014, Jed McCaleb, founder of Mt. Gox and co-founder of Ripple, launched the network system Stellar with former lawyer Joyce Kim. The nonprofit Stellar Development Foundation was created in collaboration with Stripe CEO Patrick Collison and the project officially launched that July.

[Stellar (payment network) - Wikipedia](https://en.wikipedia.org/wiki/Stellar_(payment_network))

>The Stellar network reaches consensus using the Stellar Consensus Protocol (SCP), which is a construction of the Federated Byzantine Agreement (FBA). FBA differs from other well-known consensus mechanisms like Proof of Work (which relies on a node’s computational power) and Proof of Stake (which relies on a node’s staking power) by instead relying on the agreement of trusted nodes.

[Fundamentals and concepts - stellar.org](https://developers.stellar.org/docs/fundamentals-and-concepts/stellar-consensus-protocol)

[SCP - youtube](https://www.youtube.com/watch?v=vmwnhZmEZjc])

[Engineering Talks - Intuitive Stellar Consensus Protocol - youtube](https://www.youtube.com/watch?v=fDt8Eh4T_lE)

### Concepts

#### Stellar ledger

>A ***ledger*** represents the state of the Stellar network at a point in time. It is shared across all Core nodes in the network and contains the list of accounts and balances, orders on the distributed exchange, smart contract data, and any other persisting data.

>***Other blockchains refer to this concept as a "block", and the entire blockchain as "the ledger".***


#### Networks


>Stellar has three networks: the public network (Mainnet, also called Pubnet or the Public Network), the test network (Testnet), and a dev network (Futurenet). Mainnet is the main network used by applications in production. It connects to real financial rails and requires XLM to cover minimum balances, transaction fees, and rent. The Testnet is a smaller, free-to-use network maintained by SDF that functions like the Mainnet but doesn’t connect to real money. It has a built-in testnet XLM faucet (called Friendbot), and it resets on a regular cadence, so it's the best place for developers to test applications when they need a stable environment that mirrors Mainnet functionality. Futurenet is a dev network you can use to test more bleeding edge features that also has access to its own Friendbot. It resets whenever a reset is necessary, so it's not as predictable as Testnet, but it is where new features may be introduced before the are implemented in stable releases.

[Fundamentals and concepts - Stellar](https://developers.stellar.org/docs/fundamentals-and-concepts/networks)

#### Trustlines

>Trustlines in the Stellar network are a mechanism that allows accounts to explicitly declare which assets they are willing to accept or hold. These trustlines establish a line of trust between two parties, enabling the transfer and exchange of assets issued on the Stellar network.

>A trustline entry contains information about the asset, including the asset's code (e.g., USD for US dollars) and the issuer's account ID. It also includes the limit or maximum amount of the asset that the account is willing to hold.

### Token issuance

#### Anchors

### Soroban

[What is soroban? - thedefiant.io](https://thedefiant.io/what-is-soroban)

Soroban is a smart contract platform that boosts *Stellar*’s capabilities as a borderless payments network. It was founded in 2015.


## TO DO

- Futurenet
- WebASM
- Solidity
-Government-backed currencies use the familiar mint-based model, in which a central authority, known as a mint, verifies that transactions cannot be double-spent. Cur‐ rency is returned to the mint and is periodically destroyed in order to create new currency.
The Bitcoin whitepaper proposed eliminating that mint-based central authority by publishing each and every transaction on a digital-only network: