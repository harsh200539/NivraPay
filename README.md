# NivraPay

NivraPay is a self-hosted UPI checkout and merchant operations project maintained by Harshvardhan Patil. It brings together QR payments, bank-alert payment verification, WhatsApp OTP, and COD/counter-payment workflows.

## What it does

1. A storefront creates a payment session through the JavaScript SDK or REST API.
2. Checkout offers a dynamic UPI QR and supported app intents; WhatsApp OTP can verify the customer.
3. An Android/SMS or Gmail observer forwards bank-credit notifications.
4. The engine matches amount, UTR and timing, updates the payment state, and sends a signed merchant webhook.
5. Merchant controls manage receiving accounts, branding, observers and available payment methods. COD, cash-counter and card-counter modes retain their upstream behavior.

Payments use your own receiving UPI account. Bank-alert matching depends on working observers and does not establish a direct bank-API integration. A card-counter record does not itself process a card payment.

## Stack and services

Node.js JavaScript/TypeScript workspaces; native `node:sqlite`; HTML/CSS/JavaScript interfaces; Android observer source and upstream APKs. Use Node.js 24 for the reviewed runtime.

| Service | Default port |
| --- | --- |
| Demo storefront | 5000 |
| Merchant admin | 6001 |
| SMS observer | 6002 |
| Gmail observer | 6003 |
| Payment API | 6100 |
| Checkout portal | 7000 |
| Control center | 8090 |

## Local setup

```bash
npm ci
cp .env.example .env
npm run db:setup
npm run dev
```

Configure your own credentials, receiving VPA, bank observers and webhooks before real transactions. No real payment was performed during this review.

## Branding and compatibility

Web display branding and new-merchant defaults use NivraPay. New merchants default to `hidePoweredBy: true`. Existing merchant settings are preserved: update the app name and Hide Powered By option through Merchant Admin for an existing database. The checkout decorative monogram uses N.

SDK exports (`Youpi.pay`), `/youpi.js`, `data-youpi-*`, `youpi:*` events, API routes, database paths, Android package IDs and cryptographic fingerprint strings remain compatible. The payment engines, schemas, timing, queue, webhook logic and authentication algorithms were not changed.

Android source display labels use NivraPay. Included APKs and recorded screenshots/videos are unchanged upstream assets; rebuilding native binaries and refreshing recorded media remain pending.

## Review findings

The help portal HTML is a placeholder (`Feature not available`). The upstream README contains product/security claims that this review does not certify. The original full regression runner includes external webhook destinations; use the local-only verification described in `REVIEW.md`.

See [upstream documentation](docs/UPSTREAM_README.md), [integration contracts](AGENTS.md), and [configuration](docs/CONFIGURATION.md).

## Source notices

Original source, author information, and licensing details are retained in [UPSTREAM.md](UPSTREAM.md).
