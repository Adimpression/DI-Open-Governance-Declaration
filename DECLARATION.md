# DI Open Governance Declaration

**Profile-Based Draft Specification**
**Status:** Draft
**Audience:** Builders, operators, auditors, publishers, adopters, institutions, and regulators

---

## Abstract

This document defines a profile-based conformance model for open Deterministic Intelligence.

It separates governance into three profiles:

* **Core** — the minimum structure required for a system to be governable
* **Extended** — the additional structure required for mature ecosystem and institutional use
* **Deterministic** — the additional structure required for bounded, replayable, formally reviewable execution

This structure allows granular adoption and precise public claims.

A system does not need to implement everything at once.
It may declare conformance by profile and subsection.

---

## 1. Purpose

The purpose of this declaration is to make open DI:

* governable
* adoptable
* inspectable
* enforceable
* reviewable
* revocable
* incrementally conformable

This declaration is designed so that the ecosystem can say, with precision:

* we conform to **Core.SkillDecl**
* we conform to **Extended.Approval**
* we conform to **Deterministic.Replay**

instead of making vague claims such as “we are governed” or “we are deterministic.”

---

## 2. Conformance Model

The declaration is divided into three profiles.

```text
DI Open Governance
|
+-- Core
|
+-- Extended
|
+-- Deterministic
```

Each profile contains named subsections.

Conformance is declared at the subsection level.

---

## 3. Definitions

### 3.1 Core

The minimum constitutional substrate required for governable DI.

### 3.2 Extended

Additional governance required for institutional, ecosystem, and multi-party maturity.

### 3.3 Deterministic

Additional governance required for replayable, bounded, reviewable execution under deterministic constraints.

### 3.4 Skill

An installable, governed unit of behavior that extends the core.

### 3.5 Policy

A machine-interpretable rule set governing admission, activation, invocation, composition, data access, side effects, and approval.

### 3.6 Authority

Any granted power to read, write, execute, communicate, persist, invoke, approve, modify, export, or affect the outside world.

### 3.7 Trace

A structured record of request, policy, approvals, execution, composition path, and effects.

### 3.8 Replay

The ability to reconstruct and re-evaluate a past execution from preserved artifacts and preserved context.

### 3.9 Conformance Claim

A precise declaration that a system implements a named profile subsection.

---

## 4. Constitutional Rule

All DI governance in this declaration follows this chain:

```text
SKILL
  |
  v
DECLARATION
  |
  v
GOVERNANCE
  |
  v
ENFORCEMENT
  |
  v
TRACE
  |
  v
REVIEW
  |
  v
REVOCATION / CORRECTION
  |
  v
FUTURE TRUST
```

And because the system is living, not static, the actual constitutional form is a loop:

```text
+-------------------+
|   FUTURE TRUST    |
+---------+---------+
          |
          v
+---------+---------+
|      SKILL        |
+---------+---------+
          |
          v
+---------+---------+
|   DECLARATION     |
+---------+---------+
          |
          v
+---------+---------+
|   GOVERNANCE      |
+---------+---------+
          |
          v
+---------+---------+
|   ENFORCEMENT     |
+---------+---------+
          |
          v
+---------+---------+
|      TRACE        |
+---------+---------+
          |
          v
+---------+---------+
|      REVIEW       |
+---------+---------+
          |
          v
+---------+---------+
| REVOCATION /      |
| CORRECTION        |
+-------------------+
```

If this loop is broken, governance becomes symbolic rather than real.

---

# 5. Core Profile

## 5.1 Purpose of Core

The Core profile defines the minimum structure required for a DI system to be governable at all.

A system that lacks Core should not claim governed DI.

### Core profile map

```text
Core
|
+-- Core.ID
+-- Core.SkillDecl
+-- Core.Authority
+-- Core.Policy
+-- Core.Enforcement
+-- Core.Trace
+-- Core.Review
```

---

## 5.2 Core.ID

### Meaning

Every governed entity must be distinguishable and attributable.

### Requirement

A conforming system SHALL identify, at minimum:

* skills
* policies
* operators
* approvals
* traces

### Purpose

Without identity, no accountability chain can exist.

---

## 5.3 Core.SkillDecl

### Meaning

Every skill must declare itself before trust.

### Requirement

A conforming system SHALL require every skill to declare, at minimum:

* identity
* intent
* requested authority
* inputs
* outputs
* side effects
* data classes touched
* invocation rights
* composition rights
* escalation rights
* approval requirements
* risk tier

### Canonical model

```text
+--------------------------------------------------+
|                    SKILL                         |
+--------------------------------------------------+
| Identity                                         |
| Intent                                           |
| Inputs                                           |
| Outputs                                          |
| Requested Authority                              |
| Data Classes                                     |
| Side Effects                                     |
| Invocation Rights                                |
| Composition Rights                               |
| Escalation Rights                                |
| Approval Requirements                            |
| Risk Tier                                        |
+--------------------------------------------------+
```

A skill that cannot declare these properties is not governable.

---

## 5.4 Core.Authority

### Meaning

Authority must be explicit, bounded, and deny-by-default.

### Requirement

A conforming system SHALL distinguish authority at least across:

* read
* write
* execute
* communicate
* persist
* invoke
* approve
* modify
* export
* escalate

Each grant SHALL also define its bounds:

* scope
* target
* context
* duration
* conditions
* approval class

### Evaluation model

```text
REQUESTED ACTION
      |
      v
DECLARED BY SKILL?
   |        |
  no       yes
   |        |
 DENY       v
       ALLOWED BY POLICY?
          |        |
         no       yes
          |        |
        DENY       v
             NEEDS APPROVAL?
                |        |
               yes      no
                |        |
                v        v
            APPROVED?   ENFORCE
             |    |        |
            no   yes       v
             |    |      TRACE
            HOLD  v
                ENFORCE
                   |
                   v
                 TRACE
```

---

## 5.5 Core.Policy

### Meaning

No trust or action exists outside policy.

### Requirement

A conforming system SHALL apply policy before:

* admission
* activation
* invocation
* material effect

### Purpose

Policy is the governing authority of the runtime.

---

## 5.6 Core.Enforcement

### Meaning

Declared rules must be enforced, not merely documented.

### Requirement

A conforming system SHALL mediate material action through runtime enforcement.

### Runtime model

```text
+-------+      +-----------+      +--------+
| SKILL |----->| MEDIATOR  |----->| EFFECT |
+---+---+      +-----+-----+      +---+----+
    ^                |                |
    |                v                v
    |             POLICY            TRACE
    +---------------------------------+
```

A skill shall not directly convert existence into effect.

---

## 5.7 Core.Trace

### Meaning

Every material action must produce evidence.

### Requirement

A conforming system SHALL emit a structured trace for every material action.

A trace MUST answer:

* who initiated
* what was requested
* which skill acted
* what policy applied
* what authority was requested
* what authority was granted
* what approvals occurred
* what data classes were touched
* what side effects occurred
* what result was produced

---

## 5.8 Core.Review

### Meaning

Trace must lead to reviewable accountability.

### Requirement

A conforming system SHALL provide a review path for material traces and decisions.

### Core loop

```text
SKILL
  |
  v
DECLARATION
  |
  v
POLICY
  |
  v
ENFORCEMENT
  |
  v
TRACE
  |
  v
REVIEW
```

---

# 6. Extended Profile

## 6.1 Purpose of Extended

The Extended profile defines what is needed for institutional, ecosystem, and multi-party maturity.

A system may conform to Core without Extended.
A serious public or organizational ecosystem will usually require much of Extended.

### Extended profile map

```text
Extended
|
+-- Extended.Admission
+-- Extended.Composition
+-- Extended.Data
+-- Extended.Approval
+-- Extended.Risk
+-- Extended.Registry
+-- Extended.Incident
+-- Extended.HumanRoles
```

---

## 6.2 Extended.Admission

### Meaning

Publication, installation, activation, and invocation are distinct governed stages.

### Requirement

A conforming system SHALL distinguish, at minimum:

* publish
* review
* admit
* install
* activate
* invoke

### Admission flow

```text
PUBLISH
   |
   v
REVIEW
   |
   +----> REJECT
   |
   v
ADMIT
   |
   +----> QUARANTINE
   |
   v
INSTALL
   |
   +----> HOLD
   |
   v
ACTIVATE
   |
   v
INVOKE
```

---

## 6.3 Extended.Composition

### Meaning

Skill combinations must be governed as wholes, not merely as parts.

### Requirement

A conforming system SHALL evaluate:

* invocation chains
* delegation depth
* cycles
* authority unions
* emergent side effects
* hidden transitive behavior

### Composition model

```text
          +---------+       invokes       +---------+
          | SKILL A |-------------------->| SKILL B |
          +----+----+                     +----+----+
               ^                               |
               |                               |
               |                               v
               |                         +-----+----+
               |                         | SKILL C  |
               |                         +-----+----+
               |                               |
               +----------- feedback ----------+
```

The system must ask:

* is each skill allowed alone?
* is the chain allowed as a whole?
* does the chain create new authority?
* does the loop create persistence, escalation, or drift?

---

## 6.4 Extended.Data

### Meaning

Skills must be bound to data classes.

### Requirement

A conforming system SHALL classify data and bind skills to permitted classes.

A skill SHALL declare:

* which data classes it may access
* for what purpose
* under what conditions
* for how long
* whether persistence is allowed
* whether export is allowed

### Data flow

```text
DATA REQUEST
    |
    v
DATA CLASS IDENTIFIED
    |
    v
SKILL DECLARATION CHECK
    |
    v
POLICY CHECK
    |
    v
APPROVAL CHECK IF REQUIRED
    |
    v
ALLOW OR DENY
    |
    v
TRACE
```

---

## 6.5 Extended.Approval

### Meaning

Some actions require explicit authorization beyond policy.

### Requirement

A conforming system SHALL define approval classes.

A practical model MAY include:

* automatic
* operator-approved
* multi-party approved
* organization-approved
* emergency-approved
* prohibited

### Approval flow

```text
REQUEST
   |
   v
CLASSIFY ACTION
   |
   +----> automatic ----------+
   |                          |
   +----> operator ---------- |
   |                          |
   +----> multi-party ------  |
   |                          |
   +----> prohibited -------> DENY
   |
   v
APPROVAL RESOLVED
   |
   v
ENFORCE OR HOLD
   |
   v
TRACE
```

---

## 6.6 Extended.Risk

### Meaning

Not all skills are equal in consequence.

### Requirement

A conforming system SHALL assign a risk tier to each skill.

A practical tier model MAY include:

* Tier 0 — passive
* Tier 1 — bounded transform
* Tier 2 — connected
* Tier 3 — sensitive
* Tier 4 — agentic
* Tier 5 — sovereign

### Risk ladder

```text
Tier 0 -> Tier 1 -> Tier 2 -> Tier 3 -> Tier 4 -> Tier 5
  low                                                     high
 risk                                                    impact
```

Higher tiers SHALL imply stricter:

* review
* admission
* activation
* approval
* execution limits
* incident response

---

## 6.7 Extended.Registry

### Meaning

The registry is part of the trust boundary.

### Requirement

A conforming registry SHALL support:

* publisher identity
* artifact history
* declaration visibility
* risk visibility
* review visibility
* withdrawal
* quarantine
* incident signaling

### Registry loop

```text
PUBLISHER --> REGISTRY --> OPERATOR --> RUNTIME --> TRACE --> REVIEW
                  ^                                         |
                  |                                         |
                  +----------- INCIDENT / WITHDRAWAL -------+
```

---

## 6.8 Extended.Incident

### Meaning

Compromise, misuse, drift, and failure must be governable.

### Requirement

A conforming ecosystem SHALL support:

* incident detection
* incident classification
* containment
* disablement
* trust suspension
* forensic preservation
* review
* remediation
* restoration or revocation

### Incident loop

```text
DETECT
  |
  v
CLASSIFY
  |
  v
CONTAIN
  |
  v
PRESERVE EVIDENCE
  |
  v
REVIEW
  |
  +----> REMEDIATE --> RESTORE
  |
  +----> REVOKE ----> BLOCK
```

---

## 6.9 Extended.HumanRoles

### Meaning

Human accountability must be explicit.

### Requirement

A conforming ecosystem SHALL distinguish, at minimum:

* author
* publisher
* reviewer
* operator
* approver
* auditor
* responder

### Accountability loop

```text
AUTHOR -> PUBLISHER -> REVIEWER -> OPERATOR -> APPROVER -> AUDITOR -> RESPONDER
   ^                                                                  |
   +--------------------------- governance feedback -------------------+
```

---

# 7. Deterministic Profile

## 7.1 Purpose of Deterministic

The Deterministic profile defines what is required for bounded, replayable, formally reviewable execution.

A system may conform to Core and Extended without conforming to Deterministic.

Deterministic conformance is for systems that wish to claim:

* deterministic execution mode
* deterministic reviewability
* LLM-off or bounded symbolic path
* replayable constitutional evidence

### Deterministic profile map

```text
Deterministic
|
+-- Deterministic.Mode
+-- Deterministic.Replay
+-- Deterministic.State
+-- Deterministic.TraceCompleteness
+-- Deterministic.VersionBinding
+-- Deterministic.CompositionBound
+-- Deterministic.ApprovalBinding
+-- Deterministic.LLMOff
```

---

## 7.2 Deterministic.Mode

### Meaning

A defined deterministic execution mode exists.

### Requirement

A conforming system SHALL define when deterministic execution mode is active and what constraints govern that mode.

---

## 7.3 Deterministic.Replay

### Meaning

Past executions can be reconstructed for governed review.

### Requirement

A conforming system SHALL support replay for executions claimed to be deterministic.

### Replay model

```text
PAST EXECUTION
   |
   +--> request
   +--> declarations
   +--> policy state
   +--> approvals
   +--> skill versions
   +--> chain structure
   +--> outcome
   |
   v
REPLAYABLE REVIEW
```

---

## 7.4 Deterministic.State

### Meaning

Execution-relevant state must be sufficiently preserved.

### Requirement

A conforming system SHALL preserve the state necessary to review deterministic executions.

---

## 7.5 Deterministic.TraceCompleteness

### Meaning

A trace must be sufficient for meaningful deterministic review.

### Requirement

A conforming system SHALL ensure traces for deterministic executions are complete enough to reconstruct decision flow.

---

## 7.6 Deterministic.VersionBinding

### Meaning

The exact governed versions in force must be bound to the execution.

### Requirement

A conforming system SHALL bind deterministic execution evidence to the exact versions of:

* skill
* declaration
* policy
* relevant runtime state

---

## 7.7 Deterministic.CompositionBound

### Meaning

Composed deterministic execution must remain reviewable and bounded.

### Requirement

A conforming system SHALL bound and preserve the structure of deterministic composition chains.

### Composition-bound model

```text
SKILL A --> SKILL B --> SKILL C
   |          |           |
   +----------+-----------+
              |
              v
      BOUNDED COMPOSITION
              |
              v
        DETERMINISTIC TRACE
              |
              v
             REVIEW
```

---

## 7.8 Deterministic.ApprovalBinding

### Meaning

Approvals must be bound to the exact execution context they authorize.

### Requirement

A conforming system SHALL bind approvals for deterministic execution to:

* exact request
* exact skill or chain
* exact policy state
* exact approval scope

---

## 7.9 Deterministic.LLMOff

### Meaning

A formally defined non-LLM or bounded symbolic path exists where claimed.

### Requirement

A conforming system SHALL NOT claim LLM-off conformance unless it can define and review the non-LLM or bounded symbolic path used for that claim.

---

# 8. Dependencies Between Subsections

Higher claims depend on lower ones.

A subsection SHALL NOT be claimed if its dependencies are absent.

## 8.1 Dependency map

```text
Core.ID -----------------------------+
                                     |
Core.SkillDecl ------------------+   |
                                 |   |
Core.Authority ----------------+ |   |
                               | |   |
Core.Policy -----------------+ | |   |
                             | | |   |
Core.Enforcement <-----------|-|-+   |
                             | |     |
Core.Trace <-----------------+-+-----+
                             |
Core.Review <----------------+

Extended.Admission ------> Core.SkillDecl, Core.Policy
Extended.Composition ----> Core.SkillDecl, Core.Authority, Core.Policy
Extended.Data -----------> Core.SkillDecl, Core.Policy, Core.Trace
Extended.Approval -------> Core.Policy, Core.Trace, Core.Review
Extended.Risk -----------> Core.SkillDecl
Extended.Registry -------> Core.ID, Core.SkillDecl, Extended.Admission
Extended.Incident -------> Core.Trace, Core.Review
Extended.HumanRoles -----> Core.ID, Core.Review

Deterministic.Mode ------------> Core.Policy, Core.Enforcement
Deterministic.Replay ----------> Deterministic.Mode, Core.Trace, Core.Review
Deterministic.State -----------> Deterministic.Mode
Deterministic.TraceCompleteness-> Core.Trace, Deterministic.Mode
Deterministic.VersionBinding --> Core.ID, Core.SkillDecl, Core.Policy
Deterministic.CompositionBound-> Extended.Composition, Deterministic.Mode
Deterministic.ApprovalBinding -> Extended.Approval, Deterministic.Mode
Deterministic.LLMOff ---------> Deterministic.Mode, Deterministic.VersionBinding
```

---

# 9. Conformance Claims

## 9.1 Rule

A system SHALL make claims only at the subsection level.

A system SHALL NOT claim generic compliance such as:

* “DI compliant”
* “Open Governance compliant”
* “Deterministic compliant”

unless the exact subsection claims are listed.

---

## 9.2 Human-readable examples

* Conforms to: `Core.ID, Core.SkillDecl, Core.Authority, Core.Policy, Core.Enforcement, Core.Trace`
* Conforms to: `Extended.Risk, Extended.Approval, Extended.Incident`
* Conforms to: `Deterministic.Mode, Deterministic.Replay, Deterministic.LLMOff`

---

## 9.3 Compact claim format

```text
DI-OG / Core : {ID, SkillDecl, Authority, Policy, Enforcement, Trace}
DI-OG / Extended : {Risk, Approval, Incident}
DI-OG / Deterministic : {Mode, Replay, LLMOff}
```

---

## 9.4 Full declaration example

```text
DI Open Governance Conformance Claim
Version: Draft-1
Scope: Production Runtime

Claims:
- Core.ID
- Core.SkillDecl
- Core.Authority
- Core.Policy
- Core.Enforcement
- Core.Trace
- Core.Review
- Extended.Risk
- Extended.Approval
- Extended.Incident
- Deterministic.Mode
- Deterministic.Replay
- Deterministic.LLMOff
```

---

# 10. Minimal Adoption Profiles

## 10.1 Core Minimal

A minimal governable DI system SHOULD implement:

* Core.ID
* Core.SkillDecl
* Core.Authority
* Core.Policy
* Core.Enforcement
* Core.Trace

```text
+----------------------------------------+
|         CORE MINIMAL PROFILE           |
+----------------------------------------+
| Identity                               |
| Skill Declaration                      |
| Deny-by-Default Authority              |
| Policy Before Action                   |
| Runtime Enforcement                    |
| Structured Trace                       |
+----------------------------------------+
```

---

## 10.2 Extended Minimal

A minimal institution-ready DI system SHOULD implement:

* Extended.Admission
* Extended.Composition
* Extended.Approval
* Extended.Risk
* Extended.Incident

```text
+----------------------------------------+
|       EXTENDED MINIMAL PROFILE         |
+----------------------------------------+
| Admission Lifecycle                    |
| Composition Governance                 |
| Approval Governance                    |
| Risk Tiers                             |
| Incident Governance                    |
+----------------------------------------+
```

---

## 10.3 Deterministic Minimal

A minimal deterministic DI system SHOULD implement:

* Deterministic.Mode
* Deterministic.Replay
* Deterministic.TraceCompleteness
* Deterministic.VersionBinding

```text
+----------------------------------------+
|    DETERMINISTIC MINIMAL PROFILE       |
+----------------------------------------+
| Deterministic Mode                     |
| Replay                                 |
| Trace Completeness                     |
| Version Binding                        |
+----------------------------------------+
```

---

# 11. Practical Reading of the Profiles

## Core asks:

**Is this system governable at all?**

## Extended asks:

**Can this system operate responsibly in a real ecosystem or institution?**

## Deterministic asks:

**Can this system prove what happened in bounded, replayable form?**

---

# 12. Final Declaration

We declare that open Deterministic Intelligence requires more than openness.

It requires a conformance model that can express:

* minimum governability
* institutional maturity
* deterministic reviewability

Therefore:

* **Core** defines whether DI is governable
* **Extended** defines whether DI is operationally mature
* **Deterministic** defines whether DI is replayable and bounded

We reject vague claims of compliance.

We require precise, subsection-based conformance.

We affirm that:

* skills require declaration
* declaration requires governance
* governance requires enforcement
* enforcement requires trace
* trace requires review
* review requires revocation or correction
* conformance requires precise claims

Therefore, any DI ecosystem intended for broad public trust SHOULD adopt this profile-based declaration, or a stricter compatible successor, as its constitutional foundation.
