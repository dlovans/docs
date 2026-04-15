# UIP (Universal Identity Protocol) — Business Context

## Overview
UIP is a biometric identity and signature protocol for authentication, verification, and signing. It replaces fragmented logins and DocuSign-style workflows with one cryptographically secure, government-verified identity that users carry on their phone.

## Branding

### Official colors
- **Primary:** Black (#000000)
- **Secondary:** White (#FFFFFF)
- **Accent:** Midnight blue (#1E3A8A)

The black and white color scheme represents simplicity and clarity, while midnight blue serves as the accent color for highlights and interactive elements.

## Core value proposition
**One identity. Verified everywhere.**
Replace passwords, DocuSign, and fragmented identity systems with biometric authentication and legally binding signatures.

---

## Consumer UIP app

### Main features

#### Government-verified identity
- ID verification via official documents and biometric checks (powered by Didit)
- Government-grade verification process
- One-time verification, works globally

#### Biometric authentication
- Fingerprint or face replaces all passwords
- Liveness detection to prevent fraud
- Local device processing

#### Cross-border functionality
- One identity for authentication and signing, globally
- Works across borders, governments, and businesses
- Instant proof of identity worldwide

### Quick setup (60 seconds)
1. **Get the app** — download from App Store or Google Play
2. **Quick verification** — scan ID and take a selfie
3. **Done** — start using UIP everywhere, no more passwords

### What UIP enables

- **Cross-border identity verification** — opening bank accounts with one tap, border crossings with instant proof
- **Sign legal documents** — tap to sign with biometric, legally valid and binding
- **Universal authentication** — one identity, no passwords
- **Age verification without exposing data** — returns yes/no only
- **Encrypted messaging** — important communications from banks or government, no spam

### Security features

- **Biometric authentication** — fingerprint or face, liveness detection, local device processing
- **End-to-end HTTPS** — all API calls and webhooks use TLS
- **AES-256-GCM encryption** — every PII field encrypted at rest
- **ECDSA P-256 signatures** — every critical user action is signed on-device
- **Government verification** — official document verification with live selfie matching

---

## Business UIP web app

### Value proposition
Biometric-first identity and signature protocol. Enable your business to authenticate users, sign documents, and send encrypted messages without building your own identity stack.

### Core features
- **Biometric security** — mobile-only authentication with fingerprint and face recognition
- **Global compliance** — government ID verification and legally binding signatures
- **Simple integration** — REST APIs with a QR code authentication flow

### Three powerful APIs

#### 1. Identify API
Authenticate users with biometric verification. Get verified identity information and age verification.

**Capabilities:**
- Biometric authentication
- Verified identity information
- Age and location verification

**Pricing:** $0.01 per successful authentication

#### 2. Sign API
Instant biometric document signing. Replace DocuSign with legally binding signatures powered by verified identity and biometric authentication.

**Capabilities:**
- Instant signature requests
- Legally binding documents
- Verified identity proof

**Pricing:** $0.03 per successful signature

#### 3. Message API
Send secure, encrypted messages to users. Include documents, request signatures, and control notification priority levels.

**Capabilities:**
- Encrypted messaging
- Document attachments (20MB)
- Signature requests
- Priority notification levels

**Pricing:**
- $0.03 per message without attachment
- $0.10 per message with attachment (both support signature)

### Use cases

#### Consumer applications
- **Passwordless registration** — replace email/password flows with biometric UIP accounts
- **Age and location verification** — verify age for digital platforms, clubs, events
- **High-value transactions** — secure crypto exchanges, stock trades, property purchases
- **Healthcare consent** — medical procedures, organ donation, clinical trial participation
- **Travel and immigration** — visa applications, border crossings, hotel check-ins

#### Business applications
- **Employee authentication** — save the recurring cost of password resets
- **Contract signing** — instant NDAs, employment contracts, vendor agreements
- **Compliance and auditing** — SOX compliance, financial audits, regulatory reporting
- **Financial services** — loan applications, account openings, wire transfers, KYC compliance
- **Client communication** — secure messaging for sensitive project updates

#### B2B and cross-border
- **International trade** — cross-border contracts, import/export agreements
- **Partnership verification** — verify business owner identities for joint ventures
- **Supply chain authentication** — verify supplier identities, authenticate certifications
- **Payment authorization** — large B2B payments, invoice approvals
- **Legal documentation** — cross-border litigation, international arbitration

### Why UIP

- **Composable** — mix and match APIs to create custom workflows
- **Self-managing** — UIP handles renewals, verification, and identity lifecycle management
- **Cost effective** — eliminate password management costs and reduce support overhead

---

## Permanent audit trail system

Every action returns a unique audit ID for permanent verification and compliance.

### How it works

1. **Action returns ID** — every authentication, signature, or message action returns an audit ID
2. **Store ID safely** — save the ID in your database, contracts, or compliance systems
3. **Query for verification** — use the ID to retrieve timestamp, signatory, requester, and action details

### Audit trail features

- **Unique reference generation** — one ID per action, impossible to forge, permanent record retention
- **Legal verification** — government ID verified signatories, precise UTC timestamps
- **Audit query system** — instant ID verification with signatory and requester details

### What each audit ID reveals

- **Signatory details** — full name, government ID verification status, biometric authentication time, UIP public key
- **Precise timestamp** — exact UTC timestamp, timezone info, session duration
- **Requester context** — business name, API key owner, action type

### Business applications

- **Contract verification** — store signature audit IDs in contracts for authenticity verification
- **Financial audit trails** — save transaction approval audit IDs for verified signatory and timestamp data
- **Employee authentication logs** — store login audit IDs for verified access details
- **Compliance documentation** — store audit IDs in compliance systems

### Legal and evidence

- **Court evidence** — present verified signature details as court-admissible evidence
- **Dispute resolution** — resolve "who signed when" disputes instantly
- **Regulatory investigations** — provide investigators with verified documentation

---

## Pricing model

### Simple, usage-based pricing
Pay only for what you use. No subscriptions, no hidden fees.

| API | Price | Features |
|-----|-------|----------|
| **Identify API** | $0.01 per successful authentication | Biometric authentication, verified identity, age verification, global compliance |
| **Sign API** | $0.03 per successful signature | Instant biometric signing, legally binding documents, verified identity proof, cross-border compliance |
| **Message API** | $0.03 without attachment<br/>$0.10 with attachment | End-to-end encryption, document attachments (20MB), signature requests, priority notification levels |

**Signup bonus:** $20 in credits on your first business.

---

## Technical specifications

### Security
- AES-256-GCM encryption for PII at rest
- ECDSA P-256 signatures signed on-device for every critical action
- Local biometric processing — biometric templates never leave the device
- Tamper-evident audit records (append-only with invalidation, never deletion)
- TLS 1.2+ for all API and webhook traffic

### Identity verification
- Government-issued document verification
- Live biometric matching
- Liveness detection
- Anti-fraud detection
- Multi-country support (expanding)

### Integration
- RESTful API architecture
- QR code authentication flow
- Simple polling for Identify and Sign APIs
- Webhook support for the Message API
- Comprehensive API documentation
- Quick integration (hours, not weeks)

### Compliance
- GDPR compliant
- Government-grade verification
- Court-admissible evidence
- SOX compliance support
- Cross-border legal validity

---

## Documentation notes

This is a Mintlify documentation project. **Docs are strictly external-API-facing** — they document `uip-api-external` endpoints that businesses call. Never mention internal routes (`/v1/identity`, `/v1/business`, `/v1/sessions/*`, `/v1/tokens/*`, `/v1/keys`, `/v1/audits`, `/v1/messages` under the JWT-protected group, etc.); those belong to the mobile app and dashboard, not to the public API.

Features like webhook-secret rotation, API key management, and business creation are described in terms of the dashboard UI, not the endpoints that back them.

Style guidelines:
- Use built-in Mintlify components extensively (Card, CardGroup, CodeGroup, Accordion, etc.)
- Provide clear, actionable developer documentation
- Include code examples and integration guides
- Follow Mintlify best practices for navigation and structure
- **Never use:** "self-sovereign", "zero-knowledge", "platform delegation", or "authorize API" — these concepts are not part of the v1 surface.
