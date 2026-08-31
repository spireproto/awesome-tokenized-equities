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
- [Clearing and settlement](#clearing-and-settlement)
- [Tooling](#tooling)
- [Data and explorers](#data-and-explorers)
- [Research](#research)
- [Contributing](#contributing)

## Where do I start?

Three steps, in order, if the subject is new to you.

1. **Understand that "tokenized share" is not one thing.** Read
   [Corporate actions](#corporate-actions) first. The dividend method is what
   actually distinguishes these products, and it is the part marketing pages omit.
2. **Measure a chain instead of reading its documentation.**
   [spire-checks](https://github.com/spireproto/spire-checks) does chain 4663 in
   one command with no key. It is also how the block time in our own published
   table was found to be wrong by a factor of twenty, which is the more useful
   lesson.
3. **Replay a corporate action yourself.** One `eth_getLogs` returns the entire
   history of chain 4663. Fifteen events. Read them absolutely, then read them as
   compounded deltas, and note that the answers differ.

## Issuers

- **[production]** [Robinhood Chain Stock Tokens](https://robinhoodchain.blockscout.com) - tokenized US equities on chain 4663. Corporate actions through an ERC-8056 multiplier: raw balances stay static, the shares-per-token ratio moves. 194 genuine wrappers by bytecode as of August 2026.
- **[production]** [Backed / xStocks](https://backed.fi) - collateralised tracker certificates on Solana and EVM chains. Dividends handled by rebase, net of US withholding.
- **[production]** [Dinari](https://dinari.com) - SEC-registered transfer agent issuing dShares. Dividends paid in USDC rather than accrued, which makes them the easiest of the three to reconcile.
- **[beta]** [Ondo Global Markets](https://ondo.finance) - tokenized equities and ETFs with a broker-dealer wrapper.

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

| Issuer | Dividend method | Holder sees | Reconcilable from chain alone |
| ------ | --------------- | ----------- | ----------------------------- |
| Robinhood | Multiplier accrual | Balance unchanged, ratio rises | Partially: the log exists, the entitlement record does not |
| xStocks / Backed | Rebase, net of 30% withholding | Balance rises | Partially |
| Dinari | USDC payment | Stablecoin arrives | Yes, it is a transfer |

- **[production]** [Robinhood Chain Blockscout logs](https://robinhoodchain.blockscout.com) - one `eth_getLogs` from block zero returns every corporate action the chain has recorded. Read them absolutely, then as compounded deltas, and note that the answers differ.

Nothing here indexes corporate actions as a service. Read the log yourself, and be
careful with duplicate payloads: the chain does not mark which of two identical
entries is a correction.

## Clearing and settlement

Tokenized equities settle by prefunding: the asset and the cash are both in place
before the trade, so nothing is ever owed. It works, and it is paid for in capital
that has to sit still. This section is for the work on the alternative.

- **[experimental]** [Spire Protocol](https://github.com/spireproto/spire) - clearing layer for chain 4663: novation, netting inside a 300s window across venues, collateral instead of prefunding, and a default waterfall fixed in advance. Specification complete, nothing deployed.
- **[experimental]** [spire-contracts](https://github.com/spireproto/spire-contracts) - clearing house, collateral vault, settlement engine, default fund, solvency registry and governor as interfaces, published ahead of the implementation.
- **[production]** [spire-checks](https://github.com/spireproto/spire-checks) - zero-dependency scripts that measure chain 4663 and check published parameters against it, including ours.
- **[research]** [netting-replay](https://github.com/spireproto/netting-replay) - 33 modelled trading days through those netting rules. Compression ranges from 8.3% to 47.8%, which is the point: it is a property of flow, not of a protocol.
- **[research]** [Prefunding, and what it actually costs](https://github.com/spireproto/spire/blob/main/docs/overview.md) - why a market maker's capital requirement is the cartesian product of the venues it quotes on rather than its net risk.
- **[research]** [CPMI-IOSCO Principles for Financial Market Infrastructures](https://www.bis.org/cpmi/publ/d101.htm) - the document every off-chain clearing house is built against. Principles 4, 7 and 13 are the ones an on-chain design has to answer.

## Tooling

- **[experimental]** [@spireproto/core](https://github.com/spireproto/spire-core) - windows, novation, netting, margin, collateral and waterfall arithmetic. BigInt, zero dependencies, 55 tests. Not published to npm; install from the repository.
- **[experimental]** [@spireproto/sdk](https://github.com/spireproto/spire-sdk) - clearing client with EIP-712 signing, keccak and secp256k1 written out rather than pulled in. Works offline; the endpoint it targets does not answer yet.
- **[production]** [Foundry](https://github.com/foundry-rs/foundry) - the toolchain most of this ecosystem builds and tests with.

## Data and explorers

- **[production]** [Robinhood Chain Blockscout](https://robinhoodchain.blockscout.com) - token search, holder lists, verified sources. Search by ticker and note how many contracts come back.
- **[research]** [netting-replay](https://github.com/spireproto/netting-replay) - one file per modelled trading day, each regenerated byte for byte from its own date. Modelled flow, not observed trading, and every file says so.

## Research

- **[research]** [Netting in time, with the arithmetic](https://github.com/spireproto/spire/blob/main/docs/netting.md) - a thousand of turnover that nets to 250 carries 20 of margin at 8%, and what that does and does not depend on.
- **[research]** [The default waterfall, worked twice](https://github.com/spireproto/spire/blob/main/docs/default-waterfall.md) - the same default absorbed at layer one and at layer three, with the numbers.
- **[research]** [Design notes, unedited](https://github.com/spireproto/spireproto/tree/main/notes) - including the note that put a wrong block time into a parameter table and the one, three months later, that killed it.

## Contributing

Pull requests welcome. Two rules:

1. **Every entry carries a maturity tag**, and the tag has to be defensible. If
   the product is a landing page and a waitlist, it is `[experimental]`.
2. **Describe what it does, not how good it is.** "Dividends paid in USDC" is
   useful. "The leading platform for" is not.

Entries that make a factual claim about a chain should link to something runnable.

## License

[![CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/)

Maintained by [Spire Protocol](https://github.com/spireproto).
