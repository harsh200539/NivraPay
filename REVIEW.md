# NivraPay review — 17 October 2026

Branding adaptation of gxurav1710/YouPI-PG at commit `242969c61fead71de696cec27780ec3c7ddd700b`. This is not an independent payment-engine implementation. Source history, upstream author and commercial license declaration are retained. The referenced LICENSE file was absent.

## Changes

- NivraPay web display names, default merchant name, checkout N monogram, and root workspace name.
- New merchants default to Hide Powered By. Existing merchant configuration is preserved.
- Android display labels updated in source only; original APKs are retained and still carry upstream branding.
- Original screenshots/videos remain upstream demonstration assets, not new NivraPay screenshots.
- Original documentation is preserved under docs/UPSTREAM_README.md.

## Verification

65 tests across 12 selected regression suites passed before and after customization. An isolated preloader restricted Node TCP and DNS to localhost; external webhook destinations could not receive test traffic. The original full runner was stopped after automatic review identified its external merchant webhook. It was not rerun with external access.

88 tracked files across the core engine, common package, merchant SDK, observer SDK, payment API, Gmail observer and SMS observer are byte-for-byte identical to upstream. Routes, SDK globals, DOM event names, cryptographic fingerprint strings, schemas, payment amounts, timers and state transitions are preserved. All eleven inline browser scripts retain their original parser diagnostic results.

| Suite | Before / after |
| --- | --- |
| `packages/common/src/__tests__/common.test.js` | PASS / PASS |
| `packages/db/src/__tests__/db.test.js` | PASS / PASS |
| `packages/core/src/__tests__/core.test.js` | PASS / PASS |
| `packages/core/src/__tests__/queue-timing.test.js` | PASS / PASS |
| `packages/core/src/__tests__/webhook-engine.test.js` | PASS / PASS |
| `packages/merchant-sdk/src/__tests__/merchant-sdk.test.js` | PASS / PASS |
| `packages/merchant-sdk/src/__tests__/youpi-universal-integration.test.js` | PASS / PASS |
| `apps/checkout-portal/src/__tests__/checkout-portal.test.js` | PASS / PASS |
| `apps/merchant-admin/src/__tests__/merchant-admin.test.js` | PASS / PASS |
| `apps/payment-api/src/__tests__/whitelabel-branding.test.js` | PASS / PASS |
| `apps/payment-api/src/__tests__/counter-payments.test.js` | PASS / PASS |
| `apps/payment-api/src/__tests__/selling-modes-and-cod.test.js` | PASS / PASS |

## Existing upstream defects retained

1. `npm run build` fails: ObserverSource.ANDROID is missing from a TypeScript enum, and eleven workspace tsconfig.json files are missing. The identical error messages were reproduced in a clean upstream source extraction.
2. The demo storefront `apps/coin-wallet-store/src/store.html` contains a stray closing brace in its inline JavaScript. The same parser error occurs before and after branding. The selected regression suites do not detect this browser-script error.
3. The help portal HTML is a placeholder reading “Feature not available.”
4. The bundled Android build script uses hardcoded Windows Android/JDK paths. No new APK was produced in this environment.

No real payment, Google account connection, WhatsApp pairing, bank link, production deployment, or external webhook delivery was performed during verification. This is a source customization with known upstream defects, not a production-readiness certification.

## Project archive

Source files and a Git bundle retain the original commit history. Large upstream MP4 demonstrations are represented by their original Git LFS pointers; they are not runtime dependencies. Restore history and optionally fetch the recordings with:

```bash
GIT_LFS_SKIP_SMUDGE=1 git clone NivraPay-history.bundle nivrapay
cd nivrapay
git remote rename origin archive
git remote add upstream https://github.com/gxurav1710/YouPI-PG.git
git lfs pull upstream
```

Review the upstream commercial terms before publishing or distributing the derivative. Original source notices and commit history are retained.
