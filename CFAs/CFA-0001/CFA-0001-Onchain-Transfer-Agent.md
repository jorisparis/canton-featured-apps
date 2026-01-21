# Canton Featured App – 0001

> This document is a **descriptive record** for a Canton Featured App.
> It is **non-governance**, **non-normative**, and does not define or modify any
> Canton Improvement Proposal (CIP).

---

## 1. App identity

- **App name:** Onchain Transfer Agent (OTA)
- **Organization / legal entity (operator):** Fairmint, Inc. and subsidiary
- **Website:** https://transfer-agent.xyz 
- **Public repository (if any):** N/A (proprietary application)
- **Primary contact:** transfer-agent@fairmint.com
- **Security / technical contact:** nick@fairmint.com

**Application-controlled PartyId(s):**
- `onchain-transfer-agent::12204a039322c01e9f714b56259c3e68b69058bf5dfe1debbe956c698f905ceba9d7`

---

## 2. App summary

Onchain Transfer Agent (OTA), operated by Fairmint and its regulated Transfer Agent subsidiary, is an application that
finalizes and records issuance and ownership changes for tokenized securities on
Canton Network. OTA maintains authoritative shareholder ownership state and
executes legally and economically effective ownership transitions using
privacy-preserving, on-ledger workflows with cryptographic auditability.

This document reflects specifically on the Transfer Agent service layer where
economic ownership state is finalized on-ledger.

---

## 3. Role of Canton Network

Canton Network provides the authoritative ledger and coordination layer on which
Onchain Transfer Agent finalizes ownership state for tokenized securities. OTA
relies on Canton’s privacy-preserving transaction model and multi-party
coordination capabilities to record issuance and transfer events as finalized,
cryptographically verifiable state transitions.

Canton enables OTA to ensure that ownership changes are:
- finalized with ledger-level consensus,
- visible only to entitled parties,
- auditable over time, and
- resistant to conflicting or duplicate state updates.

By anchoring Transfer Agent actions to Canton ledger finality, OTA ensures that
economically meaningful ownership transitions are recorded as a single, consistent
source of truth.


---

## 4. Operational usage

- **Operational status:** Production
- **Environment(s):** Production

### Primary on-ledger workflows

Onchain Transfer Agent performs the following **ledger-final workflows** on Canton
Network:

- **Issuance finalization:** Recording the creation of tokenized securities and
  initial ownership positions.
- **Ownership transfer:** Recording transfer of ownership between parties,
  resulting in updated authoritative ownership state.
- **Settlement outcome recording:** Recording the finalized outcome of coordinated
  Free-of-Payment (FoP) or Delivery-versus-Payment (DvP) settlement workflows.
- **Usage constraint application and release:** Recording and applying protocol-
  enforced exclusivity constraints to prevent conflicting reuse of tokenized
  ownership units while referenced by external financial arrangements.

Each workflow results in a finalized, on-ledger state transition that creates,
transfers, or conditions enforceable economic rights associated with tokenized
securities.


---

## 5. Featured App Activity Markers (CIP-0047)

This section declares the **Featured App Activity Markers** emitted by Onchain
Transfer Agent, as defined in **CIP-0047**.

Activity markers are emitted only for **finalized, on-ledger state transitions**
performed by OTA that create, transfer, or condition enforceable economic rights
associated with tokenized securities. Activity markers are not emitted for UI
actions, API calls, preparatory steps, or off-ledger processes.

**Ledger anchoring:**  
All activity markers correspond to finalized Canton ledger transactions. Ledger
finality is the sole source of truth for marker eligibility.


### 5.1 Declared activity markers

#### Issuance finalization

```
activityCategory: Issuance
activityDescription: Finalization of issuance of tokenized securities resulting
in the creation of enforceable ownership positions.
estimatedNotionalRange: Variable
assetClass: Security
userCountIndicator: SingleUser

```

#### Ownership transfer

```
activityCategory: AssetTransfer
activityDescription: Finalized transfer of ownership of tokenized securities
between parties, updating authoritative ownership state.
estimatedNotionalRange: Variable
assetClass: Security
userCountIndicator: MultipleUsersDistinctParties
```

#### Settlement outcome recording (FoP / DvP)

```
activityCategory: DvPSettlement
activityDescription: Recording of finalized outcome of a coordinated Free-of-
Payment (FoP) or Delivery-versus-Payment (DvP) settlement workflow.
estimatedNotionalRange: Variable
assetClass: Security
userCountIndicator: MultipleUsersDistinctParties
Notes: Marker is emitted only after settlement completion is confirmed and
ownership transitions are finalized on-ledger.
```

#### Usage constraint application or release

```
activityCategory: RegistryUpdate
activityDescription: Application or release of a protocol-enforced usage or
exclusivity constraint on tokenized ownership units to prevent conflicting reuse
while referenced by external financial arrangements.
estimatedNotionalRange: Variable
assetClass: Security
userCountIndicator: SingleUser
```

---

### 5.2 Marker emission policy (app-specific)

Onchain Transfer Agent emits activity markers in a manner intended to reflect the
relative economic significance of finalized on-ledger actions, while respecting
network throughput constraints and governance guidance.

Marker emission follows these principles:
- **Proportionality:** Marker counts scale with the economic magnitude of the
  underlying finalized action.
- **Granularity:** Markers are emitted per finalized transaction and are not
  aggregated across unrelated actions.
- **Minimum emission:** At least one marker is emitted for each eligible finalized
  action.
- **Rate limiting:** Marker emission is rate-limited to prevent network flooding
  and to preserve incentive integrity.

Specific emission parameters may evolve over time in accordance with Canton
Network governance processes.


---

### 5.3 Non-emitting activities

The following actions performed by Onchain Transfer Agent do **not** generate
Featured App Activity Markers:

- application setup and configuration
- account or identity registration
- preparatory or validation steps prior to finalization
- failed, rejected, or reverted transactions
- administrative updates that do not affect ownership or usage rights
- off-ledger coordination or communication processes

Only finalized, on-ledger state transitions that create, transfer, or condition
enforceable economic rights are eligible for activity marker emission.

---

### 5.4 CIP-0098 alignment and incentive integrity

Onchain Transfer Agent’s activity marker design aligns with the principles
articulated in **CIP-0098**, including incentive integrity, interpretability, and
resistance to synthetic or non-economic activity.

In particular:
- Marker eligibility is narrowly scoped to economically meaningful outcomes,
  ensuring incentives track real ownership state changes.
- Administrative, preparatory, off-ledger, or service-oriented actions are
  intentionally excluded from incentive consideration.
- Marker volume serves as a descriptive signal of activity magnitude rather than
  an objective in itself.
- Emission behavior is rate-limited and subject to Canton Network governance
  guidance.

This design ensures that activity markers remain interpretable, auditable, and
aligned with real economic outcomes on Canton Network.


---

## 6. Dependencies and integrations

Onchain Transfer Agent relies on the following components and integrations to
perform its on-ledger functions:

- Canton Network validator infrastructure
- Tokenized ownership templates, aligned with CIP-0056
- Issuer and stakeholder access control systems
- External execution or settlement applications for coordinated FoP or DvP
  workflows, where applicable

These dependencies are referenced for context only and do not imply control or
operation of external systems by the application.


---

## 7. Security and abuse-mitigation (descriptive)

Onchain Transfer Agent is designed to reduce the risk of synthetic or non-economic
activity through the following characteristics:

- **Ledger anchoring:** Activity markers are emitted only for finalized Canton
  ledger transactions that create, transfer, or condition enforceable economic
  rights.
- **Authoritative state:** OTA maintains authoritative ownership state, preventing
  duplicate or conflicting updates.
- **Usage constraints:** Protocol-enforced exclusivity constraints prevent the
  same ownership units from being referenced or reused in conflicting arrangements.
- **Rate-limited emission:** Activity marker emission is rate-limited to reduce
  the risk of excessive or abusive marker generation.

These safeguards are implemented and enforced at the application level and do not
imply automated enforcement by Canton Network itself.


---

## 8. Changelog

- 2026-01-03 - Initial internal draft outlining Transfer Agent–scoped application
  behavior and on-ledger ownership finalization.
- 2026-01-07 - Refined activity marker mapping to align with ledger-final economic
  state transitions and non-emitting administrative actions.
- 2026-01-11 - Added usage constraint and exclusivity handling to prevent
  conflicting reuse of tokenized ownership units.
- 2026-01-13 - Clarified conditional settlement outcome recording for coordinated
  FoP and DvP workflows.
- 2026-01-16 - Updated naming to 'OTA' for Onchain Transfer Agent.
- 2026-01-19 - Added application-controlled PartyId.


---
*This document is maintained in the `canton-featured-apps` repository and is
intended to serve as a canonical reference for the declared Featured App.*
