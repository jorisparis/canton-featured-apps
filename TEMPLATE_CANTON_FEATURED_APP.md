# Canton Featured App – 00XX

> Replace `00XX` with the PR number that introduces this document and then delete this comment.
>
> This document is a **descriptive record** for a Canton Featured App.
> It is **non-governance**, **non-normative**, and does not define or modify any
> Canton Improvement Proposal (CIP).

---

## 1. App identity

- **App name:**
- **Organization / legal entity:**
- **Website:**
- **Public repository (if any):**
- **Primary contact:**
- **Security / technical contact (optional):**
- **Application-controlled PartyId(s):**
  - `<PartyId or namespace>`
  - `<PartyId or namespace>`

(These are the PartyIds operated by the application that may anchor
activity marker–relevant ledger state transitions.)

---

## 2. App summary

Provide a concise, factual description of what the application does.

- 2–5 sentences
- No marketing language
- No forward-looking statements

---

## 3. Role of Canton Network

Describe why and how the application uses Canton Network.

Examples:
- settlement or coordination layer
- issuance or registry infrastructure
- privacy-preserving workflows
- protocol or infrastructure signaling

---

## 4. Operational usage

- **Application operational status:** (e.g. development, pilot, limited production, production)
- **Primary workflows on Canton:**
  - bullet list of concrete workflows

---

## 5. Featured App Activity Markers (CIP-0047)

> *This section declares the Featured App Activity Markers emitted by the application, as defined in CIP-0047. The information is declarative and provided for transparency. This document does not define, enforce, or modify activity marker mechanics.*

> ***Ledger anchoring:** All declared activity markers correspond to finalized state transitions recorded on Canton Network. Activity markers are not emitted in response to UI actions or API calls alone, prior to ledger finality, or for speculative/reversible actions. The ledger is the sole source of truth for activity marker eligibility.*

### 5.1 Declared activity markers

For each activity marker, provide the corresponding metadata fields defined in
CIP-0047 and applicable amendments.

Only activity markers intended to be public should be listed.

#### Marker format

```
activityCategory: <Enum>
activityDescription: <Text>
estimatedNotionalRange: <Enum | None>
assetClass: <Enum | None>
userCountIndicator: <Enum>
Notes: <Optional context>
```

#### Illustrative examples (non-normative)

**Example A — Single-user DvP settlement**

```
activityCategory: DvPSettlement
activityDescription: Single-user initiated delivery-versus-payment settlement
estimatedNotionalRange: $100k–$1M
assetClass: Security
userCountIndicator: SingleUser
Notes: Represents one end user intentionally initiating a settlement.
```

**Example B — Batch settlement across multiple users**

```
activityCategory: DvPSettlement
activityDescription: Batch settlement of matched trades across multiple users
estimatedNotionalRange: >= $10M
assetClass: Security
userCountIndicator: MultipleUsersDistinctParties
Notes: One app marker represents aggregated activity across many users.
```

**Example C — Infrastructure / validator activity (no asset)**

```
activityCategory: InfrastructureHealth
activityDescription: Validator liveness or protocol health signal
estimatedNotionalRange: None
assetClass: None
userCountIndicator: ValidatorOperator
Notes: Protocol-level activity; no asset movement involved.
```

**Example D — Wallet-mediated wrapped asset activity**

```
activityCategory: AssetRepresentation
activityDescription: Wallet-mediated wrapping, unwrapping, or movement of a represented asset
estimatedNotionalRange: Variable
assetClass: DigitalAsset
userCountIndicator: MultipleUsersPotentiallySharedWallet
Notes: Represents ledger-finalized activity initiated by wallet infrastructure.
May occur at high frequency due to user behavior or automated wallet logic.
```

---

### 5.2 Emission strategy

Describe how app marker volume relates to ledger activity:

- **Emission basis:** [Per transaction | Value-proportional | Quantity-based | Batched]
- **Rate limiting:** [Real-time | Throttled | Batched]
- **Calculation:** [If applicable, formula or ratio]

#### Emission approaches

| Approach | Description | Example |
|----------|-------------|---------|
| **Flat rate** | 1 app marker per transaction | Each trade settlement = 1 app marker |
| **Value-based** | App markers proportional to transaction value | 1 app marker per $100 of value |
| **Quantity-based** | App markers based on units processed | 1 app marker per 1000 shares |
| **Batched** | Multiple transactions → one app marker | Daily batch = 1 app marker |

#### Example: Value-proportional emission

> "One app marker per $100 of finalized transaction value, rounded up per individual transaction.
> For example, a $5,000 stock issuance creates 50 app markers. App markers are rate-limited to 1–5 TPS
> to avoid network congestion, minted asynchronously after transaction finality."

---

### 5.3 Non-emitting activities

As a general principle, Featured App Activity Markers are not emitted for
activity that does not represent an independent, finalized economic state
transition on the ledger.

Illustrative examples include:

- onboarding or account setup
- configuration, reference data, or metadata updates
- retries, failures, or rollback-related actions
- cancellations, reversals, or voided workflows
- internal operational, administrative, or maintenance actions

This list is illustrative, descriptive, and explicitly non-exhaustive.

---

## 6. Abuse mitigation (descriptive)

Describe high-level controls that discourage automated or artificial app marker generation.

**Useful disclosures:**
- Economic friction (transaction fees, minimum values, staking requirements)
- Access controls (KYC, waitlists, invitation-only)
- Rate limiting approach (per-user, per-entity, global)
- Monitoring and manual review processes

**Not required:** Implementation details, specific thresholds, or security-sensitive information.

The goal is to provide context about whether app marker generation involves real economic activity vs. being easily automatable.

---

## 7. Changelog

- YYYY-MM-DD — Initial version
- YYYY-MM-DD — Update summary

Material changes to activity marker behavior (e.g. introduction of new
marker categories, changes to aggregation logic, or changes in emission
patterns) should be reflected in this document promptly.
