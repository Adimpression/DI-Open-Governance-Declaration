# DI Open Governance Conformance Specification

**Status:** Draft  
**Companion to:** `DECLARATION.md`  
**Audience:** Builders, operators, auditors, publishers, adopters, institutions, and regulators

---

## Abstract

This document defines how a system makes precise conformance claims against the DI Open Governance Declaration.

It does not restate the constitutional philosophy of the declaration.
Instead, it defines:

- the conformance profiles
- the subsection identifiers
- the dependency rules
- the evidence required for claims
- the valid and invalid forms of public compliance statements

This document exists to prevent vague claims such as “we are governed” or “we are deterministic” and replace them with precise, reviewable claims.

---

## 1. Relationship to the Declaration

`DECLARATION.md` defines the constitutional foundation of DI Open Governance.

`CONFORMANCE.md` defines how a system states, scopes, and substantiates its implementation of that foundation.

In case of conflict:

- `DECLARATION.md` governs the normative meaning
- `CONFORMANCE.md` governs the claim structure and evidence model

A system SHOULD publish both documents together.

---

## 2. Purpose

The purpose of this specification is to make DI Open Governance:

- claimable
- comparable
- reviewable
- incrementally adoptable
- resistant to vague compliance language

A conforming system SHALL make claims only through the structures defined in this document.

---

## 3. Conformance Model

Conformance is divided into three profiles:

```text
DI Open Governance
|
+-- Core
|
+-- Extended
|
+-- Deterministic
````

Each profile contains named subsections.

Claims SHALL be made at the subsection level.

A system MAY conform to:

* some Core subsections only
* Core plus some Extended subsections
* Core plus Extended plus some Deterministic subsections

A system SHALL NOT imply a higher-profile claim without explicitly listing the implemented subsections.

---

## 4. Profile Meanings

### 4.1 Core

Core defines the minimum structure required for a DI system to be governable at all.

Core answers:

**Is this system governable at all?**

### 4.2 Extended

Extended defines additional governance required for ecosystem, institutional, and multi-party maturity.

Extended answers:

**Can this system operate responsibly in a real organization or public ecosystem?**

### 4.3 Deterministic

Deterministic defines additional governance required for bounded, replayable, reviewable execution under deterministic constraints.

Deterministic answers:

**Can this system prove what happened in bounded, replayable form?**

---

## 5. Subsection Registry

The following subsection identifiers are defined by this specification.

### 5.1 Core

```text
Core.ID
Core.SkillDecl
Core.Authority
Core.Policy
Core.Enforcement
Core.Trace
Core.Review
```

### 5.2 Extended

```text
Extended.Admission
Extended.Composition
Extended.Data
Extended.Approval
Extended.Risk
Extended.Registry
Extended.Incident
Extended.HumanRoles
```

### 5.3 Deterministic

```text
Deterministic.Mode
Deterministic.Replay
Deterministic.State
Deterministic.TraceCompleteness
Deterministic.VersionBinding
Deterministic.CompositionBound
Deterministic.ApprovalBinding
Deterministic.LLMOff
```

Only these subsection identifiers SHALL be used unless a future version of this specification adds more.

---

## 6. Subsection Meanings

This section provides the operational meaning of each subsection.

### 6.1 Core Subsections

#### Core.ID

The system identifies governed entities sufficiently for accountability.

Minimum covered entities:

* skills
* policies
* operators
* approvals
* traces

#### Core.SkillDecl

Every skill must declare itself before trust.

Minimum declared fields:

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

#### Core.Authority

Authority is explicit, bounded, and deny-by-default.

Minimum authority classes:

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

Each grant must define:

* scope
* target
* context
* duration
* conditions
* approval class

#### Core.Policy

Policy governs:

* admission
* activation
* invocation
* material effect

#### Core.Enforcement

Material actions are mediated through enforcement rather than directly performed by skills.

#### Core.Trace

Material actions produce structured trace evidence.

At minimum, a trace must record:

* initiator
* request
* acting skill
* policy in force
* authority requested
* authority granted
* approvals
* affected data classes
* side effects
* result

#### Core.Review

The system provides a review path for material traces and decisions.

---

### 6.2 Extended Subsections

#### Extended.Admission

The system distinguishes these governed stages:

* publish
* review
* admit
* install
* activate
* invoke

#### Extended.Composition

The system governs skill combinations as wholes, not merely as isolated parts.

At minimum it evaluates:

* invocation chains
* delegation depth
* cycles
* authority unions
* emergent side effects
* hidden transitive behavior

#### Extended.Data

The system classifies data and binds skills to permitted data classes.

#### Extended.Approval

The system defines approval classes beyond policy-only execution.

#### Extended.Risk

The system assigns a risk tier to each skill.

#### Extended.Registry

The registry is part of the trust boundary and supports:

* publisher identity
* artifact history
* declaration visibility
* risk visibility
* review visibility
* withdrawal
* quarantine
* incident signaling

#### Extended.Incident

The ecosystem supports:

* detection
* classification
* containment
* disablement
* trust suspension
* forensic preservation
* review
* remediation
* restoration or revocation

#### Extended.HumanRoles

The ecosystem explicitly distinguishes accountable human roles.

Minimum roles:

* author
* publisher
* reviewer
* operator
* approver
* auditor
* responder

---

### 6.3 Deterministic Subsections

#### Deterministic.Mode

The system defines when deterministic execution mode is active and what constraints govern that mode.

#### Deterministic.Replay

Executions claimed to be deterministic can be replayed for review.

#### Deterministic.State

Execution-relevant state is sufficiently preserved for deterministic review.

#### Deterministic.TraceCompleteness

Trace evidence for deterministic executions is complete enough to reconstruct decision flow.

#### Deterministic.VersionBinding

Deterministic execution evidence is bound to the exact versions of:

* skill
* declaration
* policy
* relevant runtime state

#### Deterministic.CompositionBound

Deterministic composition chains remain bounded and reviewable.

#### Deterministic.ApprovalBinding

Approvals are bound to the exact execution context they authorize.

#### Deterministic.LLMOff

A formally defined non-LLM path or bounded symbolic path exists for the claim being made.

A system SHALL NOT claim this subsection unless the path can be defined and reviewed.

---

## 7. Dependency Rules

A system SHALL NOT claim a subsection unless all required lower dependencies are satisfied.

### 7.1 Dependency Map

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

## 8. Claim Rules

### 8.1 Allowed Claims

A system MAY claim:

* individual subsections
* a set of subsections within one profile
* a set of subsections across multiple profiles

### 8.2 Disallowed Claims

A system SHALL NOT claim any of the following without listing exact subsection identifiers:

* “DI compliant”
* “Open Governance compliant”
* “Governed DI compliant”
* “Deterministic compliant”
* “Fully conformant”

### 8.3 Partial Conformance

Partial conformance is valid.

A system MAY truthfully claim only what it implements.

That is a feature, not a weakness.

### 8.4 Public Claim Integrity

A public claim SHALL:

* list exact subsection identifiers
* identify the system scope
* identify the version of this specification used
* not imply unlisted conformance

---

## 9. Claim Format

### 9.1 Compact Claim Format

```text
DI-OG / Core : {ID, SkillDecl, Authority, Policy, Enforcement, Trace}
DI-OG / Extended : {Risk, Approval, Incident}
DI-OG / Deterministic : {Mode, Replay, LLMOff}
```

### 9.2 Full Claim Format

```text
DI Open Governance Conformance Claim
Specification Version: Draft-1
System Scope: Production Runtime

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

### 9.3 Scope Field

The scope field SHOULD state what exactly the claim applies to, for example:

* Core Runtime
* Skill Registry
* Production Runtime
* Deterministic Review Pipeline
* Institutional Deployment Profile

A claim without scope is incomplete.

---

## 10. Evidence Requirements

A system SHALL NOT make a subsection claim without evidence appropriate to that subsection.

This specification does not require a single universal evidence format, but it does require that evidence be reviewable.

### 10.1 Minimum Evidence by Core Subsection

#### Core.ID

Evidence SHOULD show governed entities and their identifiers.

#### Core.SkillDecl

Evidence SHOULD show the skill declaration schema and at least one actual declaration.

#### Core.Authority

Evidence SHOULD show authority classes and grant boundaries.

#### Core.Policy

Evidence SHOULD show where policy is applied in the lifecycle.

#### Core.Enforcement

Evidence SHOULD show that skills do not directly convert existence into effect.

#### Core.Trace

Evidence SHOULD show trace structure and at least one material trace example.

#### Core.Review

Evidence SHOULD show the path by which traces are reviewed.

---

### 10.2 Minimum Evidence by Extended Subsection

#### Extended.Admission

Evidence SHOULD show the lifecycle distinction between publish, review, admit, install, activate, and invoke.

#### Extended.Composition

Evidence SHOULD show how chain-level governance is evaluated.

#### Extended.Data

Evidence SHOULD show data classification and skill-to-data binding.

#### Extended.Approval

Evidence SHOULD show approval classes and how they bind to actions.

#### Extended.Risk

Evidence SHOULD show the risk-tier model and actual assignment.

#### Extended.Registry

Evidence SHOULD show registry governance fields and lifecycle actions.

#### Extended.Incident

Evidence SHOULD show the incident workflow and containment path.

#### Extended.HumanRoles

Evidence SHOULD show the role model and accountability mapping.

---

### 10.3 Minimum Evidence by Deterministic Subsection

#### Deterministic.Mode

Evidence SHOULD define deterministic mode and its constraints.

#### Deterministic.Replay

Evidence SHOULD show that a deterministic execution can be replayed.

#### Deterministic.State

Evidence SHOULD show what execution-relevant state is preserved.

#### Deterministic.TraceCompleteness

Evidence SHOULD show that deterministic traces are sufficient for review.

#### Deterministic.VersionBinding

Evidence SHOULD show exact version binding for governed artifacts.

#### Deterministic.CompositionBound

Evidence SHOULD show bounded composition structure for deterministic chains.

#### Deterministic.ApprovalBinding

Evidence SHOULD show that approvals bind to exact execution scope.

#### Deterministic.LLMOff

Evidence SHOULD show the non-LLM or bounded symbolic path used for the claim.

---

## 11. Minimal Adoption Profiles

These profiles are not mandatory bundles. They are recommended entry points.

### 11.1 Core Minimal

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

### 11.2 Extended Minimal

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

### 11.3 Deterministic Minimal

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

## 12. Valid and Invalid Public Claims

### 12.1 Valid

```text
Conforms to:
- Core.ID
- Core.SkillDecl
- Core.Authority
- Core.Policy
- Core.Enforcement
- Core.Trace
```

```text
Conforms to:
- Extended.Risk
- Extended.Approval
- Extended.Incident
```

```text
Conforms to:
- Deterministic.Mode
- Deterministic.Replay
- Deterministic.LLMOff
```

### 12.2 Invalid

```text
We are DI Open Governance compliant.
```

Invalid because no exact subsection claims are listed.

```text
We are deterministic.
```

Invalid because no exact deterministic subsections are listed.

```text
We conform to Extended.Composition.
```

Invalid if dependencies such as `Core.SkillDecl`, `Core.Authority`, and `Core.Policy` are absent.

---

## 13. Recommended Publication Pattern

A system publishing a conformance claim SHOULD publish:

1. specification version
2. system scope
3. subsection claims
4. evidence references
5. date of claim
6. operator or issuer identity

A practical publication pattern may look like:

```text
DI Open Governance Conformance Claim
Specification Version: Draft-1
System Scope: Production Runtime
Date: YYYY-MM-DD
Issuer: Example Organization

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

Evidence:
- skill declaration schema
- policy evaluation flow
- trace example
- risk tier policy
- incident runbook
```

---

## 14. Versioning Rule

Claims SHALL identify which version of this conformance specification they use.

A claim made against one version SHALL NOT be assumed to apply to a later version unless restated.

---

## 15. Final Rule

DI Open Governance conformance is not a slogan.

It is a precise claim about implemented governance structure.

Therefore:

* claims must be subsection-based
* higher claims depend on lower ones
* partial conformance is valid
* vague compliance language is invalid
* evidence must exist for every claim

Any system that adopts DI Open Governance SHOULD publish its claims in the form defined by this specification.
