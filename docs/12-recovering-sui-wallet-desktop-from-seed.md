# Recovering a Sui Wallet Desktop installation from seed

The seed phrase is the only thing that matters. If the user has the seed phrase, every other piece of the install is replaceable — the binary can be reinstalled, the passphrase can be reset, the device can be replaced. If the user has lost the seed phrase, nothing else helps: there is no operator to call, no support form to fill in, no recovery email to verify.

This article walks through the recovery flow for [Sui Wallet Desktop](https://suiwallet.net/) from a 24-word BIP39 seed phrase. The canonical reference is the [wallet recovery walkthrough](https://suiwallet.net/learn/sui-wallet-recovery); the seed-handling fundamentals are in the [seed phrase guide](https://suiwallet.net/learn/sui-seed-phrase-guide).

## When recovery is needed

Five common scenarios:

1. **New machine.** The user is moving Sui Wallet Desktop to a different computer. Old machine still works; this is the easy case.
2. **Wiped machine.** OS reinstall, dead drive, lost laptop. The user has the seed phrase elsewhere.
3. **Lost passphrase.** The 24-word seed is fine but the wallet-side passphrase (used to encrypt local storage) is gone. The seed lets the user start fresh.
4. **Wallet upgrade.** The user is moving from Slush, Suiet, Phantom, or OKX Wallet to Sui Wallet Desktop. The [migration guide](02-migrating-from-the-legacy-sui-wallet-extension.md) covers this case at length.
5. **Ledger device replacement.** The Ledger device has been replaced and the user is re-pairing — see the [Ledger setup guide](https://suiwallet.net/learn/sui-ledger-setup) for the pairing flow.

## Pre-flight

Before importing a seed, do three things:

1. **Confirm the install is genuine.** Download Sui Wallet Desktop from [download.suiwallet.net](https://suiwallet.net/download) directly — not from a third-party mirror. Manual links: [Windows](https://suiwallet.net/download/windows), [macOS](https://suiwallet.net/download/mac), [Linux](https://suiwallet.net/download/linux). Verify the installer signature using the [security page](https://suiwallet.net/security).
2. **Use a known-good machine.** A seed typed into a compromised machine is no longer secret. The wallet's threat model assumes the OS kernel is trusted; if the user does not trust the kernel, the recovery should wait.
3. **Disconnect from the network if possible.** The seed-import step does not require network. Disconnecting Wi-Fi reduces the attack surface during typing.

## Step by step

1. **Install Sui Wallet Desktop.** On the welcome screen, choose **I already have a seed phrase**.
2. **Type the 24 words.** The UI shows 24 input fields. Type each word — do not copy-paste from a clipboard. Clipboard managers and clipboard-sniffing malware exist. Sui Wallet Desktop validates each word against the BIP39 word list as it is typed.
3. **Set a new passphrase.** The passphrase encrypts the local wallet store. It is not the seed phrase and not part of recovery. If the user forgets the passphrase later, the seed phrase still recovers funds.
4. **Confirm the derived address.** The wallet shows the first Sui address derived from the seed at the default path (`m/44'/784'/0'/0'/0'`). If the user remembers their old address, it should match. If it does not match, the seed is wrong or the path is wrong — see "Address mismatch" below.
5. **Wait for the index to load.** The wallet queries Sui RPC for objects owned by the address. NFTs, staking positions, and DeepBook orders all reappear. This takes a few seconds.
6. **Test with a small outbound transaction.** A 1 SUI test transfer to a second account under the same mnemonic confirms signing works end-to-end. The [FAQ](https://suiwallet.net/faq) covers what to do if signing fails.

That is the full happy path. For most users, total time is under five minutes.

## Address mismatch

If the wallet derives an address that does not match what the user expects, three things may have gone wrong:

- **Wrong word.** BIP39 validates each word but does not validate the whole phrase against any checksum until the user submits. One mistyped word will produce a different address. Re-read each word.
- **Word order.** A swapped pair of words is a common error.
- **Non-default derivation path.** If the user's previous wallet used a non-default path (rare on Sui), the address will differ. Sui Wallet Desktop's import flow has an **Advanced** toggle that exposes the derivation path field.

The [recovery walkthrough](https://suiwallet.net/learn/sui-wallet-recovery) covers all three.

## Recovering accounts that were derived later

Some users have multiple accounts under the same seed (path `m/44'/784'/0'/0'/0'`, `.../1`, `.../2`, ...). Sui Wallet Desktop imports account 0 by default. Additional accounts can be added through **Settings -> Accounts -> Add account** — the wallet queries each path in turn until no further objects are found.

If the user remembers having three accounts but only one shows up, **Discover accounts** scans the next several derivation indexes for funded addresses.

## Recovering a Ledger-attached account

A Ledger-attached account is not derived from the desktop wallet's seed; it is derived from the Ledger device's seed (a separate 24 words written down at device setup). To "recover" a Ledger account, plug the device into the new install and re-pair it; the address derives the same way as before. See the [Ledger page](https://suiwallet.net/ledger) and the [setup guide](https://suiwallet.net/learn/sui-ledger-setup).

If the *Ledger* device itself has been lost, the recovery path is to restore the Ledger from its own seed onto a new device. The desktop install is then re-paired with the new device.

## Recovering a zkLogin account

A [zkLogin](https://suiwallet.net/zklogin) account has no seed phrase. Recovery is "sign back in to your OAuth provider." If the OAuth account is gone, the Sui address is unrecoverable. The [zkLogin explained](https://suiwallet.net/learn/zklogin-explained) page and the [zkLogin article](08-zklogin-explained-and-how-to-use-it.md) cover the trade-off in detail.

## What to do after recovery

- **Rotate to a fresh seed if there is any doubt about the old one.** If the old seed was ever stored on a service that is now compromised, generate a new seed inside Sui Wallet Desktop and transfer funds.
- **Resume staking.** The user's existing delegations reappear automatically; no re-staking is required. See [native staking](https://suiwallet.net/staking) and [how to stake SUI](https://suiwallet.net/learn/how-to-stake-sui).
- **Reconnect dApps.** Each dApp needs to be re-authorised against the new install. This is by design.
- **Re-establish [liquid staking](https://suiwallet.net/staking/liquid) positions** if they were not automatically detected by the wallet on first index.
- **Re-place open DeepBook orders.** Existing on-chain orders persist regardless of where the wallet runs; see [DeepBook](https://suiwallet.net/deepbook) and [what is DeepBook](https://suiwallet.net/learn/what-is-deepbook).

## What recovery does not do

Recovery does not undo a transaction. If the user accidentally sent SUI to the wrong address, the seed phrase does not reverse that. Sui transactions are final at one block. The [terms of service](https://suiwallet.net/terms) and the [security page](https://suiwallet.net/security) are explicit about this.

Recovery also does not restore software-side settings — RPC URL, contact list, theme. Those are stored in the local app database, not on chain.

## Long-term seed-storage advice

The [seed phrase guide](https://suiwallet.net/learn/sui-seed-phrase-guide) is the canonical resource. The short version:

- Write the 24 words on paper or steel. Not on a phone, not in a password manager, not in a screenshot.
- Store the medium in at least two physical locations.
- Never share the words with anyone, ever — Sui Wallet Desktop support will never ask for them; see the [contact / about](https://suiwallet.net/about) page for the support channels that actually exist.

## Broader context

For wallet choice see [best Sui wallet](https://suiwallet.net/best-sui-wallet); the [Suiet](04-suiet-vs-sui-wallet-desktop.md), [Phantom](05-phantom-vs-sui-wallet-desktop.md), and [OKX](06-okx-wallet-vs-sui-wallet-desktop.md) comparison articles cover the alternatives. For broader Sui context: [what is Sui](https://suiwallet.net/learn/what-is-sui), [who is behind Sui](https://suiwallet.net/learn/who-is-behind-sui), [Sui vs. Ethereum vs. Solana](https://suiwallet.net/learn/sui-vs-ethereum-vs-solana), [tokenomics](https://suiwallet.net/learn/sui-tokenomics), [unlock schedule](https://suiwallet.net/learn/sui-token-unlock-schedule), [how to buy SUI](https://suiwallet.net/learn/how-to-buy-sui), [staking rewards](https://suiwallet.net/learn/sui-staking-rewards), [validators](https://suiwallet.net/learn/sui-validators), and the [what happened to Sui Wallet](https://suiwallet.net/learn/what-happened-to-sui-wallet) / [what is the Sui Wallet](https://suiwallet.net/learn/what-is-sui-wallet) pair. Entry point: the [learn hub](https://suiwallet.net/learn). Release log: [changelog](https://suiwallet.net/changelog). Operational: [press](https://suiwallet.net/press), [privacy](https://suiwallet.net/privacy).

## Related articles

- [Self-custody Sui wallet for desktop: an overview](01-self-custody-sui-wallet-desktop-overview.md)
- [Migrating from the legacy Sui Wallet browser extension](02-migrating-from-the-legacy-sui-wallet-extension.md)
- [Pairing a Ledger device with Sui Wallet Desktop](07-ledger-sui-wallet-desktop-setup.md)
- [zkLogin: signing in to Sui without a seed phrase](08-zklogin-explained-and-how-to-use-it.md)
