# ASI Evaluation Containment Plan (v4)

A defense-in-depth plan for running capability, alignment, and agentic evaluations against highly capable models without letting tool use turn into host compromise, weight theft, internet reach, cross-sample contamination, or capture of operator credentials.

**Read it:** open [`index.html`](index.html) in a browser, or view the GitHub Pages site if it is enabled for this repo.

## What's in it

- Seven separated trust domains: execution (Firecracker, optional Kata), orchestration, artifact/scoring quarantine, inference, an independent safety/model-path plane, backend secrets, and the operator plane (Qubes).
- Verifiable policy: a signed maximum authority envelope checked by a policy prover before launch, plus conformance testing between the prover's model and the real enforcers.
- A fail-closed model path: inference and brokered service access run on short leases that stop by themselves unless the safety plane keeps renewing them.
- A defined stop sequence (cut model → revoke credentials → drop network → pause VM → forensic capture → destroy).
- Capability stages C0–C4, residual-risk register, go/no-go checklist, and 45 acceptance tests.

## v4 changes

v4 reviews v3 against its own threat model and against NVIDIA's Open Agent Safety Platform and OpenShell material (28 September 2026). The findings table at the top of the document lists each gap (F1–F18) and where it is fixed.

## Status and limits

This is an engineering design for bounded evaluation runs. It is not a formal proof that an arbitrarily capable system is contained. Timing targets in §9A are proposed starting values, not measurements.

Author: Benjamin John Schulz
