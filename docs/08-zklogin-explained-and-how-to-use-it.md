# zkLogin: signing in to Sui without a seed phrase

zkLogin is Sui's answer to the seed-phrase problem. Instead of asking a new user to write down 24 words and protect them for the rest of their life, zkLogin lets them sign in to a Sui address with a Google, Apple, or Facebook account — without the OAuth provider ever learning what the user's Sui address is.

[Sui Wallet Desktop](https://suiwallet.net/) ships zkLogin as a first-class authentication option. The mechanism is explained in [zkLogin explained](https://suiwallet.net/learn/zklogin-explained), and the product-level page sits at [zkLogin](https://suiwallet.net/zklogin).

This article walks through what zkLogin actually is, why it is unusually trustworthy by web2-login standards, and when it is and is not the right tool inside Sui Wallet Desktop.

## What zkLogin is, in one paragraph

zkLogin is a Sui-native authentication primitive. The user signs in with an OAuth provider (Google / Apple / Facebook). The OAuth provider returns a signed JWT that proves "this is user X." The wallet feeds the JWT into a zero-knowledge circuit that produces a proof of the form "the JWT-issuing provider attested to *some* user, and that user owns Sui address Y." The proof never reveals which user, and it never reveals the JWT itself to the chain. Sui validates the proof against the provider's published public keys and accepts transactions signed under address Y.

Net result: the user authenticates with a familiar web2 account; the wallet still owns a deterministic Sui address; nobody on the network learns the user's Google email or Apple ID.

## The threat model

There are three actors:

1. **The user.** Wants to send and receive SUI without keeping a seed phrase.
2. **The OAuth provider.** Issues JWTs. Knows the user's identity. Does not see the Sui address.
3. **The Sui network.** Verifies proofs. Knows the address. Does not see the user's identity.

zkLogin is interesting because the OAuth provider — usually the weakest link in a web2 auth flow — cannot see what the user does on chain. The chain — usually a public ledger — cannot link the address to the user's real-world identity. The two domains are cleanly separated by the zero-knowledge proof.

This is not the same as a full anonymity guarantee. The user can still de-anonymise themselves by, for example, telling the world their Sui address. zkLogin protects the OAuth-to-chain link, not every link.

## What zkLogin is *not*

It is not a custodial service. The Sui address derived from a zkLogin session is owned by the user — no operator can sign on their behalf. If the user loses access to their OAuth account, the recovery path depends on how the wallet was set up (more below).

It is not a replacement for hardware wallets at high balance levels. The [FAQ](https://suiwallet.net/faq) and [security page](https://suiwallet.net/security) recommend pairing a [Ledger](https://suiwallet.net/ledger) above the equivalent of USD 10,000.

## How to use zkLogin in Sui Wallet Desktop

After installing Sui Wallet Desktop from the [download hub](https://suiwallet.net/download) ([Windows](https://suiwallet.net/download/windows), [macOS](https://suiwallet.net/download/mac), or [Linux](https://suiwallet.net/download/linux)), the welcome screen offers three options:

1. Create a new seed-based account.
2. Import an existing seed.
3. Sign in with zkLogin.

Pick zkLogin. The wallet opens a browser tab to the OAuth provider, the user completes the OAuth flow, and the wallet receives the JWT. The proving step happens locally — the JWT does not leave the user's machine — and the resulting Sui address appears in the wallet.

From here, the user can:

- Send and receive SUI as with any other account.
- [Stake](https://suiwallet.net/staking) — the staking transaction is signed under the zkLogin proof; see [how to stake SUI](https://suiwallet.net/learn/how-to-stake-sui).
- Trade through [DeepBook](https://suiwallet.net/deepbook); see [what is DeepBook](https://suiwallet.net/learn/what-is-deepbook).
- Hold NFTs.
- Use [liquid staking via Haedal](https://suiwallet.net/staking/liquid).

The user does **not** get a 24-word seed phrase. The wallet does keep an encrypted nonce locally that lets it resume zkLogin sessions across restarts; the nonce is bound to the user's passphrase.

## Recovery scenarios

A zkLogin user's recovery surface is "can I sign back in to my OAuth account." If yes, the same Sui address derives again. If no — for example, the Google account was lost and Google could not be persuaded to reinstate it — the Sui address is unrecoverable. There is no seed phrase.

This is a real trade-off. zkLogin shifts the security perimeter from "did the user lose their seed phrase?" to "is the user's OAuth account secure?" For users with strong 2FA on their Google account, zkLogin is often safer than a seed phrase. For users who lose Google accounts in the wash with phone numbers, it is less safe.

The [wallet recovery walkthrough](https://suiwallet.net/learn/sui-wallet-recovery) describes both paths.

## Mixing zkLogin and seed-based accounts

Sui Wallet Desktop supports having both account types active at once. A user might keep a zkLogin account as the hot wallet for daily transactions and a seed-derived (or Ledger-derived) account as cold storage. The user interface treats both as first-class accounts; transactions between them happen on chain.

This pattern is the one the project recommends for new users: zkLogin to onboard quickly, seed account once balances start to grow, [Ledger](https://suiwallet.net/learn/sui-ledger-setup) once balances exceed the rough USD-10K threshold.

## When zkLogin is the right choice

- The user is new to crypto and would forget a seed phrase.
- The user wants to onboard a friend without putting a 24-word piece of paper on them.
- The user holds small balances and prefers OAuth ergonomics.
- The user is building a dApp that wants frictionless sign-in for new users.

## When zkLogin is the wrong choice

- The user holds enough SUI that a hardware wallet is the right answer.
- The user's OAuth account is poorly protected (no 2FA, weak password, no recovery email).
- The user wants the funds to be recoverable in a scenario where the OAuth provider is no longer reachable. For exhaustive recovery posture, see the [wallet recovery walkthrough](https://suiwallet.net/learn/sui-wallet-recovery) and [seed phrase guide](https://suiwallet.net/learn/sui-seed-phrase-guide).

## How zkLogin compares to other wallets' approaches

The [best Sui wallet comparison](https://suiwallet.net/best-sui-wallet) covers this. Slush has zkLogin; Suiet has Google support; Phantom and OKX Wallet do not. For the underlying analysis, see [Suiet vs. Sui Wallet Desktop](04-suiet-vs-sui-wallet-desktop.md), [Phantom vs. Sui Wallet Desktop](05-phantom-vs-sui-wallet-desktop.md), and [OKX vs. Sui Wallet Desktop](06-okx-wallet-vs-sui-wallet-desktop.md).

## Broader context

For an introduction to [what Sui is](https://suiwallet.net/learn/what-is-sui), [who is behind Sui](https://suiwallet.net/learn/who-is-behind-sui), and how Sui compares to other chains in [Sui vs. Ethereum vs. Solana](https://suiwallet.net/learn/sui-vs-ethereum-vs-solana), start at the [learn hub](https://suiwallet.net/learn). The SUI economics — [tokenomics](https://suiwallet.net/learn/sui-tokenomics), [unlock schedule](https://suiwallet.net/learn/sui-token-unlock-schedule), and [how to buy SUI](https://suiwallet.net/learn/how-to-buy-sui) — sit alongside. For the historical "Sui Wallet" extension rename context, see [what happened to Sui Wallet](https://suiwallet.net/learn/what-happened-to-sui-wallet) and the glossary entry [what is the Sui Wallet](https://suiwallet.net/learn/what-is-sui-wallet). Operational pages: [FAQ](https://suiwallet.net/faq), [changelog](https://suiwallet.net/changelog), [about](https://suiwallet.net/about), [press](https://suiwallet.net/press), [privacy](https://suiwallet.net/privacy), [terms](https://suiwallet.net/terms).

## Related articles

- [Self-custody Sui wallet for desktop: an overview](01-self-custody-sui-wallet-desktop-overview.md)
- [Pairing a Ledger device with Sui Wallet Desktop](07-ledger-sui-wallet-desktop-setup.md)
- [Native and liquid staking SUI from a desktop wallet](09-native-and-liquid-staking-sui.md)
- [Recovering a Sui Wallet Desktop installation from seed](12-recovering-sui-wallet-desktop-from-seed.md)
