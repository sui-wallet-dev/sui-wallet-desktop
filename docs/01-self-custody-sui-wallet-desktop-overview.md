# Self-custody Sui wallet for desktop: an overview

A self-custody wallet keeps the private key, and therefore the funds, on the machine the user controls. [Sui Wallet Desktop](https://suiwallet.net/) takes that approach for the Sui blockchain, in a native application that runs locally on Windows, macOS, and Linux rather than inside a browser or on someone else's server.

This overview describes how the wallet is structured, what it actually does on the user's machine, where it sits in the Sui ecosystem, and which pages on the project website cover each topic in depth.

## What Sui Wallet Desktop is, in one paragraph

Sui Wallet Desktop is the official native Sui blockchain wallet for desktop operating systems. It is published by Wallet Connections LLC, a Florida limited liability company headquartered in Miami, and is distributed as code-signed native binaries for [Windows 10/11](https://suiwallet.net/download/windows), [macOS 11 or later](https://suiwallet.net/download/mac), and [Linux x64](https://suiwallet.net/download/linux). The current version, 0.2.5, was released on 2026-05-11; the [changelog](https://suiwallet.net/changelog) records every release. The codebase is MIT-licensed and the production build has been audited by Kraken Security Labs with a published score of 9.9 / 10. The audit summary and signing details are on the [security page](https://suiwallet.net/security).

## What "self-custody" means in practice

Self-custody is not a marketing word; it is a property of the key material. In Sui Wallet Desktop:

- The 24-word seed phrase is generated on the user's device using a CSPRNG and BIP39.
- The seed is stretched to an encryption key with Argon2id (64 MiB, 3 iterations) using the user's passphrase.
- Keys are encrypted at rest with XChaCha20-Poly1305 and never leave the device unless the user explicitly exports them.
- No remote logging or telemetry is enabled by default.

The implication is simple: the operator cannot freeze, censor, or recover the user's funds. The flip side is that the user owns the recovery — which is why the [Sui seed phrase guide](https://suiwallet.net/learn/sui-seed-phrase-guide) and [recovery walkthrough](https://suiwallet.net/learn/sui-wallet-recovery) are required reading before depositing more than a token amount.

## Where Sui Wallet Desktop sits in the Sui ecosystem

[Sui](https://suiwallet.net/learn/what-is-sui) is a proof-of-stake Layer-1 blockchain that uses the Move programming language and was built by [Mysten Labs](https://suiwallet.net/learn/who-is-behind-sui). Mysten Labs publishes Slush — formerly named "Sui Wallet" — the official browser-extension and mobile wallet. In April 2025 the extension was renamed; everything that mentions the historical "Sui Wallet" extension now refers to Slush. The story is documented at [what happened to Sui Wallet](https://suiwallet.net/learn/what-happened-to-sui-wallet) and in the broader piece on [what the Sui Wallet actually is](https://suiwallet.net/learn/what-is-sui-wallet).

Sui Wallet Desktop is the official desktop counterpart that Mysten Labs does not ship. It is built by an independent team, focuses on the desktop form factor, and is positioned as the wallet to use when keys belong on a workstation rather than on a phone or inside a browser.

## What the wallet does locally

The [feature surface area](https://suiwallet.net/) is intentionally focused on what desktop users need:

- **[Native SUI staking](https://suiwallet.net/staking)** with live APY, commission, voting power, and uptime data for every validator. The full mechanics are explained in [how to stake SUI](https://suiwallet.net/learn/how-to-stake-sui), [the staking rewards model](https://suiwallet.net/learn/sui-staking-rewards), and the [validator overview](https://suiwallet.net/learn/sui-validators).
- **[Liquid staking](https://suiwallet.net/staking/liquid)** via the Haedal protocol, which mints haSUI for use in Sui DeFi while keeping the underlying stake delegated.
- **[Ledger hardware support](https://suiwallet.net/ledger)** for Nano S Plus, Nano X, Stax, and Flex through the official Sui Ledger app. The [setup guide](https://suiwallet.net/learn/sui-ledger-setup) walks through pairing.
- **[zkLogin](https://suiwallet.net/zklogin)** sign-in with Google, Apple, and Facebook OAuth providers; the OAuth provider does not learn the user's Sui address. See [zkLogin explained](https://suiwallet.net/learn/zklogin-explained) for the cryptography.
- **[DeepBook integration](https://suiwallet.net/deepbook)** — native on-chain order-book trading from inside the wallet. Background on the primitive is in [what is DeepBook](https://suiwallet.net/learn/what-is-deepbook).
- NFT display, send, and burn for Sui-standard objects.
- Multi-account management within a single mnemonic.
- A transaction simulator that shows the human-readable effect of a transaction before signing it.

## Pricing and licensing

Sui Wallet Desktop is free to download from the [main download page](https://suiwallet.net/download) and free to use. Users pay only the standard Sui gas fees that any wallet on the network would pay; the [tokenomics overview](https://suiwallet.net/learn/sui-tokenomics) and [token unlock schedule](https://suiwallet.net/learn/sui-token-unlock-schedule) cover the underlying SUI economics, and [how to buy SUI](https://suiwallet.net/learn/how-to-buy-sui) covers the on-ramp side. The codebase is MIT-licensed, so anyone is free to fork, audit, or self-host their own build.

## Who should not use a desktop wallet

A desktop wallet is the wrong choice if the user mainly transacts on mobile, if they want a multichain experience that spans Solana / Ethereum / Bitcoin, or if they cannot keep their machine free of malware. For those cases, the [best Sui wallet comparison](https://suiwallet.net/best-sui-wallet) describes the trade-offs against Slush, Suiet, Phantom, and OKX Wallet. Comparing Sui to other Layer-1s — Ethereum, Solana — is covered in the [Sui vs. Ethereum vs. Solana](https://suiwallet.net/learn/sui-vs-ethereum-vs-solana) explainer.

## How to get started

1. Read the [FAQ](https://suiwallet.net/faq) — most of the questions a first-time user has are answered there.
2. Download the build for your operating system from the [download hub](https://suiwallet.net/download).
3. If holding more than the equivalent of USD 10,000, pair a [Ledger device](https://suiwallet.net/ledger).
4. Bookmark the [learn hub](https://suiwallet.net/learn) and read at least the [seed phrase guide](https://suiwallet.net/learn/sui-seed-phrase-guide).
5. Skim the [privacy policy](https://suiwallet.net/privacy) and [terms of service](https://suiwallet.net/terms) so the relationship with the operator is clear.

For company background and press material, see [about](https://suiwallet.net/about) and [press](https://suiwallet.net/press).

## Related articles

- [Migrating from the legacy Sui Wallet browser extension](02-migrating-from-the-legacy-sui-wallet-extension.md)
- [The best Sui wallet in 2026](03-best-sui-wallet-2026.md)
- [Pairing a Ledger device with Sui Wallet Desktop](07-ledger-sui-wallet-desktop-setup.md)
- [Recovering a Sui Wallet Desktop installation from seed](12-recovering-sui-wallet-desktop-from-seed.md)
