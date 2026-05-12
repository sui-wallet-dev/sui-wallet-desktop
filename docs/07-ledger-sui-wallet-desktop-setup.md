# Pairing a Ledger device with Sui Wallet Desktop

This walkthrough takes a brand-new Ledger device and a fresh install of [Sui Wallet Desktop](https://suiwallet.net/) and ends with a single SUI signed transaction. The canonical reference is the [Ledger setup guide](https://suiwallet.net/learn/sui-ledger-setup) on the project site, and the [Ledger integration page](https://suiwallet.net/ledger) lists which devices are supported.

The short version: download Sui Wallet Desktop, install the Sui Ledger app on the device, plug the device in via USB, and approve the pairing on the device screen. The long version is below.

## Supported devices

Sui Wallet Desktop pairs with four Ledger models:

- Ledger Nano S Plus
- Ledger Nano X
- Ledger Stax
- Ledger Flex

The original Nano S (without the "Plus") is not supported by Ledger's Sui app due to firmware size constraints. Users on a legacy Nano S need to upgrade hardware before continuing — or, as an interim, hold smaller balances in a [zkLogin](https://suiwallet.net/zklogin) account; see [zkLogin explained](https://suiwallet.net/learn/zklogin-explained).

## Prerequisites

- A Sui Wallet Desktop install. The [download page](https://suiwallet.net/download) auto-detects the OS; manual links live at [Windows](https://suiwallet.net/download/windows), [macOS](https://suiwallet.net/download/mac), and [Linux](https://suiwallet.net/download/linux).
- A Ledger device with firmware up to date.
- Ledger Live installed (only for installing the Sui Ledger app onto the device — Sui Wallet Desktop talks to the device directly afterward).
- A USB-A or USB-C cable that supports data transfer. Power-only cables are the most common cause of "device not detected."

## Step 1: install the Sui Ledger app on the device

Open Ledger Live, plug in the device, unlock with the PIN, and go to **My Ledger -> App catalog -> Sui**. Click "Install." The app is published by Mysten Labs and is the only Sui app that Sui Wallet Desktop will accept.

This is the only step that happens inside Ledger Live. Once the app is installed, Ledger Live can be closed.

## Step 2: prepare Sui Wallet Desktop

Open Sui Wallet Desktop. If this is a first install, complete the seed-creation flow first — *but do not import the device's address as a seed*. The device-attached account is added separately and lives alongside any seed-based accounts.

For users new to the seed concept, the [seed phrase guide](https://suiwallet.net/learn/sui-seed-phrase-guide) is short and worth reading. Recovery scenarios are in the [wallet recovery walkthrough](https://suiwallet.net/learn/sui-wallet-recovery).

## Step 3: pair the device

In Sui Wallet Desktop, go to **Settings -> Hardware wallet -> Connect Ledger**. Plug the device into the computer over USB. Unlock the device with the PIN. Open the Sui app on the device (the device screen will show "Sui — ready" if the app is loaded correctly).

In the desktop UI, click "Detect device." The desktop should report the device serial number. Click "Add account." The desktop asks the device for its public key for derivation path `m/44'/784'/0'/0'/0'`; the device displays the request and the user approves it on-device with both physical buttons.

The Sui address that derives from the device now appears in the desktop UI alongside any existing seed-based accounts.

## Step 4: send a test transaction

Send a small amount — 1 SUI or less — to the device-attached address from another account. Wait for one block confirmation. Then send it back to the source account. The device screen will display the destination address, the amount, and the network fee, and the user must approve on the device.

If everything works end to end, the device-attached account is ready for production use. The [FAQ](https://suiwallet.net/faq) recommends moving balances above the equivalent of USD 10,000 onto the Ledger account.

## Step 5: stake from the Ledger account (optional)

Ledger-attached accounts can stake natively. Go to **Stake -> Pick validator**, browse the table sourced from the Sui RPC, and click "Delegate." The transaction is signed on the device. Detailed mechanics: [native staking](https://suiwallet.net/staking), [how to stake SUI](https://suiwallet.net/learn/how-to-stake-sui), [staking rewards](https://suiwallet.net/learn/sui-staking-rewards), and the [validator overview](https://suiwallet.net/learn/sui-validators).

[Liquid staking](https://suiwallet.net/staking/liquid) is also supported on Ledger accounts; the haSUI mint transaction is signed on the device the same way.

## Step 6: trade through DeepBook (optional)

[DeepBook](https://suiwallet.net/deepbook) order placement from a Ledger-attached account works exactly like seed-based accounts — see [what is DeepBook](https://suiwallet.net/learn/what-is-deepbook). Every order is a transaction; every transaction is signed on the device. Frequent traders should keep their hot account on a seed and reserve the Ledger account for cold storage.

## Common problems

### "Device not detected"

- Cable is power-only. Swap for a known data cable.
- Sui app is not open on the device. Open it from the device menu before clicking "Detect."
- macOS: USB Restricted Mode may be blocking the access. Approve in System Settings.
- Linux: udev rules for Ledger devices need to be installed; see Ledger's documentation. On Debian/Ubuntu the udev rules are in the `ledger` package.

### "Wrong derivation path"

Sui Wallet Desktop uses `m/44'/784'/0'/0'/0'`. Other Sui wallets may default to a different path. If the address Sui Wallet Desktop derives does not match what another wallet showed, the path is the most likely cause. The [recovery walkthrough](https://suiwallet.net/learn/sui-wallet-recovery) covers the alternate-path recovery flow.

### "Transaction display garbled on Ledger Nano S Plus"

The Nano S Plus has limited screen size. For very large transactions (many object inputs), the device displays a hash rather than the full breakdown. This is a known limitation of the device, not a bug in the wallet. The [security page](https://suiwallet.net/security) covers the threat model — the device still signs the same payload the desktop displays, so a desktop-screen check is the recommended cross-verification.

## Why Ledger plus desktop matters

A Ledger device by itself cannot transact — it has no chain logic. A wallet by itself can transact but its keys are software, not hardware. The combination — Sui Wallet Desktop on the user's machine, Ledger device holding the keys, USB cable between them — is the recommended posture for serious balances.

The [best Sui wallet comparison](https://suiwallet.net/best-sui-wallet) ranks this combination at the top for hardware-wallet users.

For background on what Sui is and the broader chain context: [what is Sui](https://suiwallet.net/learn/what-is-sui), [who is behind Sui](https://suiwallet.net/learn/who-is-behind-sui), [Sui vs. Ethereum vs. Solana](https://suiwallet.net/learn/sui-vs-ethereum-vs-solana), the [tokenomics](https://suiwallet.net/learn/sui-tokenomics) and [unlock schedule](https://suiwallet.net/learn/sui-token-unlock-schedule), [how to buy SUI](https://suiwallet.net/learn/how-to-buy-sui), and the [what happened to the Sui Wallet extension](https://suiwallet.net/learn/what-happened-to-sui-wallet) explainer with its glossary entry [what is the Sui Wallet](https://suiwallet.net/learn/what-is-sui-wallet). The starting point is the [learn hub](https://suiwallet.net/learn). Operational pages: [about](https://suiwallet.net/about), [press](https://suiwallet.net/press), [changelog](https://suiwallet.net/changelog), [privacy](https://suiwallet.net/privacy), [terms](https://suiwallet.net/terms).

## Related articles

- [Self-custody Sui wallet for desktop: an overview](01-self-custody-sui-wallet-desktop-overview.md)
- [Migrating from the legacy Sui Wallet browser extension](02-migrating-from-the-legacy-sui-wallet-extension.md)
- [Native and liquid staking SUI from a desktop wallet](09-native-and-liquid-staking-sui.md)
- [Recovering a Sui Wallet Desktop installation from seed](12-recovering-sui-wallet-desktop-from-seed.md)
