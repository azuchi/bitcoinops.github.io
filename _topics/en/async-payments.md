---
title: Async payments

## Optional.  Shorter name to use for reference style links e.g., "foo"
## will allow using the link [topic foo][].  Not case sensitive
# shortname: foo

## Optional.  An entry will be added to the topics index for each alias
#title-aliases:
#  - Foo

## Required.  At least one category to which this topic belongs.  See
## schema for options
topic-categories:
  - Lightning Network

## Optional.  Produces a Markdown link with either "[title][]" or
## "[title](link)"
#primary_sources:
#    - title: Test
#    - title: Example
#      link: https://example.com

## Optional.  Each entry requires "title" and "url".  May also use "feature:
## true" to bold entry and "date"
optech_mentions:
  - title: Paying offline nodes
    url: /en/newsletters/2021/10/20/#paying-offline-ln-nodes

  - title: Trampoline routing and async mobile payments
    url: /en/newsletters/2022/06/15/#trampoline-routing-and-mobile-payments

  - title: "Eclair #2435 adds support for a basic form of async payments when trampoline relay is used"
    url: /en/newsletters/2022/10/05/#eclair-2435

  - title: "2022 year-in-review: async payments"
    url: /en/newsletters/2022/12/21/#async-payments

  - title: "Eclair #2464 adds a trigger useful for allowing one node to deliver an async payment to a peer"
    url: /en/newsletters/2023/01/04/#eclair-2464

  - title: "Idea for non-interactive channel open commitments may allow fast rebalancing for async payments"
    url: /en/newsletters/2023/01/11/#non-interactive-ln-channel-open-commitments

  - title: Request for proof that an async payment was accepted
    url: /en/newsletters/2023/01/25/#request-for-proof-that-an-async-payment-was-accepted

  - title: Using adaptor signatures to prove an async payment was accepted
    url: /en/newsletters/2023/02/01/#ln-async-proof-of-payment

  - title: "LDK #2973 adds support for intercepting onion messages to facilitate async payments"
    url: /en/newsletters/2024/05/17/#ldk-2973

  - title: "LDK #3125 introduces support for encoding and parsing messages needed for async payments"
    url: /en/newsletters/2024/07/05/#ldk-3125

  - title: "Eclair #2865 enables waking up a disconnected mobile peer for async payments or onion messages"
    url: /en/newsletters/2024/09/06/#eclair-2865

  - title: "LDK #3140 adds support for paying static BOLT12 invoices to send async payments"
    url: /en/newsletters/2024/09/20/#ldk-3140

  - title: "LDK #3618 implements the client-side logic for async payments"
    url: /en/newsletters/2025/07/04/#ldk-3618

  - title: "LDK #3628 implements the server-side logic for async payments"
    url: /en/newsletters/2025/07/18/#ldk-3628

## Optional.  Same format as "primary_sources" above
see_also:
  - title: Trampoline payments
    link: topic trampoline payments

  - title: PTLCs
    link: topic ptlc

  - title: Signature adaptors
    link: topic adaptor signatures

  - title: Proof of payment
    link: topic proof of payment

## Optional.  Force the display (true) or non-display (false) of stub
## topic notice.  Default is to display if the page.content is below a
## threshold word count
#stub: false

## Required.  Use Markdown formatting.  Only one paragraph.  No links allowed.
## Should be less than 500 characters
excerpt: >
  **Async payments** are payments that are made when the receiver is
  offline.  Onchain payments are async but interactive protocols like LN
  may require cooperation of a third party to enable async payments.
---
Traditional onchain Bitcoin payments are asynchronous (async) because
the receiver can generate an output script (Bitcoin address) and give
that address to the spender at any time, and then the spender can pay
that address at any time---even when the receiver is offline.
The process of securing that payment (receiving block confirmations)
doesn't require any action from the receiver.

For LN, the receiver needs to release a secret at the time a payment is
received in order to secure that payment.  This requires that both the
sender and receiver of a payment both be online at the same time.  In
many cases, it's not a significant problem for a spender to be online
because they've initiated the spending process and can trigger actions
to ensure the payment gets sent.  But for some receivers, being online
to receive a payment is more of a challenge.  For example, an LN node
running on a mobile phone may be entirely disconnected from the internet
some of the time and may not have access to the network other times
because the node's app is running in the background.

A [2021 discussion][offline ln] about improving this user experience led
to several ideas about allowing a forwarding node to hold a payment for
a receiving node until the receiver was known to be online.  The best
described trustless method in that discussion required the use of
[PTLCs][topic ptlc], which have not yet been added to LN as of the end
of 2022.  An alternative [method][trampoline method], which could be
implemented in the existing protocol, involved the use of trampoline
relays.

Async payments are also a key feature of the [Ark][topic ark] protocol.

{% include references.md %}
{% include linkers/issues.md issues="" %}
[offline ln]: https://gnusha.org/url/https://lists.linuxfoundation.org/pipermail/lightning-dev/2021-October/003307.html
[trampoline method]: /en/newsletters/2022/06/15/#trampoline-routing-and-mobile-payments
