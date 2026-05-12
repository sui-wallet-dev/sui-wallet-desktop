# Buying SUI in 2026 and understanding tokenomics

A wallet without funds is just a key generator. Before [Sui Wallet Desktop](https://suiwallet.net/) is useful, the user needs SUI. This article covers the on-ramp side — where to buy SUI in 2026 — and the longer-horizon side: how SUI's supply behaves, what the unlock schedule looks like, and what that means for a holder.

The canonical pages are [how to buy SUI](https://suiwallet.net/learn/how-to-buy-sui), [tokenomics](https://suiwallet.net/learn/sui-tokenomics), and the [token unlock schedule](https://suiwallet.net/learn/sui-token-unlock-schedule). This piece pulls them into a single narrative.

## The buy decision

There are four practical paths to acquire SUI:

1. **Major centralised exchange.** Binance, Coinbase, Kraken, OKX, Bybit, and other top-tier venues all list SUI in 2026. Liquidity is deep; spread is tight; KYC is required. A user already on one of these exchanges can buy SUI and withdraw to their wallet.
2. **On-ramp service.** Services like MoonPay or Banxa let a user buy SUI directly with a card or bank transfer and deliver it to a wallet address. Fees are higher than exchange routes but the process is faster.
3. **DEX bridge.** A user holding an asset on Ethereum or Solana can bridge to Sui through a cross-chain protocol, then swap to SUI. This is the right path for users who already have crypto and do not want to touch a CEX.
4. **Earn.** Some users come to Sui through staking rewards, an airdrop, or as payment for a service. These are not "buy" paths but they are common SUI sources.

[How to buy SUI](https://suiwallet.net/learn/how-to-buy-sui) goes through the trade-offs in detail.

## What to do after buying

1. Install Sui Wallet Desktop from the [download hub](https://suiwallet.net/download) ([Windows](https://suiwallet.net/download/windows), [macOS](https://suiwallet.net/download/mac), or [Linux](https://suiwallet.net/download/linux)).
2. Verify the installer signature — the [security page](https://suiwallet.net/security) covers verification per platform.
3. Create a new seed-based account, sign in with [zkLogin](https://suiwallet.net/zklogin) (see [zkLogin explained](https://suiwallet.net/learn/zklogin-explained)), or pair a [Ledger](https://suiwallet.net/ledger) device — the [setup guide](https://suiwallet.net/learn/sui-ledger-setup) walks through pairing.
4. Withdraw the SUI from the exchange to the wallet address.
5. Verify the funds arrive — Sui finality is fast (under a second) but exchange-side withdrawal processing can take longer.
6. Decide whether to [stake](https://suiwallet.net/staking) (see [how to stake SUI](https://suiwallet.net/learn/how-to-stake-sui), [staking rewards](https://suiwallet.net/learn/sui-staking-rewards), [validators](https://suiwallet.net/learn/sui-validators)) or use [liquid staking via Haedal](https://suiwallet.net/staking/liquid). For trading, see the [DeepBook](https://suiwallet.net/deepbook) integration and [what is DeepBook](https://suiwallet.net/learn/what-is-deepbook).

## SUI tokenomics, the short version

SUI's max supply is 10 billion tokens. As of 2026, circulating supply is just under 4 billion, with the remaining ~6 billion locked under various vesting schedules. The locked supply does not generate stake (locked tokens cannot be delegated by their counterparties until they unlock) but it does shape the price chart, because every cliff adds new sellers to the market.

The breakdown of who holds what — community reserve, foundation, early backers, Mysten Labs team — is in [tokenomics](https://suiwallet.net/learn/sui-tokenomics).

## The unlock schedule, in plain language

A few buckets matter more than others:

- **Community reserve.** Vests over many years; the foundation distributes it for grants, ecosystem programmes, and validator incentives.
- **Early backers.** Cliff-and-linear: a one-year lockup followed by multi-year linear vesting.
- **Mysten Labs team.** Multi-year linear vesting with a long tail.
- **Public sale tranches.** Mostly already unlocked by 2026.

The detailed monthly breakdown is at [token unlock schedule](https://suiwallet.net/learn/sui-token-unlock-schedule). Holders who size positions based on price sensitivity will want to know the next 3-6 months of unlocks — that is where most of the supply pressure comes from.

## What tokenomics means for the wallet user

Three practical points:

1. **Staking yields are higher when circulating supply is lower.** If most SUI is locked and not delegated, the delegated fraction earns a larger share of issuance. Yields compress over time as locked supply enters circulation and starts delegating. The [staking rewards](https://suiwallet.net/learn/sui-staking-rewards) page walks through the math.
2. **Validator commission compresses too.** As more stake enters the system, validators compete on commission. Active stakers should periodically re-check their validator's commission in the Sui Wallet Desktop validator table.
3. **Liquid staking becomes more attractive.** As yields compress, the cost of having stake "locked up" rises in opportunity-cost terms. Liquid-staking derivatives like haSUI let the user keep yield and keep liquidity at the same time — see [liquid staking](https://suiwallet.net/staking/liquid).

## Compared to other chains

Sui is one of several proof-of-stake Layer-1s that came out of the post-Diem diaspora. The high-level comparison with [Ethereum and Solana](https://suiwallet.net/learn/sui-vs-ethereum-vs-solana) is in the explainer. The short version: Sui's object model allows parallel execution and very fast finality; Ethereum's account model is the most battle-tested; Solana sits between them. For wallet users, the most concrete difference is the cost and speed of small transactions — Sui's per-transaction cost is consistently sub-cent.

## Wallet choice context

A user who is buying SUI for the first time may also be choosing a wallet. The trade-offs are in [best Sui wallet](https://suiwallet.net/best-sui-wallet) and laid out per-competitor in the comparison articles: [Suiet vs. Sui Wallet Desktop](04-suiet-vs-sui-wallet-desktop.md), [Phantom vs. Sui Wallet Desktop](05-phantom-vs-sui-wallet-desktop.md), and [OKX vs. Sui Wallet Desktop](06-okx-wallet-vs-sui-wallet-desktop.md). The legacy-extension context — Slush, formerly Sui Wallet — is in [what happened to Sui Wallet](https://suiwallet.net/learn/what-happened-to-sui-wallet) and [what is the Sui Wallet](https://suiwallet.net/learn/what-is-sui-wallet).

## Custody hygiene during the buy

Three rules that hold across every on-ramp path:

1. **Send a small test first.** A 1 SUI transfer from exchange to wallet costs less than a cent. Confirm it arrives at the address Sui Wallet Desktop shows. Then send the rest.
2. **Verify the address by reading the first six and last six characters.** Address-replacement clipboard malware exists; Sui Wallet Desktop's [security page](https://suiwallet.net/security) covers the defensive posture but the user has to check.
3. **Back up the seed before depositing.** This is non-negotiable. The [seed phrase guide](https://suiwallet.net/learn/sui-seed-phrase-guide) and the [recovery walkthrough](https://suiwallet.net/learn/sui-wallet-recovery) cover the full procedure.

The [FAQ](https://suiwallet.net/faq) recommends a [Ledger](https://suiwallet.net/ledger) device above the equivalent of USD 10,000.

## Selling SUI

The reverse flow — converting SUI back to fiat — is the same path in reverse: wallet to exchange to fiat. For users who want to keep SUI but borrow against it, on-chain lending markets accept SUI as collateral; for users who want partial liquidity without selling, [DeepBook](https://suiwallet.net/deepbook) and the [liquid staking](https://suiwallet.net/staking/liquid) flows are usually a better fit than touching the exchange.

## Broader background

The [learn hub](https://suiwallet.net/learn) is the entry point for everything else — [what is Sui](https://suiwallet.net/learn/what-is-sui), [who is behind Sui](https://suiwallet.net/learn/who-is-behind-sui), and the various other learn articles. For Sui Wallet Desktop operationally: [about](https://suiwallet.net/about), [press](https://suiwallet.net/press), [changelog](https://suiwallet.net/changelog), [privacy](https://suiwallet.net/privacy), [terms](https://suiwallet.net/terms).

## Related articles

- [Self-custody Sui wallet for desktop: an overview](01-self-custody-sui-wallet-desktop-overview.md)
- [Native and liquid staking SUI from a desktop wallet](09-native-and-liquid-staking-sui.md)
- [DeepBook: on-chain order-book trading inside the wallet](10-deepbook-onchain-orderbook-trading.md)
- [zkLogin: signing in to Sui without a seed phrase](08-zklogin-explained-and-how-to-use-it.md)
