# International Token Identification Number (ITIN) - Technical Specification

## Versioning

| Version | Release Date | Comments                         |
|---------|--------------|----------------------------------|
| 1.0     | TBD          | Initial release                  |

## Authors

ITSA PWG1 Members

## Summary

The token economy has gained significant momentum. As of today, an ecosystem of more than 5,100 publicly traded crypto tokens and over 245,000 Ethereum token contracts has emerged. However, due to the lack of holistic market standards, this wave of new tokens may confront market participants with ambiguity and uncertainty, exposing retail investors to avoidable risks and deterring institutional funds. Acknowledging the market‘s need for more standardization in order to grow and mature, the International Token Standardization Association e.V. (ITSA) has developed the International Token Identification Number (ITIN) as a unique identifier, which covers all Blockchain-based cryptographic tokens, regardless of their status as security, their fungibility or tradability. But any identifier needs a strong foundation that copes with the particularities of the ecosystem it is intended for. To build a strong and sustainable foundation for the ITIN and to consider the characteristics peculiar to the decentralized world, ITSA is introducing the Uniform Token Locator (UTL). The UTL is a novel identification and referencing standard capable of uniquely identifying all types of tokens across different ledgers and is resilient to chain splits. Just like information on the World Wide Web (WWW) is identified by a Uniform Resource Locator (URL), tokens are identified and located through the UTL. ITSA maintains a register on how to map UTLs to ITINs. Other organizations can also use the UTL and map it to their shortened identifier.

## Design Principles

We here define the very design principles on which we build throughout this document and when defining the ITSA token identification standard.

### Principle 1: Blockchain-based tokens

The identification standard considers tokens as digital assets that are defined by a blockchain system.

Hence, the standard explicitly excludes tokens that are defined by other Distributed Ledger Technologies (DLTs) such as a Directed Acyclic Graph-based DLT.

### Principle 2: Identification of technical tokens

The identification standard provides a solution for the identification of technical tokens defined by a blockchain system. 

The standard does not attempt to identify nor describe or classify any underlying asset that is referenced by the token.

### Principle 3: Universal application

The identification standard can be applied to all relevant use cases. 

In particular, the standard supports the following use cases
the identification of tokens on different blockchain systems
the identification of fungible and non-fungible tokens

### Principle 4: Fork-resilient

The identification standard is resilient against  blockchain forks. That is, the standard accurately attributes a token to a specific fork of the same blockchain system.

### Principle 5: Static identifier

The identification standard provides a static identification number that references a token. 

This number can be used to e.g. reference a token in static documents, databases or messages in third-party protocols.

### Principle 6: Open 

The identification standard constitutes an open set of definitions that do not require a central authority for the issuance or interpretation of an identifier.

## Terms & Notations

Throughout this document we will build on the vocabulary of terms and definitions as promulgated in the [ISO:22739:2020 standard [1]](https://www.iso.org/obp/ui/#iso:std:iso:22739:ed-1:v1:en). However, while the referenced ISO standards cover DLT in general, the concepts developed in this document are currently applicable to distributed ledgers implemented as a blockchain only. As a result, when applying ISO definitions referring to DLT in general we shall in this document assume the narrower class of blockchain technologies instead.

We consider a blockchain system `S={C(t), N, M}S={C(t), N, M}` with blockchain C(t)C(t), a set of nodes `N={n1,n2, …}N={n1,n2, …}` connected by a peer-to-peer communication protocol and synchronized using a consensus mechanism MM.

At any time `t`, blockchain `C(t)` is defined by a set of confirmed blocks `B={b0, b1, b2,. . . ,bi}` which are connected using cryptographic links. The genesis block b0 marks the very first confirmed block in a blockchain such that `C(0) = b0`. A block bi on blockchain system S can be unambiguously identified through its block hash `H(bi)` which is the block’s respective hash value. That is, for any two blocks bi and bk on blockchain system `S` we have that if `i != k` then `H(bi) != H(bk)`. New blocks are created by nodes `ni` and appended to `C` if and only if they are confirmed through consensus of all nodes `N` applying `M`. Thereby, any blockchain `C` forms final, definitive and immutable ledger records.

Accounts `A={a1,a2,...}` on a blockchain system `S` are representations of entities that initiate or are involved in transactions `txi`. Note that we do not directly relate an account to a single public key or private key but allow 1-to-n and n-to-1 relationships. In fact, an account is rather defined as the units through which entities are able to interact on a blockchain system through their involvement in transactions. Thereby, these entities may be able to control multiple accounts with the same private key or an account may only be controlled through multiple private keys (possibly held by different entities). We continue assuming that any account `ai` can be unambiguously identified within `S` through its (account) address. More specifically, for any two accounts `ai` and `ak` on blockchain system `S` and with addresses `di` and `dk` it holds that if `i != k` then `di != dk`.

smart contracts `SC` are computer programs stored in a blockchain system `S` where the outcome of executing the smart contract (or a specific function thereof) may lead to an update of the blockchain `C`. Such a smart contract is always created under a specific account `ai` which we refer to as the contract creating account.

Turning to the concept of a token, we apply the very generic ISO definition according to which a token is a “digital asset that represents a collection of entitlements” [1]. For the purpose of this document this definition shall include cryptocurrencies, colored coins, utility tokens, security tokens and more generally all kinds of fungible, non-fungible, and hybrid tokens. A new token may be created with and defined by a smart contract but this does not necessarily have to be the case. However, a new token is always created from a specific account `ai` which we denote the token creating account and the respective account address the token address `di`. In general, a token creating account and a specific token are related by a 1-to-many relationship indicating that multiple tokens may be created under a single token creating account. As a result, tokens do not have unique token addresses. We shall thus assume that at its creation a token symbol `mi` is assigned to the token that is unique for all tokens created under a specific token creating account. Hence, a token may be identified by the combination of its token address and token symbol or the tuple `(di, mi)`, respectively.

Furthermore, a token may be divided into a number of interchangeable units such that we call the token a fungible token. Or, a token may represent a collection of individual digital assets each with its distinct characteristics and entitlements in which case the token is called a non-fungible token. In order to identify individual assets in a non-fungible token those are associated with a sub-identifier `ui`, the token sub-address, such that the combination of token address, symbol and sub-address or the triple `(di, mi, ui)`, respectively, serves as identifier.

So far we have considered a blockchain system `S` to evolve only by adding new confirmed blocks to the blockchain `C` through nodes `N`. An alternative scenario for how `S` may evolve is if the consensus mechanism `M` is updated leading to new rules for how the nodes reach consensus over whether a new block is confirmed or not. More generally, we speak of a blockchain fork if at a given time `t’` a blockchain system `S` is changed leading to a new blockchain system `S’={C(t’), N’, M’}`. Note that the set of nodes `N’` may include nodes applying the old consensus mechanism `M` as well as other nodes using `M’`. Thereby, a soft fork leads to a new blockchain system in which new blocks created by nodes using `M’` are also accepted by nodes using `M`. On the other hand, the fork constitutes a hard fork if blocks created using `M’` are not accepted by nodes using the old consensus mechanism `M`.

After a fork a blockchain system can split into two independent systems `S` and `S’` which share the same blockchain `C` up to time `t’` but maintain different blockchains `C` and `C’` thereafter. In other words, the two blockchains `C` and `C’` share the same history but evolve individually after `t’`. Hence, `S(s) = S’(s)` for any time `s <= t’` but `S(u) != S’(u)` for times `u > t’`. As a result, a token created under a certain token creating account on blockchain system `S` at time `s` is replicated on blockchain system `S’` after it splits from `S` at time `t’`. Obviously this leads to a duplication of the token making its token address unfit as an identifier.

## Specification

We have seen in the previous section that the unambiguous identification of a token in a blockchain system `S` is not trivial. This problem is even more challenging in an environment where the underlying blockchain system may fork and split over time. At the same time, safe and efficient token markets rely on a static token identification number. We therefore propose a token identification standard that builds on two components: a Universal Token Locator (UTL) that dynamically locates the token and the blockchain hosting it (1) and an International Token Identification Number (ITIN) that serves as a static identifier referencing a specific token (2).

### Universal Token Locator (UTL)

Consider a blockchain system S that defines an arbitrary number of tokens each with token address di, token symbol mi, and for non-fungible tokens sub-address ui. Assume that the system S may fork and split at any time. Furthermore, we assume that a split S’ of that blockchain system can be created by anyone and anytime such that we may not be aware of all chain splits at a certain time t.

We are interested in locating a token on that blockchain system and across all observed and unobserved splitted systems S’. We therefore define a multi-data point identification scheme based on the data-points in the following table.

| Identification Point | Abbr. | Mode     | Description |
|----------------------|-------|------    |-------------|
| Genesis Block Hash   | GBH   | Required | The hash of the genesis block `b0` of blockchain `C` in blockchain system `S` |
| Post Fork Block Hash | FBH   | Required | The hash of the block `bi` of blockchain `C` in blockchain system `S` following immediately after an observed fork. If no fork has been observed so far the GBH is used. |
| Recent Block Hash    | RBH   | Required | The hash of a recent block `bj` of blockchain `C` in blockchain system `S`. With each update of the FBH the RBH is also updated. |
| Token Address        | TAD   | Required | The token address `di` of the token to be located. For the location of a native token the `0x000…` address is used. |
| Token Symbol         | TSY   | Optional | The token symbol `mi` of the token to be located. For the location of a native token this field may also be blank. |
| Token Sub-address    | TSA   | Optional | The token sub-address `ui` of the individual digital asset under a non-fungible token contract to be located. For the location of fungible tokens this field is left blank. |

Note that the recent block `b(t)` changes dynamically with time `t` such that at time `T, T>t, b(T) != b(t)`. Hence, the respective token identifier may be “accurate” at time `t` but outdated at time `T`. With block times being a small number of seconds this potentially requires a frequent updating of the RBH and, thus, the UTL.

### International Token Identification Number (ITIN)

The ITIN builds the second component for the unambiguous identification of tokens. The main feature of the ITIN is that it is a static identification number that remains associated with a distinct token even when its UTL changes due to e.g. a chain-split and the subsequent duplication of the token or it’s token address, respectively. Thereby, the ITIN may be embedded in static resources for the consistent referencing of a token.

The ITIN is defined as a 9-digit character sequence consisting of two components

ITIN := [XXXX-XXXX]-[Y]

where the components are defined in the following table.

Sequence
Component
Description
[XXXX-XXXX]
Token ID
The Token ID is a unique identifier that is randomly generated for each token as follows:

X is an alphanumeric capital character
Excluding the letters “I”, “L” and “O” as well as the numbers “0” and “1” to eliminate the risk of a potential confusion
Generated and assigned at random
ITINs containing real words like “coin” or “bits” are eliminated for maximum fairness

Hence, 10-2=8 numeric characters and 26-3=23 alphabetic characters are available allowing for the distinct identification of 31^8 > 850 billion tokens.
[Y]
Checksum
Y is a single-digit number calculated by taking the modulo of the sum of ASCII code values for the positions 1-8 of the Token ID and a reassignment of the ASCII code to the numeric result.

Recalculation of the checksum allows market participants to verify the correct communication of the identifier and, hence, the Checksum serves as a built-in security feature.

## Fork Guidelines

As discussed previously, blockchains regularly fork, sometimes causing chain splits and two individual blockchain systems S and S’ such that C(s)=C’(s) for times s<t where t is the time of the chain split. As a result, post-fork the identifier for a token on that blockchain system needs to be updated. For this update clear governance rules have to be defined. Specifically, (1) what is updated, (2) how is it updated, and (3) by whom is it updated. 

In this section we outline the governance framework for updating the token locator UTL and identifier ITIN upon an observed blockchain fork.

### UTL Updating Rules

#### Rules for Post-Fork Block Hash

The Post-Fork Block Hash is updated upon every fork that leads to a sustainable chain split.

A sustainable chain split is a chain split that leads to two parallel chains continuing for at least M blocks.

The ITSA oversight committee reviews and updates if necessary from time to time and possibly for different blockchain systems individually the number of blocks M.

#### Rules for Recent Block Hash

The Recent Block Hash is updated every N blocks.

The ITSA oversight committee reviews and updates if necessary from time to time and possibly for different blockchain systems individually the number of blocks N.

Note, the updating rules for the Recent Block Hash imply that between any two updates of the RBH at most N undetected forks duplicating a token may have occurred. In other words, the likelihood that the UTL is pointing to the token it should identify is bounded by p=1/N. As an example, if N=100 then there exist 100 potential events that an undetected fork has occurred or a likelihood of 1% for no such fork. This may help define an appropriate value for N given the accepted level of uncertainty attached to the UTL for a blockchain system.

### ITIN Assignment Rules

Other than the UTL, the ITIN is a static identifier for a specific token. As such, the ITIN for a token does not change over time and, in particular, upon blockchain forks and subsequent chain splits. However, a chain split effectively creates two parallel blockchain systems S and S’ which share the same history in terms of blockchains C and C’ and, thus, duplicate all tokens in existence previous to the chain split. Hence, the ITIN Assignment Rules essentially govern how existing ITINs are associated with, and new ITINs are created for, the original and duplicate tokens.

#### Relevant Chain Splits

The ITIN Assignment Rules apply upon a new sustainable chain split.

#### Identification of the Continuing Blockchain System

In a chain split the continuing blockchain system S is defined as the blockchain system that economically and/or legally represents the continuation of the original, pre-chain split, system.

The continuing blockchain system S is identified as this post-chain split blockchain system for which:
a public consensus exists about its economic and/or legal succession of the original system
the fork choice rule (e.g. heaviest chain) of the unforked S leads to a higher score. This is only applied if the fork choice rule is not modified in the forked system.
the fork that did not update the consensus rules is considered the continuing blockchain system.
In cases where
(i) the fork choice rule has been modified, an effort is made to translate the semantics of the rule. If that’s not possible this criteria is omitted
(ii) the blockchain system that is supported by the fork choice rule does not keep its initial name, symbol and/or website, 
(iii) the original blockchain system’s community appears not to be correctly represented by the blockchain system identified by the fork choice rule,
the ITIN oversight committee will decide upon which blockchain system to use as the continuing system.

The alternative blockchain system S’ is defined as the blockchain system that is not considered the continuing system in a chain split.

Note, in general sustainable chain splits follow extensive public discussions among the community and/or key stakeholders along the course of which a consensus is established of which is to be considered the continuing and the alternative blockchain system. As such the identification of the continuing blockchain system is unproblematic according to the decision rule (1).

#### Association of Existing ITINs

The association of existing ITINs with the token defined by either the continuing (S) or alternative (S’) blockchain system is governed by the following decision tree:

If a token issuer exists and if this issuer, or an authorized representative, has filed a valid request for Association of ITIN Upon Blockchain Split then this request will define the association of ITIN with the token.
Otherwise, the existing ITIN remains associated with the tokens defined by the continuing blockchain system S.

#### Creation of New ITINs

The native token defined by the alternative blockchain system S’ receives a new ITIN.

A new ITIN is assigned to non-native tokens defined by the alternative blockchain system S’ only upon request.

## Limitations

to be added?

## References

[1] https://www.iso.org/obp/ui/#iso:std:iso:22739:ed-1:v1:en