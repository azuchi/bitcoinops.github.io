---
layout: page
permalink: /en/compatibility/copay/

name: Copay
internal_url: /en/compatibility/copay
logo: /img/compatibility/copay/copay.png
rbf:
  tested:
    date: "2018-10-02"
    platforms:
      - macOS
    version: "4.7.0"
  features:
    receive:
      notification: "false"
      list: "false"
      details: "false"
      shows_replaced_version: "false"
      shows_original_version: "false"
    send:
      signals_bip125: "false"
      list: "untested"
      details: "untested"
      shows_replaced_version: "untested"
      shows_original_version: "untested"
  examples:
    - image: /img/compatibility/copay/rbf/default-send-screen.png
      caption: >
        Sending RBF Transaction - Default send screen. No RBF options.
    - image: /img/compatibility/copay/rbf/send-miner-fee-options.png
      caption: >
        Sending RBF Transaction - Miner fee detail options.
    - image: /img/compatibility/copay/rbf/send-fee-level-options.png
      caption: >
        Sending RBF Transaction - Fee level dropdown options.
    - image: /img/compatibility/copay/rbf/send-dialog-custom-fee-level.png
      caption: >
        Sending RBF Transaction - Dialog box for custom fee level.
    - image: /img/compatibility/copay/rbf/transaction-list-sent.png
      caption: >
        Bumping RBF Enabled Transaction - Transactions list screen.
    - image: /img/compatibility/copay/rbf/transaction-details-sent.png
      caption: >
        Bumping RBF Enabled Transaction - Transaction details of sent transaction. No bumping available. NOTE Transactions not sent with RBF signaled.
    - image: /img/compatibility/copay/rbf/transaction-details-sent-warning.png
      caption: >
        Bumping RBF Enabled Transaction - Transactions details screen of sent transaction with “Amount too low to spend” warning message. Learn more link [goes here](https://support.bitpay.com/hc/en-us/articles/115004497783-What-does-the-BitPay-wallet-s-warning-amount-too-low-to-spend-mean-). Error message doesn’t make sense given a ~$7 transactions size. Note fee was 3 sat/byte.
    - image: /img/compatibility/copay/rbf/transaction-list-incoming-rbf.png
      caption: >
        Receiving RBF Transaction - Transaction list does not show any unconfirmed transactions.
    - image: /img/compatibility/copay/rbf/transaction-details-incoming-rbf.png
      caption: >
        Receiving RBF Transaction - Transaction details do not show that the transaction was RBF enabled.
segwit:
  tested:
    date: "2019-08-21"
    platforms:
      - iOS
    version: "6.1.0"
  features:
    receive:
      p2sh_wrapped: "false"
      bech32: "false"
      bech32m: "untested"
      default: "p2pkh"
    send:
      bech32: "true"
      bech32m: "untested"
      change_bech32: "false"
      segwit_v1: "Allows v1 address to be entered in the UI. Fails during broadcast."
      bech32_p2wsh: "true"
  examples:
    - image: /img/compatibility/copay/segwit/receive-screen.png
      caption: >
        Copay generates only P2PKH addresses for receiving.
    - image: /img/compatibility/copay/segwit/send-screen.png
      caption: >
        Copay can send to both P2WPKH and P2WSH bech32 addresses.
---

<!-- Copay -->

{% assign tool = page %}
{% include templates/compatibility-page.md %}
