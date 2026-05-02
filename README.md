# DI Open Governance Declaration

This repository defines a profile-based governance declaration for open **Deterministic Intelligence (DI)**, plus a companion conformance specification that makes implementation claims precise, comparable, and reviewable.

The core design goal is to replace vague statements like “we are governed” or “we are deterministic” with explicit, subsection-level claims (e.g., `Core.Trace`, `Extended.Approval`, `Deterministic.Replay`).

## Documents

- `DECLARATION.md` — the normative meaning (what each subsection requires).
- `CONFORMANCE.md` — how to make, scope, and substantiate conformance claims (profiles, subsection identifiers, dependency rules, evidence expectations, valid/invalid public claim formats).

## Conformance Model (Profiles)

The declaration is organized into three adoption profiles:

- **Core**: minimum structure required for a DI system to be governable at all.
- **Extended**: additional governance for institutional / ecosystem maturity.
- **Deterministic**: additional governance for bounded, replayable, formally reviewable execution.

Conformance is declared **at the subsection level**, and higher-profile claims depend on lower-profile subsections (see the dependency map in both documents).

## Example Claim (Compact)

```text
DI-OG / Core : {ID, SkillDecl, Authority, Policy, Enforcement, Trace}
DI-OG / Extended : {Risk, Approval, Incident}
DI-OG / Deterministic : {Mode, Replay, LLMOff}
```

## License

Creative Commons Attribution 4.0 International (CC BY 4.0). See `LICENSE`.

