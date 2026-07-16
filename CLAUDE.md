# UIP Documentation — context for editing these docs

This is the **Mintlify** docs site for UIP (Universal Identity Protocol). It is
external, developer-facing documentation for the **public v2 API**.

> ⚠️ These docs were rewritten for **v2** (June 2026). The old v1 product
> (biometric/Didit verification, an "Identify / Sign / Message API" split, QR
> polling, on-device ECDSA) **no longer exists** — do not reintroduce those concepts.

## What UIP v2 actually is
Government-attested identity **primitives** verified from the user's own **digital
wallet**. Coverage is a canonical jurisdiction + credential profile + presentation
provider ledger; Google Utopia is the active sandbox route and production Google,
Apple, and EUDI routes remain individually gated. UIP builds the request,
cryptographically verifies the wallet's signed (encrypted) response against the
issuer's trust anchors, and delivers results by webhook.

- **Primitives:** `identify`, `age_verify`, `sign`, `light_sign` (reserved/roadmap:
  `envelope` for multi-party). Chaining = the `steps[]` array, not a primitive.
- **Flow:** business `POST /v1/sessions` (API key) → hand the user the hosted
  `url` (`/s/{id}`) → the browser invokes the wallet → **signed webhook** per
  step, with `GET /v1/sessions/{id}` for one-off reconciliation.
- **Pricing:** per **successfully verified step** — age_verify $0.05, identify $0.10,
  light_sign $0.15, sign $0.30. No starter credit or subscription.

## Source of truth
The **code** is authoritative — verify claims against it before documenting:
- `uipv2-services` — the Go `/v1` API (`internal/server/router.go`), primitives
  (`internal/mdl`, `internal/wallet`), webhooks (`internal/webhook`).
- `uipv2-services/internal/catalog/ledger.go` — canonical credential coverage.
- `uipv2-web/src/lib/{primitive,pricing}.js` — canonical labels and prices.
- Repo root `ARCHITECTURE.md` / `PRIMITIVES.md` — design + the primitive philosophy.

## The doc surface (IMPORTANT — this inverted from v1)
Document the **business API** (what a customer's server calls):
`POST /v1/sessions`, `GET /v1/sessions/{id}`, `POST /v1/sessions/{id}/continue`,
`POST /v1/sessions/{id}/stop`, `GET /v1/audits/{id}`, `GET /v1/catalog`,
`GET /v1/wallets`, the public audit JWKS, and webhooks.

**Do NOT document the hosted-page transport** — `/sessions/{id}/open`, `/request`,
`/response`, `/report`, `/documents`. Those are called by UIP's hosted page, not by
the business; treat them as internal. (In v1 the rule was the opposite — ignore the
old guidance.) API keys, webhook secrets, and balance top-ups are described in terms
of the **dashboard UI**, not the endpoints behind them.

## Branding
- **Accent / brand color: Vermillion `#E34234`** (bright `#F4604E`, deep `#B22F22`)
  — the evidence-led "hanko seal" accent. Ink `#0A0A0B`, paper `#F4F2EC`.
  Mirror `uipv2-web/src/app.css` (`--color-accent`) — it's the source of truth; the
  docs theme uses deep `#B22F22` as its light-background primary for WCAG contrast.
  The old midnight-blue/cyan is retired. Domain: `uip.digital`; docs at
  `docs.uip.digital`; API base `https://api.uip.digital/v1`; support
  `support@uip.digital`.

## Style
- Use Mintlify components: `Card`/`CardGroup`, `Steps`/`Step`, `CodeGroup`,
  `Accordion`/`AccordionGroup`, `ParamField`/`ResponseField`/`Expandable`,
  `Note`/`Warning`/`Tip`, `RequestExample`/`ResponseExample`.
- Keep prose tight and developer-first; show real, accurate request/response shapes.
- Nav lives in `docs.json`; every page listed there must exist (and vice versa).
- **Don't claim features that aren't in the code.** Real wallet verification +
  encrypted transport are done; only Google Utopia is active in sandbox. Production
  ledger routes are coming soon until accepted; direct national/OIDC transports and
  `envelope` are not shipped. (There is no public roadmap page —
  it was removed; keep "coming soon / planned" as de-linked prose, don't re-add `/roadmap`.)
- **Avoid v1 ghosts:** no "biometric", "Didit", "liveness", "Message API", "QR
  polling", "Identify/Sign/Message API" split, "self-sovereign", or "zero-knowledge".
- **Retention is deliberate.** A completed `sign` result, its audit/evidence, and
  the original signed document bytes are immutable legal evidence and cannot be
  customer-deleted or scheduled for cleanup. Only uploads explicitly marked
  `transient` because they never joined a completed sign result may be purged.
- **Environment contract:** unset service `ENVIRONMENT` is local development
  (stub acceptance + relaxed issuer trust; the Simulate button also needs a web dev
  build); `SANDBOX` is Google Wallet's published Utopia test setup
  with strict sandbox trust; `PRODUCTION` activates only accepted live ledger routes
  with provisioned provider credentials and profile-specific IACA roots. Never describe
  development or coming-soon routes as production.
- **Audit claims:** records use RFC 8785 canonical hashing, a per-session hash chain,
  explicit RFC 3161 synchronous/backfill status, and a UIP ES256 signature verifiable from
  `/.well-known/uip-audit-jwks.json`. Wallet evidence is separately encrypted and
  available only where the disclosure tier permits it. Say "designed to support
  evidence"; do not promise legal enforceability, admissibility, or an HSM unless
  the deployed key's protection level independently proves that claim.
