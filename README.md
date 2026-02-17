# Awesome Tokenized Equities [![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re)

> A curated list of tokenized equity issuers, standards, venues, tooling and
> research - with a maturity tag on every entry.

Tokenized equities are a real market with several incompatible designs sitting
under the same words. One share can be a rebasing token in one place, a
multiplier in another, and a stablecoin payment in a third. This list is
organised so those differences are visible rather than flattened.

## Maturity tags

Every entry carries one. They describe **how much of the thing is load-bearing
today**, not how good it is.

| Tag | Meaning |
| --- | ------- |
| **[production]** | Live with real assets, real users, public track record |
| **[beta]** | Live, limited scope or limited jurisdictions |
| **[experimental]** | Testnet, prototype, or spec ahead of implementation |
| **[research]** | Written work, no implementation claimed |

## Contents

- [Where do I start?](#where-do-i-start)
- [Issuers](#issuers)
- [Standards](#standards)
- [Chains](#chains)
- [Corporate actions](#corporate-actions)
- [Tooling](#tooling)
- [Data and explorers](#data-and-explorers)
- [Research](#research)
- [Contributing](#contributing)

## Where do I start?

Three steps, in order, if the subject is new to you.

1. **Understand that "tokenized share" is not one thing.** Read
   [Corporate actions](#corporate-actions) first. The dividend method is what
   actually distinguishes these products, and it is the part marketing pages omit.
2. **Pick one issuer and find its real contract.** Not by ticker: by bytecode.
   [erc8056-checks](https://github.com/usestockledger/erc8056-checks) does it for
   Robinhood Chain in one command, and the exercise is more instructive than any
   overview.
3. **Replay a corporate action yourself.** One `eth_getLogs` returns the entire
   history of chain 4663. Fifteen events. Read them absolutely, then read them as
   compounded deltas, and note that the answers differ.

## Issuers
