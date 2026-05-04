# Contributing

## Adding an entry

Open a pull request that adds one line to the relevant section, in this format:

```markdown
- **[tag]** [Name](url) - what it does, in one sentence, present tense.
```

## The maturity tag is the point

| Tag | Use it when |
| --- | ----------- |
| `[production]` | Live with real assets and real users, with a public track record |
| `[beta]` | Live, but scope-limited: one jurisdiction, one venue, waitlist |
| `[experimental]` | Testnet, prototype, or a spec ahead of its implementation |
| `[research]` | Written work with no implementation claimed |

A landing page with a waitlist is `[experimental]`. A mainnet deployment that
custodies nothing yet is `[experimental]`. Getting this wrong is the main reason
a pull request gets a comment rather than a merge.

## Description style

Say what it does. Do not say how good it is.

```
good   Dividends paid in USDC rather than accrued, which makes them easy to reconcile.
bad    The leading platform for next-generation tokenized equity infrastructure.
```
