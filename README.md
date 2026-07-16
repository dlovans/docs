# UIP Documentation

API documentation for the **Universal Identity Protocol** -- government-attested identity primitives verified from the user's own digital wallet through a canonical country/credential/provider route.

**Live Docs:** [docs.uip.digital](https://docs.uip.digital)

> **Private beta.** Google Sandbox runs the real encrypted wallet path with fictional
> Utopia credentials. Every production Google, Apple, or EUDI route requires its
> provider/issuer access, trust material, acceptance, and UIP production approval.

---

## What is UIP?

UIP is a developer platform exposing government-attested identity primitives verified from the user's own digital wallet. Each session pins one country, credential profile, and presentation provider. UIP builds the request, verifies the wallet's signed response against that profile's trust anchors, and delivers results via signed webhook.

### Primitives

One `/v1/sessions` API composes these primitives into ordered `steps`. You pay per successfully verified step — no subscription.

| Primitive | Description | Price |
|-----------|-------------|-------|
| **identify** | Selective disclosure of requested attested credential attributes | $0.10 |
| **age_verify** | Business-redacted age check — returns the boolean + threshold; signer evidence is sealed in the audit | $0.05 |
| **light_sign** | Device-signs short inline terms text (WYSIWYS, no file upload) | $0.15 |
| **sign** | Device-signs a UIP-computed document manifest hash (WYSIWYS) | $0.30 |

`envelope` (multi-party signing) is reserved/roadmap — named but not yet available.

Every verified step produces an immutable **audit** record. Its RFC 8785 hash and UIP ES256 signature can be checked against the public JWKS; authorized disclosures also contain the wallet material needed to re-run ISO mdoc verification. RFC 3161 status is explicit: `ts_status` records the synchronous outcome, while a recovered token is marked `ts_backfilled`. Retrieve the record with `GET /v1/audits/{id}`. The audit is part of the step, not a separately priced API.

Completed `sign` results include the original signed document bytes as immutable evidence. They are not customer-deletable or time-purged. Cleanup applies only to explicitly transient uploads that never joined a completed sign result.

---

## Key Features

- **Wallet-native** — credential trust and presentation-provider transport stay separate
- **Selective identity disclosure** — choose the `identify` attributes you need
- **Business-redacted age_verify** — boolean to the customer; encrypted identity retained as evidence
- **Evidence-oriented signatures** — device-signed content with a reproducible audit hash, public UIP signature, and wallet verification material
- **Issuer-attested** — credentials verified against the environment's configured IACA trust anchors
- **Composable primitives** — chain steps in one audited session
- **Usage-based pricing** — no subscriptions, pay per verified step

---

## Quick Links

- [Quickstart](https://docs.uip.digital/quickstart) -- Create a session and receive a result
- [API Reference](https://docs.uip.digital/api-reference/introduction) -- Complete API docs
- [Pricing](https://docs.uip.digital/pricing) -- Usage-based pricing
- [Get API Keys](https://uip.digital) — create a business, fund its wallet, and mint a key

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
