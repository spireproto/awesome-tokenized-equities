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

- **[production]** [Robinhood Chain Stock Tokens](https://robinhoodchain.blockscout.com) - tokenized US equities on chain 4663. Corporate actions through an ERC-8056 multiplier: raw balances stay static, the shares-per-token ratio moves. 194 genuine wrappers by bytecode as of August 2026.
- **[production]** [Backed / xStocks](https://backed.fi) - collateralised tracker certificates on Solana and EVM chains. Dividends handled by rebase, net of US withholding.
- **[production]** [Dinari](https://dinari.com) - SEC-registered transfer agent issuing dShares. Dividends paid in USDC rather than accrued, which makes them the easiest of the three to reconcile.
- **[beta]** [Ondo Global Markets](https://ondo.finance) - tokenized equities and ETFs with a broker-dealer wrapper.
- **[beta]** [Swarm](https://swarm.com) - regulated tokenized stocks and bonds, BaFin-licensed venue.

## Standards

- **[production]** [ERC-8056 Scaled UI Amount](https://eips.ethereum.org/) - a multiplier adjusts displayed amounts while `balanceOf` and `totalSupply` stay fixed. Explicitly not a rebase; integrators opt in. The design chain 4663 uses.
- **[production]** [ERC-1400 Security Token Standard](https://github.com/ethereum/EIPs/issues/1411) - partitioned balances plus transfer restrictions. The older, permissioning-first approach.
- **[production]** [ERC-3643 (T-REX)](https://www.erc3643.org) - on-chain identity and compliance for permissioned securities.
- **[experimental]** [ERC-7726 / oracle composition notes](https://eips.ethereum.org/) - relevant because applying a UI multiplier on top of a price that already includes it is the most common integration bug in this category.

## Chains

- **[production]** [Robinhood Chain](https://robinhoodchain.blockscout.com) - chain id 4663, block 1 dated 30 April 2026. Purpose-built for the issuer's stock tokens.
- **[production]** [Solana](https://solana.com) - where xStocks has the deepest tokenized-equity liquidity.
- **[production]** [Base](https://base.org) - Dinari dShares and several ETF wrappers.

## Corporate actions

The part that actually differs between products.
