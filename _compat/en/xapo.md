---
layout: page
permalink: /en/compatibility/xapo/

name: Xapo
internal_url: /en/compatibility/xapo
logo: /img/compatibility/xapo/xapo.png
rbf:
  tested:
    date: "2018-11-05"
    platforms:
      - iOS
    version: "4.6.1"
  features:
    receive:
      notification: "false"
      list: "false"
      details: "false"
      shows_replaced_version: "true"
      shows_original_version: "true"
    send:
      signals_bip125: "false"
      list: "untested"
      details: "untested"
      shows_replaced_version: "untested"
      shows_original_version: "untested"
  examples:
    - image: /img/compatibility/xapo/rbf/send-screen.png
      caption: >
        Sending Transaction - Default wallet send screen
    - image: /img/compatibility/xapo/rbf/send-miner-fee-options.png
      caption: >
        Sending Transaction - Send transaction, choose miner fees. No RBF options.
    - image: /img/compatibility/xapo/rbf/tranasction-details-sent.png
      caption: >
        Attempting Transaction Replacement - Transaction not sent with RBF signaled. No bumping possible.
    - image: /img/compatibility/xapo/rbf/notification-incoming-rbf.png
      caption: >
        Receiving Transaction Signaling RBF - Email notification. No RBF warning.
    - image: /img/compatibility/xapo/rbf/transaction-list-incoming-rbf.png
      caption: >
        Receiving Transaction Signaling RBF - Incoming RBF signaling transaction in list. No label for RBF.
    - image: /img/compatibility/xapo/rbf/transaction-details-incoming-rbf.png
      caption: >
        Receiving Transaction Signaling RBF - Incoming RBF signaling transaction details. No RBF flag.
    - image: /img/compatibility/xapo/rbf/transaction-list-incoming-replacement.png
      caption: >
        Receiving Replacement Transaction - Incoming replacement transaction. Both transactions show. Balance credited twice.
    - image: /img/compatibility/xapo/rbf/dashboard-incoming-replacement.png
      caption: >
        Receiving Replacement Transaction - Dashboard shows 2 incoming transaction. Balance includes both transactions.
    - image: /img/compatibility/xapo/rbf/notification-incoming-replacement.png
      caption: >
        Receiving Replacement Transaction - Additional email notification for replacement transaction.
    - image: /img/compatibility/xapo/rbf/transaction-list-replacement-confirmed.png
      caption: >
        Receiving Replacement Transaction - Even after replacement transaction has 100 confirms, original transaction stays pending.
segwit:
  tested:
    date: "2019-07-27"
    platforms:
      - iOS
    version: "5.0.3"
  features:
    receive:
      p2sh_wrapped: "true"
      bech32: "false"
      bech32m: "untested"
      default: "p2sh_wrapped_p2wsh"
    send:
      bech32: "true"
      bech32m: "untested"
      change_bech32: "false"
      segwit_v1: "Xapo allows users to create segwit v1 transactions in the UI. However,
        the transaction gets stuck as pending for an indeterminate period of time."
      bech32_p2wsh: "true"
  examples:
    - image: /img/compatibility/xapo/segwit/receive-screen.png
      caption: >
        Xapo only generates P2SH wrapped P2WSH receive addresses.
    - image: /img/compatibility/xapo/segwit/send-screen.png
      caption: >
        Xappo allows sending to any segwit v0 address.
    #- image: /img/compatibility/xapo/segwit/send-screen-segwit-v1-pending.png
    #  caption: >
    #    Xapo allows users to create segwit v1 transactions in the UI. However,
    #    the transaction gets stuck as pending.
---

<!-- Xapo -->

{% assign tool = page %}
{% include templates/compatibility-page.md %}
