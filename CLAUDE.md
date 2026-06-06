# UIP Documentation — context for editing these docs

This is the **Mintlify** docs site for UIP (Universal Identity Protocol). It is
external, developer-facing documentation for the **public v2 API**.

> ⚠️ These docs were rewritten for **v2** (June 2026). The old v1 product
> (biometric/Didit verification, an "Identify / Sign / Message API" split, QR
> polling, on-device ECDSA) **no longer exists** — do not reintroduce those concepts.

## What UIP v2 actually is
Government-attested identity **primitives** verified from the user's own **digital
wallet**. Today: US mobile driver's license (ISO 18013-5 mdoc) via Apple Wallet /
Google Wallet over the **W3C Digital Credentials API**. UIP builds the request,
cryptographically verifies the wallet's signed (encrypted) response against the
issuer's trust anchors, and delivers results by webhook.

- **Primitives:** `identify`, `age_verify`, `sign`, `light_sign` (reserved/roadmap:
  `envelope` for multi-party). Chaining = the `steps[]` array, not a primitive.
- **Flow:** business `POST /v1/sessions` (API key) → hand the user the hosted
  `url` (`/s/{id}`) → wallet completes on-device → **signed webhook** per step.
- **Pricing:** per **successfully verified step** — identify $0.01, age_verify $0.01,
  light_sign $0.02, sign $0.03. $20 launch credit. No subscription.

## Source of truth
The **code** is authoritative — verify claims against it before documenting:
- `uipv2-services` — the Go `/v1` API (`internal/server/router.go`), primitives
  (`internal/mdl`, `internal/wallet`), webhooks (`internal/webhook`).
- `uipv2-web/src/lib/{primitive,coverage,pricing}.js` — canonical labels, wallet
  coverage, and prices.
- Repo root `ARCHITECTURE.md` / `PRIMITIVES.md` — design + the primitive philosophy.

## The doc surface (IMPORTANT — this inverted from v1)
Document the **business API** (what a customer's server calls):
`POST /v1/sessions`, `GET /v1/sessions/{id}`, `POST /v1/sessions/{id}/continue`,
`POST /v1/sessions/{id}/stop`, `GET /v1/wallets`, and webhooks.

**Do NOT document the hosted-page transport** — `/sessions/{id}/open`, `/request`,
`/response`, `/report`, `/documents`. Those are called by UIP's hosted page, not by
the business; treat them as internal. (In v1 the rule was the opposite — ignore the
old guidance.) API keys, webhook secrets, and balance top-ups are described in terms
of the **dashboard UI**, not the endpoints behind them.

## Branding
- **Primary:** Black (#000000) · **Secondary:** White (#FFFFFF) · **Accent:**
  Midnight blue (#1E3A8A). Domain: `uip.digital`; docs at `docs.uip.digital`;
  API base `https://api.uip.digital/v1`; support `support@uip.digital`.

## Style
- Use Mintlify components: `Card`/`CardGroup`, `Steps`/`Step`, `CodeGroup`,
  `Accordion`/`AccordionGroup`, `ParamField`/`ResponseField`/`Expandable`,
  `Note`/`Warning`/`Tip`, `RequestExample`/`ResponseExample`.
- Keep prose tight and developer-first; show real, accurate request/response shapes.
- Nav lives in `docs.json`; every page listed there must exist (and vice versa).
- **Don't claim features that aren't in the code.** Real wallet verification +
  encrypted transport are done; the international/OIDC wallets and `envelope` are
  roadmap (`/roadmap`), not shipped — frame them as such.
- **Avoid v1 ghosts:** no "biometric", "Didit", "liveness", "Message API", "QR
  polling", "Identify/Sign/Message API" split, "self-sovereign", or "zero-knowledge".
