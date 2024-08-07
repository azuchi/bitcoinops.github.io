---
layout: page
permalink: /en/compatibility/trezor/

name: Trezor Suite
internal_url: /en/compatibility/trezor
logo: /img/compatibility/trezor/trezor.png
rbf:
  tested:
    date: "2021-04-13"
    platforms:
      - macOS
    version: "21.4.1"
  features:
    receive:
      notification: "na"
      list: "true"
      details: "true"
      shows_replaced_version: "true"
      shows_original_version: "false"
    send:
      signals_bip125: "true"
      list: "true"
      details: "true"
      shows_replaced_version: "true"
      shows_original_version: "false"
  examples:
    - image: /img/compatibility/trezor/rbf/send-screen.png
      caption: >
        Sending Transaction - Send transaction screen. Fee options. RBF options. By default, transaction sent as RBF.
    - image: /img/compatibility/trezor/rbf/transaction-list-sent.png
      caption: >
        Attempting Transaction Replacement - Transaction list screen showing sent transaction. No bumping options.
    - image: /img/compatibility/trezor/rbf/transaction-list-incoming-rbf.png
      caption: >
        Receiving Transaction Signaling RBF - Incoming transaction list. No RBF flag.
    - image: /img/compatibility/trezor/rbf/transaction-details-incoming-rbf.png
      caption: >
        Receiving Transaction Signaling RBF - Trezor Suite's block explorer for incoming RBF
        transaction. Does not note that the transaction has signaled RBF.
    - image: /img/compatibility/trezor/rbf/transaction-list-incoming-replacement.png
      caption: >
        Receiving Replacement Transaction - replacement transaction replaces original transaction. Block explorer no longer finds original transaction.
segwit:
  tested:
    date: "2021-04-13"
    platforms:
      - macOS
    version: "21.4.1"
  features:
    receive:
      p2sh_wrapped: "true"
      bech32: "true"
      bech32m: "true"
      default: "bech32"
    send:
      bech32: "true"
      bech32m: "true"
      change_bech32: "true"
      segwit_v1: "Fails on validation of the address."
      bech32_p2wsh: "true"
  examples:
    - image: /img/compatibility/trezor/segwit/receive-screen.png
      caption: >
        By default, Trezor generates a bech32 native P2WPKH receive addresses.
        There is also an option to generate a legacy P2SH-wrapped-P2WPKH and P2PKH addresses.
    - image: /img/compatibility/trezor/segwit/send-screen.png
      caption: >
        Trezor Suite allows for sending to any bech32 segwit v0 address.
    #- image: /img/compatibility/trezor/segwit/send-screen-segwit-v1-error.png
    #  caption: >
    #    Trezor Suite displays a validation error when attempting to send to a segwit
    #    v1 address.
---

<!-- Trezor -->

{% assign tool = page %}
{% include templates/compatibility-page.md %}
