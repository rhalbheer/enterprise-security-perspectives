# European Digital Sovereignty In Practice

*Roger Halbheer, Chief Security Advisor*

A customer‑facing framework for CISOs regarding sovereignty with scenarios mapped to the Cloud Sovereignty Framework and Microsoft‑centric controls.

*This document was written with the help of Copilot.*

---

## Abstract

European customers increasingly ask for "sovereignty," but the term is ambiguous and often conflates data residency, legal jurisdiction, operational control, supply-chain dependency, and — more recently — strategic continuity under geopolitical pressure (e.g., sanctions or forced service suspension).

This paper provides:

- a taxonomy aligned to the European Commission's [Cloud Sovereignty Framework](https://digital-strategy.ec.europa.eu/en/library/cloud-sovereignty-framework) (CSF),
- a reduced set of six practical scenarios mapped to those objectives,
- countermeasures across people/process/technology/legal (using Microsoft examples where possible),
- tradeoffs to avoid "sovereignty theatre"

---

## Why this matters now (and what "sovereignty" usually means)

In Europe, "sovereignty" is rarely a single requirement. Customers typically mean some combination of:

- **Control over data and AI** (where data is stored/processed; who can access it; key custody; auditability).
- **Jurisdictional resilience** (exposure to non‑EU laws with cross‑border reach; enforceability of European rights).
- **Strategic continuity** (the "kill switch" fear: could a provider be forced to suspend services due to sanctions/export controls or geopolitical pressure).

The European Commission Cloud Sovereignty Framework makes this explicit by defining eight sovereignty objectives (SOV‑1..SOV‑8) and graded assurance levels (SEAL‑0..SEAL‑4), rather than treating sovereignty as binary.

---

## Sovereignty taxonomy — aligned to the EU Cloud Sovereignty Framework

The Cloud Sovereignty Framework defines the following objectives and the factors that contribute to each, including legal exposure, operational oversight, key control, auditability, supply-chain provenance, and sustainability.

| Objective | Description |
|-----------|-------------|
| **SOV‑1** (Strategic Sovereignty) | Are services anchored in the EU ecosystem — and can operations continue if asked to cease/suspend service or if support is disrupted? |
| **SOV‑2** (Legal & Jurisdictional Sovereignty) | Which laws can compel actions, and to what extent is the service insulated from external legal claims? |
| **SOV‑3** (Data & AI Sovereignty) | Where is data processed, who has effective control over cryptographic access, and how is AI usage/access audited? |
| **SOV‑4** (Operational Sovereignty) | Can EU actors operate/support/evolve the service without foreign dependency; how portable is it? |
| **SOV‑5** (Supply Chain Sovereignty) | What non‑EU dependencies exist in hardware, firmware, code, and delivery chain; what transparency/audit rights exist? |
| **SOV‑6** (Technology Sovereignty) | Is the stack open/interoperable/auditable; can customers avoid irreversible lock‑in and evolve independently? |
| **SOV‑7** (Security & Compliance Sovereignty) | Can security operations and compliance be evidenced under EU-aligned control expectations (e.g., NIS2/DORA)? |
| **SOV‑8** (Environmental Sustainability) | Does long-term autonomy/resilience depend on energy/resource constraints, and is sustainability measurable? |

### SEAL levels (assurance)

The Cloud Sovereignty Framework uses graded Sovereignty Assurance Levels (SEAL0..SEAL4) to express how strongly a service meets an objective — moving from no specific sovereignty assurances to independently evidenced, highest-rigor controls:

| Level | Description |
|-------|-------------|
| **SEAL0** | Not assessed / no explicit Cloud Sovereignty Framework sovereignty assurances claimed. |
| **SEAL1** | Baseline controls and statements of conformity; limited evidence. |
| **SEAL2** | Defined controls implemented and documented; more structured evidence. |
| **SEAL3** | High assurance — controls are comprehensive and consistently operated; strong evidence and auditability. |
| **SEAL4** | Highest assurance — most stringent requirements with robust, independent verification and continuous assurance signals where applicable. |

### Implementation consequences

In customer discussions, sovereignty is often framed as a binary choice. It is critical to move away from this mindset and treat sovereignty as part of standard risk management. The appropriate approach is to assess requirements through a structured matrix that reflects different needs across services, rather than applying a one-size-fits-all answer.

In practice, for each service or workload, you typically end up with a matrix like this:

**Assurance Level needed for service x:**

|  | SEAL-0 | SEAL-1 | SEAL-2 | SEAL-3 | SEAL-4 |
|--|--------|--------|--------|--------|--------|
| SOV‑1 (Strategic Sovereignty) |  |  |  |  |  |
| SOV‑2 (Legal & Jurisdictional Sovereignty) |  |  |  |  |  |
| SOV‑3 (Data & AI Sovereignty) |  |  |  |  |  |
| SOV‑4 (Operational Sovereignty) |  |  |  |  |  |
| SOV‑5 (Supply Chain Sovereignty) |  |  |  |  |  |
| SOV‑6 (Technology Sovereignty) |  |  |  |  |  |
| SOV‑7 (Security & Compliance Sovereignty) |  |  |  |  |  |
| SOV‑8 (Environmental Sustainability) |  |  |  |  |  |

These choices affect architecture, operations, and cost — and should be weighed accordingly.

---

## Key Scenarios mapped to sovereignty objectives

Below are six scenarios that cover the majority of customer "sovereignty" conversations and map cleanly to the Cloud Sovereignty Framework objectives:

**Legend:** ● Primary | ○ Secondary

| Scenario | SOV‑1 | SOV‑2 | SOV‑3 | SOV‑4 | SOV‑5 | SOV‑6 | SOV‑7 | SOV‑8 |
|----------|-------|-------|-------|-------|-------|-------|-------|-------|
| S1 — Sanctions / service suspension / geopolitical "kill switch" | ● | ○ |  | ● | ○ | ○ | ○ |  |
| S2 — Extraterritorial laws / legal conflict / compelled actions | ○ | ● | ○ | ○ |  |  | ○ |  |
| S3 — EU/EFTA data residency & processing (incl. support data) |  | ○ | ● |  |  |  | ○ |  |
| S4 — Privileged access & operational transparency (support access) |  |  | ○ | ● |  |  | ● |  |
| S5 — Key sovereignty ("provider can't decrypt") & confidential processing |  | ○ | ● | ○ |  | ● | ○ |  |
| S6 — Supply chain + sustainability resilience (long‑term autonomy) | ○ |  |  | ○ | ● | ○ | ○ | ● |

---

## Scenario playbooks

### Scenario S1 — Sanctions / service suspension / geopolitical "kill switch"

**Mapped**
- Primary: SOV‑1 (Strategic Sovereignty), SOV‑4 (Operational Sovereignty)
- Secondary: SOV‑2 (Legal & Jurisdictional Sovereignty), SOV‑5 (Supply Chain Sovereignty), SOV‑6 (Technology Sovereignty), SOV‑7 (Security & Compliance Sovereignty)

**Description**

Customers fear a foreign administration could pressure a provider via sanctions/export controls or restrictions on service provision, resulting in suspension of digital services. The Cloud Sovereignty Framework explicitly calls out the need to sustain operations against requests to cease/suspend service or disrupted vendor support.

Sanctions practice can include restrictions on providing "cloud‑based services" and SaaS categories for certain destinations, demonstrating that service delivery can be targeted as a policy instrument.

**Risk**

- *Likelihood:* Low overall but higher perceived concern for public sector/critical operators; service‑restriction instruments exist.
- *Impact:* Severe for "must‑run" services (public services, critical infrastructure) because this is an availability/continuity failure mode.

**Countermeasures**

- *People:* Assign a cross‑functional owner (CISO + Legal + Risk) for "geopolitical/service‑continuity risk" and maintain board visibility for critical services.
- *Process:* Implement and test exit plans (data export, identity, app portability, runbooks) and define a "minimum viable operations" baseline for crisis continuity.
- *Technology (Microsoft examples):*
  - For most workloads: use Sovereign Public Cloud controls and architect for portability (reduce single‑point dependency while retaining hyperscale benefits).
  - For "must‑run" workloads: use Sovereign Private Cloud (customer‑operated) combining Azure Local + Microsoft 365 Local.

**Downside / tradeoff**

Private/local sovereign environments significantly reduce benefits of hyperscale cloud (cost efficiency, agility, innovation speed), which Microsoft's own sovereignty guidance acknowledges as a tradeoff between control and cloud value.

Sovereign Private Clouds typically increase operational cost and can significantly reduce functionality.

---

### Scenario S2 — Extraterritorial laws / legal conflict / compelled actions

**Mapped**
- Primary: SOV‑2 (Legal & Jurisdictional Sovereignty)
- Secondary: SOV‑1 (Strategic Sovereignty), SOV‑3 (Data & AI Sovereignty), SOV‑4 (Operational Sovereignty), SOV‑7 (Security & Compliance Sovereignty)

**Description**

Customers worry that non‑EU laws with cross‑border reach can compel actions or create legal uncertainty even if services run in Europe — exactly what SOV‑2 (Legal & Jurisdictional Sovereignty) evaluates.

The EU's [Blocking Statute](https://finance.ec.europa.eu/economic-and-fiscal-policy-coordination/international-economic-relations/blocking-statute_en) exists to protect EU operators from the extraterritorial application of certain third‑country laws and sets mechanisms including non‑recognition of certain foreign judgments, damage recovery, and restrictions on compliance (with a derogation mechanism).

**Risk**

- *Likelihood:* Low to Medium depending on sector, footprint, and exposure; EU guidance emphasizes mapping transfers and assessing protections.
- *Impact:* High to Severe for public sector and regulated industries due to enforceability and trust consequences.

**Countermeasures**

- *People/Process:* Maintain "know your transfers" discipline and a documented approach to risk assessment and supplementary measures. The International Association of Privacy Professionals (IAPP) provides [published guidance on performing Transfer Impact Assessments](https://iapp.org/resources/article/transfer-impact-assessment-templates/).
- *Technology:* Minimize cross‑border processing and strengthen cryptographic and operational controls (ties directly to S3, S4, S5).
- *Legal:* Understand Blocking Statute obligations and derogation path; treat this as a governance tool — not a guaranteed technical control.

**Downside / tradeoff**

Legal and process overhead is ongoing: maintaining transfer maps, running Transfer Impact Assessments, updating contracts and supplementary measures, and managing Blocking Statute obligations/derogations can add continuous governance work. In practice, this often lengthens procurement cycles and slows change management, because legal review and evidence collection must keep pace with new services, features, vendors, and cross-border support scenarios — especially in regulated sectors.

---

### Scenario S3 — EU/EFTA data residency & processing (incl. support data)

**Mapped**
- Primary: SOV‑3 (Data & AI Sovereignty)
- Secondary: SOV‑2 (Legal & Jurisdictional Sovereignty), SOV‑7 (Security & Compliance Sovereignty)

**Description**

Customers require that customer content and related processing stay within EU/EFTA boundaries — not only for primary storage, but also for compute, backups, and the operational data created during service delivery (e.g., support artifacts, logs, diagnostic traces, and engineering access workflows). This scenario typically appears in regulated sectors and public procurement where "residency" is defined as an end-to-end constraint across the service lifecycle, including incident response and vendor support.

The practical nuance: residency commitments are only meaningful if the customer can evidence where data is processed and how exceptions (break/fix support, remote operations, cross-border escalation) are prevented, approved, or transparently governed.

**Risk**

- *Likelihood:* Low to Medium depending on service selection and configuration; Microsoft notes some Azure services may require customer action for certain commitments.
- *Impact:* High due to regulatory exposure and reputational impact.

**Countermeasures**

- *People:* Assign data residency accountability; require residency verification in architecture and procurement.
- *Process:* Maintain data flow maps and evidence packs for audits and tenders.
- *Technology (Microsoft examples):*
  - Use [EU Data Boundary](https://www.microsoft.com/en-us/trust-center/privacy/european-data-boundary-eudb) baseline for eligible services.
  - Use [Advanced Data Residency](https://learn.microsoft.com/en-us/microsoft-365/enterprise/advanced-data-residency) (ADR) where country-level commitments are required and eligible.

**Downside / tradeoff**

EU Data Boundary configurations and (where needed) Advanced Data Residency can add both cost and delivery friction: eligibility checks and tenant migrations, tighter constraints on where workloads and support processes may run, and additional operational discipline to keep new features, integrations, and incident workflows inside the agreed boundary. The supporting countermeasures (data-flow mapping, evidence packs, and residency verification in architecture/procurement) also create ongoing governance overhead, and overly strict residency choices can reduce service options or delay adoption without materially reducing risk for non-critical workloads.

---

### Scenario S4 — Privileged access & operational transparency (support access)

**Mapped**
- Primary: SOV‑4 (Operational Sovereignty), SOV‑7 (Security & Compliance Sovereignty)
- Secondary: SOV‑3 (Data & AI Sovereignty)

**Description**

Customers want assurance that provider engineers cannot access customer content without explicit customer approval, and that any access is time-bound, least-privilege, and fully auditable. This includes clear separation between routine service operations and exceptional break/fix scenarios, with transparent logging of who accessed what, when, and why, so the customer can evidence control to regulators and internal audit.

**Risk**

- *Likelihood:* Medium — support scenarios occur; some require content access workflows.
- *Impact:* High — content exposure, audit gaps, compliance issues.

**Countermeasures**

- *People:* Minimize privileged roles; define 24/7 approver coverage if Lockbox is enabled.
- *Process:* Approval workflows + periodic review of access logs and requests.
- *Technology (Microsoft examples):*
  - [Microsoft Purview Customer Lockbox](https://learn.microsoft.com/en-us/microsoft-365/compliance/customer-lockbox-requests) requires explicit customer approval before Microsoft can access content for service operations in supported services.
  - [Microsoft Data Guardian](https://learn.microsoft.com/en-us/azure/security/fundamentals/data-guardian-overview) (Sovereign Public Cloud capability) adds EU‑resident approval/monitoring for remote access and logs sessions in a tamper‑evident ledger.

**Downside / tradeoff**

Support can slow if the countermeasures are not operationalized: Customer Lockbox/Data Guardian introduce an explicit approval step, and if 24/7 approver coverage, escalation paths, and runbooks are not in place, break/fix activities can queue while teams wait for authorization. Minimizing privileged roles and performing periodic review of access requests/logs improves control and auditability, but adds process overhead and coordination, particularly during incidents when speed matters.

---

### Scenario S5 — Key sovereignty ("provider can't decrypt") & confidential processing

**Mapped**
- Primary: SOV‑3 (Data & AI Sovereignty), SOV‑6 (Technology Sovereignty)
- Secondary: SOV‑2 (Legal & Jurisdictional Sovereignty), SOV‑4 (Operational Sovereignty), SOV‑7 (Security & Compliance Sovereignty)

**Description**

Customers ask for key sovereignty because control of the encryption keys is control of the data: if the provider does not hold the keys, it cannot technically decrypt customer content — even if its platform, administrators, or supply chain are compromised — and it is materially harder to comply with compelled access requests, since the provider cannot disclose plaintext it cannot produce.

**Risk**

- *Likelihood:* Medium because stronger key custody increases operational complexity and the chance of key lifecycle mistakes.
- *Impact:* High–Severe (data loss if keys are lost; exposure if misconfigured).

**Countermeasures**

- *People:* Segregation of duties (key admins ≠ data admins).
- *Process:* Rotation, escrow/break-glass, recovery testing.
- *Technology (Microsoft examples):*
  - [Customer-Managed Keys](https://learn.microsoft.com/en-us/azure/security/fundamentals/customer-managed-keys) (CMK): customer controls the encryption keys, so the provider can't decrypt customer data without customer authorization.
  - [Double Key Encryption](https://learn.microsoft.com/en-us/microsoft-365/compliance/double-key-encryption) (DKE): data is protected by two keys (provider + customer), so the provider can't decrypt it without customer participation.
  - [External Key Management](https://learn.microsoft.com/en-us/azure/security/fundamentals/external-key-management) (Sovereign Public Cloud): customer-held keys outside the provider, so the provider can't decrypt customer data without customer authorization.
  - [Azure Confidential Computing](https://learn.microsoft.com/en-us/azure/confidential-computing/overview): protects data in use by running workloads in hardware-isolated trusted environments, reducing exposure even to privileged infrastructure access.

**Downside / tradeoff**

Strong key sovereignty (CMK/DKE/EKM) adds a hard operational dependency between the cloud service and your external key environment (often on‑prem), so outages or misconfiguration in key operations can directly impact availability.

It can also reduce cloud-native features that require server-side content processing, e.g., limited web viewing for DKE‑protected content and constraints on capabilities like AI usage, search, malware scanning, and some DLP-style workflows depending on configuration.

---

### Scenario S6 — Supply chain + sustainability resilience (long‑term autonomy)

**Mapped**
- Primary: SOV‑5 (Supply Chain Sovereignty), SOV‑8 (Environmental Sustainability)
- Secondary: SOV‑1 (Strategic Sovereignty), SOV‑4 (Operational Sovereignty), SOV‑6 (Technology Sovereignty), SOV‑7 (Security & Compliance Sovereignty)

**Description**

The Cloud Sovereignty Framework evaluates supply-chain sovereignty through the origin and transparency of critical components, and sustainability through long-term resilience to energy and resource constraints. In practice, the countermeasures (supplier mapping, contractual transparency, and substitution/portability plans) improve visibility and contingency options, but the "twist" is market reality: for key technologies (chips, firmware supply chains, hyperscale platforms, and energy-dense datacenter infrastructure) supplier diversity is limited, capacity is concentrated, and switching is slow and costly if even possible.

This means many organizations can realistically reduce dependency risk only for a narrow set of truly critical workloads — while for the majority of services, resilience comes more from multi-region design, tested exit/portability runbooks, and procurement leverage than from achieving full "EU-only" sourcing end-to-end.

**Risk**

- *Likelihood:* Medium (supply and energy disruptions are recurring; effect varies by sector).
- *Impact:* High for critical services dependent on specialized hardware or constrained locations.

**Countermeasures**

- *People/Process:* Map key suppliers; require contractual transparency; define substitution and exit plans; and keep procurement evidence aligned to SOV‑5 and SOV‑8.
- *Technology:* Use portability and resilience patterns (multi-region design, tested recovery, documented exit runbooks). Only for exceptional cases, consider local operating models to reduce dependence on specific external supply chains.

**Downside / tradeoff**

The countermeasures can look tidy on paper but become costly "paperwork sovereignty" if applied broadly: deep supplier mapping and transparency demands slow procurement (and often meet vendor pushback), while exit/substitution plans are rarely realistic or exercised enough to be credible. Portability patterns help, but they still add engineering and operating cost — and in a concentrated market, switching is slow and uncertain. Local operating models can reduce specific dependencies, but typically reintroduce platform cost, staffing burden, and innovation drag; in practice, reserve the strictest measures for truly critical services and treat full supply-chain sovereignty as an aspiration, not a default baseline.

---

## What makes sense (and what doesn't) — the evaluation

### What usually makes sense for most customers (Tier 1–2 workloads)

- Treat sovereignty as an enterprise risk and manage it through standard risk management practices; it is not binary.
- Target SEAL‑2/SEAL‑3 outcomes for the sovereignty objectives that matter most (often SOV‑2, SOV‑3, SOV‑4, SOV‑7) rather than "full sovereignty everywhere," consistent with the Cloud Sovereignty Framework's graded approach.
- Use EU Data Boundary as baseline and Advanced Data Residency only where country-level commitments are necessary and eligible.
- Implement Customer Lockbox and/or Data Guardian when operational access transparency is required.
- Use Customer‑Managed Keys broadly; reserve Double Key Encryption/External Key Management for a narrow, truly critical data class because key sovereignty increases operational complexity and impacts usability.

### What only makes sense for exceptional cases (Tier 3 must‑run)

- Use Sovereign Private Cloud (Azure Local + Microsoft 365 Local) when business continuity requirements outweigh the loss of some hyperscale cloud benefits and the loss of functionality — because SOV‑1 (Strategic Sovereignty) explicitly includes resilience against service suspension and disrupted support.

### What usually does not make sense ("sovereignty theatre")

- "Residency-only" without operational access governance and key strategy fails to address SOV‑3 (Data & AI Sovereignty) and SOV‑4 (Operational Sovereignty) realities (control over access, keys, and operational oversight).
- Declaring every workload "must‑run" and forcing private sovereign everywhere increases cost and reduces innovation speed without proportional risk reduction — Microsoft's own framing highlights trade‑offs between private environments and hyperscale benefits.

---

## Microsoft-centric control palette

Use this as a "menu" of controls in workshops and procurement. Each item includes what it does and where it typically fits.

### Data residency & processing controls

- **EU Data Boundary (Microsoft Cloud):** Baseline commitment for eligible core services to store and process customer data (and pseudonymized personal data) within EU/EFTA, and to keep professional services data from support interactions in EU/EFTA for core services.
- **Advanced Data Residency (ADR) for Microsoft 365:** Optional add‑on for country-level residency commitments (where eligible) and expanded service coverage beyond baseline commitments.

### Operational access control & transparency

- **Microsoft Purview Customer Lockbox:** Ensures Microsoft can't access your content for service operations without explicit customer approval (for supported services), improving transparency and control.
- **Data Guardian (Sovereign Public Cloud):** Adds EU‑resident oversight of remote access by Microsoft personnel with approval + monitoring and logs sessions to a tamper‑evident ledger, strengthening operational sovereignty.

### Encryption & key sovereignty

- **Customer‑Managed Keys (CMK) with Azure Key Vault / Managed HSM:** Lets customers control encryption keys for many Azure services (broad coverage varies by service) to support separation of duties and stronger key custody.
- **Double Key Encryption (DKE) for Microsoft 365:** For highly sensitive data, requires two keys to decrypt: one customer‑controlled via a customer‑operated DKE service and one in Azure; supports "provider can't decrypt without customer participation" posture for protected content.
- **External Key Management (Sovereign Public Cloud capability):** Designed to enable customer control of encryption keys outside Microsoft's cloud boundary (e.g., customer/trusted third‑party HSMs) while still using Azure services — used where regulations demand stronger separation of key custody.

### Confidential Computing (data in use protection)

- **Azure Confidential Computing (Confidential VMs / containers; TEEs):** Protects data in use by running computations inside hardware-based Trusted Execution Environments (TEEs), complementing encryption at rest/in transit and reducing the risk associated with operational access during processing.
- **Secure key release via attestation (pattern):** Enables releasing keys only after the workload proves (via attestation) it is executing inside a TEE, strengthening end‑to‑end control for sensitive workloads.

### Sovereign configuration & governance at scale

- **Regulated Environment Management (REM):** Provides a unified experience to configure, deploy, and monitor workloads for sovereign operations, working with policy‑as‑code guardrails and surfacing sovereignty signals (e.g., key usage/access oversight) for ongoing assurance.

### Deployment models for maximum autonomy

- **Sovereign Public Cloud (Microsoft Sovereign Cloud):** Applies sovereign controls across European datacenter regions for services such as Azure/M365/Security/Power Platform, combining residency + operational oversight + encryption options without requiring migrations for EU workloads in-region.
- **Sovereign Private Cloud (Azure Local + Microsoft 365 Local):** Customer‑operated environment for extraordinary sovereignty needs (air‑gapped / disconnected / "must‑run"), enabling operation with full infrastructure control where public cloud dependency is unacceptable.
- **National Partner Clouds (where available):** Local partner‑operated sovereign implementations designed to meet country‑specific frameworks (availability and scope vary by geography).

### Regulatory alignment (governance & assurance)

- **NIS2 alignment:** Use NIS2 risk‑management and reporting requirements as a governance baseline across critical sectors (board accountability, supply chain security, incident reporting).
- **DORA alignment (financial services):** Use DORA for ICT risk management and ICT third‑party risk management: contracts, auditability, resilience testing, and oversight for critical providers.

---

## References

1. [Cloud Sovereignty Framework](https://digital-strategy.ec.europa.eu/en/library/cloud-sovereignty-framework)
2. [Extraterritoriality (Blocking Statute) — Finance — European Commission](https://finance.ec.europa.eu/economic-and-fiscal-policy-coordination/international-economic-relations/blocking-statute_en)
3. [Transfer Impact Assessment Templates | IAPP](https://iapp.org/resources/article/transfer-impact-assessment-templates/)
4. [Microsoft EU Data Boundary Overview | Microsoft Trust Center](https://www.microsoft.com/en-us/trust-center/privacy/european-data-boundary-eudb)
5. [Advanced data residency in Microsoft 365 | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/enterprise/advanced-data-residency)
6. [Customer Lockbox requests | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/compliance/customer-lockbox-requests)
7. [Data Guardian overview — Microsoft Sovereign Cloud | Microsoft Learn](https://learn.microsoft.com/en-us/azure/security/fundamentals/data-guardian-overview)
8. [Services that support customer managed keys (CMKs) in Azure Key Vault and Azure Managed HSM | Microsoft Learn](https://learn.microsoft.com/en-us/azure/security/fundamentals/customer-managed-keys)
9. [Double Key Encryption (DKE) | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/compliance/double-key-encryption)
10. [External Key Management overview — Microsoft Sovereign Cloud | Microsoft Learn](https://learn.microsoft.com/en-us/azure/security/fundamentals/external-key-management)
11. [Azure Confidential Computing Overview | Microsoft Learn](https://learn.microsoft.com/en-us/azure/confidential-computing/overview)
