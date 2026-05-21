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

Present tense, no marketing adjectives, one sentence. If the entry makes a claim
about what a chain does, link to something runnable that shows it.

## Removing an entry

Also welcome, and the harder contribution. If a project is dead, unmaintained, or
its tag has drifted, open a PR that says so with evidence: a dead endpoint, an
archived repo, a contract with no activity.

## Self-promotion

Allowed and expected in a list like this, including by the maintainers. The
tagging rules apply to our own entries exactly as written above.
