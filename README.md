# UIP Documentation

API documentation for the **Universal Identity Protocol** -- government-attested identity primitives verified from the user's own digital wallet (US mobile driver's license via Apple Wallet & Google Wallet).

**Live Docs:** [docs.uip.digital](https://docs.uip.digital)

---

## What is UIP?

UIP is a developer platform exposing government-attested identity primitives verified from the user's own digital wallet. Each session presents the user's US mobile driver's license from Apple Wallet (Safari) or Google Wallet (Chrome) over the W3C Digital Credentials API. UIP builds the request, verifies the wallet's signed response against AAMVA issuer trust anchors, and delivers results via signed webhook.

### Primitives

One `/v1/sessions` API composes these primitives into ordered `steps`. You pay per successfully verified step — no subscription.

| Primitive | Description | Price |
|-----------|-------------|-------|
| **identify** | Selective disclosure of attested mDL attributes (default blocks: `first_name`, `last_name`, `dob`, `country`) | $0.01 |
| **age_verify** | Privacy-preserving age check — returns only a boolean; full identity is sealed in the audit | $0.01 |
| **light_sign** | Device-signs short inline terms text (WYSIWYS, no file upload) | $0.02 |
| **sign** | Device-signs a UIP-computed document hash (WYSIWYS, legally binding under US ESIGN/UETA) | $0.03 |

`envelope` (multi-party signing) is reserved/roadmap — named but not yet available.

Every `sign` / `light_sign` produces an append-only, offline-verifiable **audit** record (issuer cert chain + RFC 3161 trusted timestamp + UIP HSM signature), retrievable via `GET /v1/audits/{id}`. It is part of the signing step, not a separately priced API.

---

## Key Features

- **Wallet-native** — US mDL via Apple & Google over the W3C Digital Credentials API
- **Selective disclosure** — request only the attributes you need
- **Privacy-preserving age_verify** — boolean answer only, never the full identity
- **Legally binding signatures** — device-signed under US ESIGN/UETA, with an offline-verifiable audit proof
- **Government-attested** — credentials verified against AAMVA issuer trust anchors
- **Composable primitives** — chain steps in one audited session
- **Usage-based pricing** — no subscriptions, pay per verified step

---

## Quick Links

- [Getting Started](https://docs.uip.digital/getting-started) -- Set up in 5 minutes
- [API Reference](https://docs.uip.digital/api-reference/introduction) -- Complete API docs
- [Pricing](https://docs.uip.digital/pricing) -- Usage-based pricing
- [Get API Keys](https://uip.digital) — $20 launch credit

---

## Development

This documentation is built with [Mintlify](https://mintlify.com).

```bash
# Install Mintlify CLI
npm i -g mint

# Run local dev server
mint dev

# View at http://localhost:3000
```
