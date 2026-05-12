# Native and liquid staking SUI from a desktop wallet

SUI is a proof-of-stake asset. Holders can earn rewards by delegating their stake to a validator, and they can keep their stake liquid — usable in DeFi — by minting a liquid-staking derivative. [Sui Wallet Desktop](https://suiwallet.net/) supports both flows inside the same app: [native staking](https://suiwallet.net/staking) and [liquid staking via Haedal](https://suiwallet.net/staking/liquid).

This article explains how each works, when one is preferable to the other, and how to do both step by step inside Sui Wallet Desktop.

## Native staking, in one paragraph

The user picks a validator. The user delegates a SUI amount to that validator with a stake-add transaction. The validator counts the user's stake toward its voting power for the rest of the current epoch. At the end of each epoch (~24 hours on Sui mainnet), the validator earns a share of network rewards and the user's delegation receives a pro-rata share, minus the validator's commission. Rewards accrue continuously and compound automatically — the user does not need to "claim." When the user wants to unstake, they submit a stake-withdraw transaction; the SUI returns to their account at the next epoch boundary. The full mechanics are in [how to stake SUI](https://suiwallet.net/learn/how-to-stake-sui) and the underlying economics in [staking rewards](https://suiwallet.net/learn/sui-staking-rewards).

## Liquid staking, in one paragraph

Liquid staking lets the user keep their stake delegated *and* keep a liquid token they can use in DeFi. In Sui's case, [Haedal](https://suiwallet.net/staking/liquid) is the dominant liquid-staking protocol. The user deposits SUI into Haedal; Haedal aggregates the deposit with others, delegates the aggregate to a curated set of validators, and mints haSUI to the user proportional to the deposit. haSUI accrues value relative to SUI as rewards accumulate. Whenever the user wants liquidity, they can swap haSUI back to SUI on a DEX (instant, but at the prevailing market rate) or unstake through Haedal directly (slower, but at the exact accrued rate).

## Picking a validator

Sui Wallet Desktop renders the full validator set, sourced from the Sui RPC. The columns the user cares about are:

- **APY.** Annualised reward rate, computed from the validator's recent reward history.
- **Commission.** The percentage of rewards the validator keeps before distributing to delegators.
- **Voting power.** The validator's share of total active stake — high values mean the validator is more influential but adds to network centralisation.
- **Uptime.** The validator's missed-block rate. Low uptime hurts rewards.

The conventional wisdom in Sui is to spread stake across several validators in the middle of the table — not the largest (centralisation risk, lower marginal APY) and not the smallest (uptime risk). The [validator overview](https://suiwallet.net/learn/sui-validators) covers the considerations in depth.

## Step by step: native staking

1. Open Sui Wallet Desktop. If the install is new, follow the [self-custody overview](01-self-custody-sui-wallet-desktop-overview.md) or the [migration guide](02-migrating-from-the-legacy-sui-wallet-extension.md) to get to a funded account.
2. Click **Stake** in the left rail. The wallet shows the full validator table from [native staking](https://suiwallet.net/staking).
3. Sort by APY (descending), then by uptime (descending). Pick three or four validators with APY in the top quartile, commission under 10%, and uptime above 99%.
4. Click **Delegate** on the chosen validator. Enter the amount of SUI to stake. The wallet shows the expected reward rate and the fee.
5. Approve the transaction. If the account is [Ledger](https://suiwallet.net/ledger)-attached, approve on the device — see the [Ledger setup guide](https://suiwallet.net/learn/sui-ledger-setup).
6. Repeat for the other validators, splitting the stake.
7. Wait one epoch (~24 hours). After that, the **Rewards** column updates each epoch.

To unstake, click the validator entry under **Your delegations** and choose **Withdraw**. The funds return after the next epoch boundary.

## Step by step: liquid staking

1. From the same Sui Wallet Desktop install, open the [liquid staking](https://suiwallet.net/staking/liquid) panel.
2. Enter the SUI amount to convert. The panel shows the haSUI quantity that will be minted at the current rate.
3. Approve the transaction. The user's wallet balance now shows haSUI instead of (the converted portion of) SUI.
4. The haSUI balance appreciates relative to SUI over time as the underlying delegation earns rewards.
5. To unwind: either swap haSUI for SUI on a Sui DEX (instant, market-rate), or redeem through Haedal (delayed, exact-rate).

## Native vs. liquid: when to pick which

- **Native staking** suits users who delegate and forget, who want full control over which validator they support, and who do not need liquidity.
- **Liquid staking** suits users who want their stake to remain composable — usable in lending markets, AMMs, or other DeFi primitives — and who are comfortable holding a derivative asset rather than the underlying.

Many serious users do both: 80% native, 20% liquid, with the liquid portion deployed into a yield strategy elsewhere on Sui.

## DeepBook interactions

[DeepBook](https://suiwallet.net/deepbook) is the on-chain order book that backs many Sui DEXes. haSUI is one of the asset pairs that trades on DeepBook. A user holding haSUI can place limit orders directly through the Sui Wallet Desktop DeepBook UI without leaving the app. Background on the primitive is in [what is DeepBook](https://suiwallet.net/learn/what-is-deepbook).

## Buying more SUI to stake

Users topping up to stake should read [how to buy SUI](https://suiwallet.net/learn/how-to-buy-sui). The supply-side context — [tokenomics](https://suiwallet.net/learn/sui-tokenomics) and [unlock schedule](https://suiwallet.net/learn/sui-token-unlock-schedule) — is worth a glance, since large unlocks can affect short-term price and therefore short-term USD-denominated yield.

## Tax notes (informal — not advice)

Staking rewards on Sui accrue per epoch and are reflected in the validator's reward pool, not paid out as discrete events to the user's address. In tax regimes that treat staking as ordinary income on receipt, this raises the question of "when is the reward received" — answers vary by jurisdiction. The [terms of service](https://suiwallet.net/terms) make clear that Sui Wallet Desktop does not provide tax guidance; users should consult their own advisers.

## Operational notes

- **Validator commission can change.** The wallet refreshes commission per epoch. If a validator quietly raises commission, the user sees it on the next refresh.
- **Validator can leave the active set.** If a validator drops out, the delegation is automatically returned at the next epoch.
- **Ledger-attached accounts can stake normally.** The transaction-signing flow is on the device; otherwise the UX is identical.

## Security context

Audits, signing, and the threat model live on the [security page](https://suiwallet.net/security). The [FAQ](https://suiwallet.net/faq) recommends hardware-wallet usage above the equivalent of USD 10,000; for stakers with meaningful positions, the [Ledger setup guide](https://suiwallet.net/learn/sui-ledger-setup) is the right next step.

## Context

For an introduction to Sui itself — [what is Sui](https://suiwallet.net/learn/what-is-sui), [who is behind Sui](https://suiwallet.net/learn/who-is-behind-sui), [Sui vs. Ethereum vs. Solana](https://suiwallet.net/learn/sui-vs-ethereum-vs-solana) — see the [learn hub](https://suiwallet.net/learn). The [best Sui wallet comparison](https://suiwallet.net/best-sui-wallet) covers wallet choice; the legacy-extension context is at [what happened to Sui Wallet](https://suiwallet.net/learn/what-happened-to-sui-wallet) and [what is the Sui Wallet](https://suiwallet.net/learn/what-is-sui-wallet). Operational pages: [download](https://suiwallet.net/download) ([Windows](https://suiwallet.net/download/windows) / [macOS](https://suiwallet.net/download/mac) / [Linux](https://suiwallet.net/download/linux)), [changelog](https://suiwallet.net/changelog), [about](https://suiwallet.net/about), [press](https://suiwallet.net/press), [privacy](https://suiwallet.net/privacy). For zero-seed onboarding alternatives, see [zkLogin](https://suiwallet.net/zklogin) and [zkLogin explained](https://suiwallet.net/learn/zklogin-explained), and the [seed phrase guide](https://suiwallet.net/learn/sui-seed-phrase-guide) for the regular-seed flow.

## Related articles

- [The best Sui wallet in 2026](03-best-sui-wallet-2026.md)
- [Pairing a Ledger device with Sui Wallet Desktop](07-ledger-sui-wallet-desktop-setup.md)
- [DeepBook: on-chain order-book trading inside the wallet](10-deepbook-onchain-orderbook-trading.md)
- [Buying SUI in 2026 and understanding tokenomics](11-buying-sui-and-tokenomics.md)
