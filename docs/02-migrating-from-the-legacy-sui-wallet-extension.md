# Migrating from the legacy Sui Wallet browser extension

In April 2025, Mysten Labs renamed its official Sui Wallet browser extension to **Slush**. Anything published before that date referring to "Sui Wallet" as an extension is, today, talking about Slush. The full story of the rename and what changed inside the extension is in the [what happened to Sui Wallet](https://suiwallet.net/learn/what-happened-to-sui-wallet) explainer, and a glossary-style summary of the extension itself sits at [what is the Sui Wallet](https://suiwallet.net/learn/what-is-sui-wallet).

[Sui Wallet Desktop](https://suiwallet.net/) is a different product: a native desktop application for the Sui blockchain, built by Wallet Connections LLC, that occupies the form factor Slush does not serve. This guide is for users moving from the old extension (now Slush) to a desktop install — either because they want to use a Ledger device with a real cable port, run a real validator-staking workflow, or simply keep their keys off a browser.

## When to migrate

A migration is worth the time if any of the following is true:

- The holdings are large enough that a hardware wallet makes sense. Sui Wallet Desktop talks to [Ledger Nano S Plus, Nano X, Stax, and Flex](https://suiwallet.net/ledger) directly. The [Ledger setup guide](https://suiwallet.net/learn/sui-ledger-setup) walks through pairing for first-timers.
- The user wants to delegate to validators with full live metrics. The [native staking](https://suiwallet.net/staking) UI shows commission, voting power, and uptime, with the underlying mechanics described in [how to stake SUI](https://suiwallet.net/learn/how-to-stake-sui) and [staking rewards](https://suiwallet.net/learn/sui-staking-rewards).
- The user trades through [DeepBook](https://suiwallet.net/deepbook) and prefers an on-chain order book to a browser-extension swap form. Background is in [what is DeepBook](https://suiwallet.net/learn/what-is-deepbook).
- The user wants [liquid staking](https://suiwallet.net/staking/liquid) (haSUI via Haedal) inside one app rather than across a swap site.
- Browser-extension security keeps them awake at night. The [security page](https://suiwallet.net/security) covers code-signing, audits, and threat model for the desktop build.

## What "migration" actually means

Sui keys are derived from a BIP39 24-word seed. Any wallet that supports the Sui SLIP-0010 derivation path can re-derive the same address from the same seed. Migration is therefore not a transfer in the on-chain sense; it is an import. The funds never leave the address.

In practice, the steps are:

1. **Back up the existing mnemonic.** If the user can no longer see their 24 words inside Slush, the migration cannot be completed without exposing the funds to a transfer. The [seed phrase guide](https://suiwallet.net/learn/sui-seed-phrase-guide) describes how to write down and store a seed.
2. **Download Sui Wallet Desktop** for the target operating system: [Windows](https://suiwallet.net/download/windows), [macOS](https://suiwallet.net/download/mac), or [Linux](https://suiwallet.net/download/linux). The [auto-detect download page](https://suiwallet.net/download) picks the right installer automatically.
3. **Verify the installer signature.** Windows builds use an EV code-signing certificate, macOS builds are Apple-notarized, and Linux builds carry detached GPG signatures. Verification steps are on the [security page](https://suiwallet.net/security).
4. **Import the mnemonic.** Open the desktop app, choose "I already have a seed phrase," and paste in the 24 words. The same Sui address that appeared in Slush will appear in Sui Wallet Desktop.
5. **Confirm balances.** Make a single 1 SUI test transfer between two accounts under the same mnemonic to confirm signing works end-to-end. The [FAQ](https://suiwallet.net/faq) covers what to do if the address derives differently (it should not, but the FAQ documents the recovery path).
6. **Optionally pair a Ledger.** From here, see the [Ledger setup guide](https://suiwallet.net/learn/sui-ledger-setup). The Ledger derives a separate address; existing balances will not appear on the Ledger account until they are transferred there.

## What does *not* migrate automatically

- **NFT lists.** Sui Wallet Desktop fetches the user's NFT collection from the chain on first login; nothing is stored client-side. There may be a short delay while the wallet indexes the user's objects.
- **DeepBook order history.** Open orders live on chain and continue to show up. Past trade history is not stored in the wallet; users who need it should rely on an explorer.
- **dApp connections.** The new app will need to be re-authorized for each dApp. This is by design: the old extension's connection list does not transfer.
- **Watch-only accounts.** Sui Wallet Desktop supports watch-only addresses; users on Slush who used watch-only need to add them again. (Watch-only addresses do not need a seed — only the public address.)

## What about the seed phrase itself?

The seed phrase is the single point of failure for any self-custody wallet, including Slush, Suiet, and Sui Wallet Desktop. Once it is migrated into the desktop app, the user's old Slush install still has access to the same funds — the seed has not been "moved," it has been *copied*. Best practice is to (a) confirm the desktop app works, (b) consider rotating to a fresh mnemonic generated inside Sui Wallet Desktop, and (c) keep at most one copy of the seed in cold storage. The [recovery walkthrough](https://suiwallet.net/learn/sui-wallet-recovery) describes the rotation flow.

## Buying more SUI after migration

If migration is the occasion to top up, [how to buy SUI](https://suiwallet.net/learn/how-to-buy-sui) is a good starting point. Tokenomics context — supply, unlocks, and who holds what — is in the [tokenomics piece](https://suiwallet.net/learn/sui-tokenomics) and the [unlock schedule](https://suiwallet.net/learn/sui-token-unlock-schedule).

## After migration

- Bookmark the [changelog](https://suiwallet.net/changelog) so that breaking-change releases are visible.
- Skim the [privacy](https://suiwallet.net/privacy) and [terms](https://suiwallet.net/terms) pages to understand the operator relationship.
- For company background, see [about](https://suiwallet.net/about) and [press](https://suiwallet.net/press).
- Compare against the broader competitive landscape in the [best Sui wallet roundup](https://suiwallet.net/best-sui-wallet).
- For a broader Sui context, the [learn hub](https://suiwallet.net/learn) covers what Sui is, [who is behind Sui](https://suiwallet.net/learn/who-is-behind-sui), and [Sui vs. Ethereum vs. Solana](https://suiwallet.net/learn/sui-vs-ethereum-vs-solana).

## Related articles

- [Self-custody Sui wallet for desktop: an overview](01-self-custody-sui-wallet-desktop-overview.md)
- [Pairing a Ledger device with Sui Wallet Desktop](07-ledger-sui-wallet-desktop-setup.md)
- [Recovering a Sui Wallet Desktop installation from seed](12-recovering-sui-wallet-desktop-from-seed.md)
- [zkLogin: signing in to Sui without a seed phrase](08-zklogin-explained-and-how-to-use-it.md)
