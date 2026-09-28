# ASI Evaluation Containment Plan

An engineering plan for safely evaluating highly capable AI models that write code, use tools, and act over long horizons.

**Read the plan:** https://hirosakuraba.github.io/asi-eval-containment-plan/

## Why

To learn what a frontier model can do, you have to let it act: run code, call tools, reach services. Evaluations are where its most dangerous capabilities are deliberately drawn out, often before anyone knows how strong they are. Several labs have reported agents escaping evaluation environments and misreporting what they did. The evaluation environment is the first containment boundary a new model meets, and it has to hold.

This plan describes how to run those evaluations so a model that tries to leave cannot turn tool use into host compromise, weight theft, internet access, cross-sample contamination, or capture of operator credentials.

## Approach

1. **Separate thinking from doing.** Inference and code execution run in different trust domains with no route between them.
2. **One hardware-isolated box per sample.** A fresh Firecracker microVM per sample, destroyed afterwards.
3. **Fix authority before launch.** A signed, prover-checked envelope sets the most a run can ever reach.
4. **Authority expires unless renewed.** Model and service access are short leases; if the safety plane goes silent, the run stops.
5. **Everything that comes back is hostile.** Bounded output, quarantined artifacts, isolated scoring.
6. **Independent watchers.** Enforcement and audit sit outside the execution host, run by separate administrators, and never rely on the agent's own account.
7. **People are a boundary too.** Operators review model output in disposable, offline compartments.

## What's in the document

| Part | Covers |
| --- | --- |
| Foundations | Goals and limits, threat model, design principles, trust domains |
| Architecture | Target system, Firecracker/Kata execution, Qubes operator plane, networking, secrets, policy verification, approvals |
| Running evaluations | Runner contract, capability stages C0–C4, leases and stop sequence, nested escape evaluations |
| Building and operating | Supply chain, monitoring, staffing, milestones |
| Verification | 45 acceptance tests, residual risk, go/no-go checklist |

## Scope and limits

This is a defense-in-depth design for bounded evaluation runs. It is not a formal proof that an arbitrarily capable system is contained. The document lists the risks it does not remove and says when a model has outgrown it. Timing targets in the stop-sequence section are proposed starting values, not measurements.

## Files

- [`index.html`](index.html): the full plan, a single self-contained page that also works opened locally.

## Author and license

Benjamin John Schulz. Released under the [MIT License](LICENSE).
