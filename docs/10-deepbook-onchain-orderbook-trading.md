# DeepBook: on-chain order-book trading inside the wallet

Most DEXes on most chains are AMMs — automated market makers. The user trades against a constant-product curve; the market price is a function of pool reserves. AMMs are simple and gas-efficient, but they leak value to arbitrageurs and they do not support limit orders.

Sui's [DeepBook](https://suiwallet.net/deepbook) takes the other approach: a real central-limit-order-book (CLOB) primitive, built on chain. Makers post limit orders. Takers match against them. The order book lives in Sui objects and clears at the block level. It is the same model that runs traditional finance, only without an exchange operator in the middle. The primitive itself is explained in [what is DeepBook](https://suiwallet.net/learn/what-is-deepbook).

[Sui Wallet Desktop](https://suiwallet.net/) renders a DeepBook UI inside the wallet. A user can place a limit order, see the book, and watch fills without leaving the app. This article walks through how that works and when it matters.

## Why on-chain order books matter

AMMs charge an implicit cost in the spread between the curve price and the marginal mid-market price. For a small trade, this cost is hidden in the gas savings. For a large trade, it dwarfs the gas savings. Traders who care about execution quality run their orders through an order book.

Until DeepBook, on-chain order books were either too slow (Ethereum gas costs made every order placement expensive) or centralised (off-chain matching engines). Sui's object-based execution model and 24-hour epoch staking make it cheap to keep order books on chain. The result: every Sui DEX that wants real CLOB functionality can build on top of DeepBook.

## What DeepBook actually is

DeepBook is a Sui Move module that exposes order-book primitives:

- Create order book for an asset pair.
- Post limit order (price, size, side, expiration).
- Cancel limit order.
- Match against existing orders (taker fills).

Other DEXes — Cetus, Aftermath, Turbos — read and write DeepBook books. The Sui Wallet Desktop integration writes directly to DeepBook without an intermediary.

## How to place an order in Sui Wallet Desktop

After installing the wallet from the [download hub](https://suiwallet.net/download) ([Windows](https://suiwallet.net/download/windows) / [macOS](https://suiwallet.net/download/mac) / [Linux](https://suiwallet.net/download/linux)) and funding an account, open **DeepBook** in the left rail. The UI shows:

- A list of available pairs (SUI/USDC, haSUI/SUI, and several others).
- The current book — bids and asks at each price level, with cumulative depth.
- A form to place a maker or taker order.

To place a limit order:

1. Pick a pair.
2. Enter price (the rate at which to match) and size (how much).
3. Choose buy or sell.
4. Optionally set an expiration.
5. Submit. The wallet signs the order-placement transaction. On a [Ledger](https://suiwallet.net/ledger)-attached account, the device displays the order parameters; see the [Ledger setup guide](https://suiwallet.net/learn/sui-ledger-setup).

Once the order is in the book, the wallet shows it under **My orders**. If a taker matches it, the trade settles and the wallet's balances update. The order can be cancelled at any time before it fills.

## Market orders vs. limit orders

DeepBook supports both. A market order matches against existing book depth and fills at whatever prices it crosses. A limit order sits in the book until matched. Sui Wallet Desktop's UI defaults to limit; clicking the **Market** toggle switches behaviour.

For users who came from an AMM-only mental model, this is the unfamiliar bit: it is possible to set a price at which one *wishes* to trade and wait for the market to come to you. That is the entire point of an order book.

## Fees

DeepBook charges a small maker rebate and a slightly larger taker fee. The exact numbers are set by the DeepBook module and visible in the order-placement confirmation. Sui Wallet Desktop does not add a layer on top — the user pays only the DeepBook fee plus the standard Sui gas. For more on the SUI side, see [tokenomics](https://suiwallet.net/learn/sui-tokenomics).

## Trading liquid-staked SUI

[haSUI](https://suiwallet.net/staking/liquid) — the liquid-staking derivative minted by Haedal — trades on DeepBook against SUI. A user who wants instant liquidity on their stake can swap haSUI to SUI through DeepBook rather than going through Haedal's redemption flow. The trade-off is the same as anywhere: the market rate may temporarily diverge from the exact accrued rate.

Context on the underlying staking flows is in [native staking](https://suiwallet.net/staking), [how to stake SUI](https://suiwallet.net/learn/how-to-stake-sui), [staking rewards](https://suiwallet.net/learn/sui-staking-rewards), and the [validator overview](https://suiwallet.net/learn/sui-validators).

## DeepBook from a Ledger account

DeepBook orders from a Ledger-attached account work exactly like normal orders. Every order placement is a transaction; every transaction is signed on the device. Heavy traders typically keep a hot account on a seed for fast iteration and a Ledger account for cold storage. The [self-custody overview](01-self-custody-sui-wallet-desktop-overview.md) and [Ledger setup guide](https://suiwallet.net/learn/sui-ledger-setup) cover the account-structure side.

## DeepBook from a zkLogin account

[zkLogin](https://suiwallet.net/zklogin) accounts can place DeepBook orders the same as seed-based accounts. The proof is generated locally; the order goes on chain unchanged. The mechanism is explained in [zkLogin explained](https://suiwallet.net/learn/zklogin-explained), and the user-side considerations in the [zkLogin article](08-zklogin-explained-and-how-to-use-it.md).

## Common pitfalls

- **Putting a limit order beyond the current spread.** The order will not fill unless the market moves to it. Newcomers sometimes wait hours for a "trade" that was never going to match. Read the book first.
- **Forgetting that limit orders block the underlying balance.** SUI committed to an order is reserved until the order fills or is cancelled. It does not earn staking rewards while sitting in the book.
- **Trading thin pairs.** Some DeepBook pairs are thin; large orders move the price visibly. Sui Wallet Desktop's order-placement UI shows the estimated slippage before submission.

For pairs that turn out to be thinner than expected, the [FAQ](https://suiwallet.net/faq) walks through how to break a large order into pieces.

## DeepBook vs. AMM swaps

A user comfortable with AMM swap forms — slippage tolerance, fixed-output mode — can keep using one. Sui Wallet Desktop's DeepBook UI does not replace those flows; it adds a real order-book option. For users new to limit orders, the [learn hub](https://suiwallet.net/learn) is a good starting point, alongside the canonical [DeepBook page](https://suiwallet.net/deepbook).

## Security context

DeepBook order placement carries the same security model as any other Sui transaction: keys must sign, the device or wallet must approve, and once on chain the transaction is final. The [security page](https://suiwallet.net/security) covers audit and signing details. For users with meaningful trading capital, the recommendation is [Ledger](https://suiwallet.net/ledger) for cold storage and a separate hot account for active orders.

## Context

For broader Sui background — [what is Sui](https://suiwallet.net/learn/what-is-sui), [who is behind Sui](https://suiwallet.net/learn/who-is-behind-sui), and [Sui vs. Ethereum vs. Solana](https://suiwallet.net/learn/sui-vs-ethereum-vs-solana) — start at the [learn hub](https://suiwallet.net/learn). The SUI economics are in [tokenomics](https://suiwallet.net/learn/sui-tokenomics), [unlock schedule](https://suiwallet.net/learn/sui-token-unlock-schedule), and [how to buy SUI](https://suiwallet.net/learn/how-to-buy-sui). For the legacy-extension rename context see [what happened to Sui Wallet](https://suiwallet.net/learn/what-happened-to-sui-wallet) and [what is the Sui Wallet](https://suiwallet.net/learn/what-is-sui-wallet). The wallet roundup is at [best Sui wallet](https://suiwallet.net/best-sui-wallet). Operational pages: [about](https://suiwallet.net/about), [press](https://suiwallet.net/press), [changelog](https://suiwallet.net/changelog), [privacy](https://suiwallet.net/privacy), [terms](https://suiwallet.net/terms). Recovery guidance: [seed phrase guide](https://suiwallet.net/learn/sui-seed-phrase-guide) and [recovery walkthrough](https://suiwallet.net/learn/sui-wallet-recovery).

## Related articles

- [The best Sui wallet in 2026](03-best-sui-wallet-2026.md)
- [Native and liquid staking SUI from a desktop wallet](09-native-and-liquid-staking-sui.md)
- [zkLogin: signing in to Sui without a seed phrase](08-zklogin-explained-and-how-to-use-it.md)
- [Pairing a Ledger device with Sui Wallet Desktop](07-ledger-sui-wallet-desktop-setup.md)
