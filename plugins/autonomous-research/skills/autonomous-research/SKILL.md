---
name: autonomous-research
description: Use when conducting autonomous scientific research in an initialized project through native custom agents and Goal Mode, with falsifiable hypotheses, bounded experiments, independent audits and literature-guided revisions.
---

# Autonomous scientific research

The primary agent is the PI. Read AGENTS.md and research/CONFIG.toml, BUDGET.toml,
GOAL.md, STATE.md, EXPERIMENTS.md, DECISIONS.md and LITERATURE.md before choosing
work. Read research/CONFIG_REFERENCE.md for configuration/ledger semantics.
Use only native Custom Agents, AGENTS.md, Skills and Goal Mode for orchestration.
Only create a native Goal when the user explicitly requests it (including /goal).

## Entry gate and ownership

Real research requires READY_FOR_RESEARCH, a complete authorized protocol, current
native role/model/effort evidence and actual permissions. If the client cannot
explicitly select custom roles, report the limitation and stop delegation. Never
use a default Agent to impersonate a role. PI alone updates shared memory/ledgers.
Use fresh auditor context with raw paths and protocol, without a preferred verdict.
Children do not delegate. Auditor writes only its assigned report; PI independently
checks source/protocol/raw hashes and diff. Literature is read-only and returns
findings for PI persistence. These instructions do not provide connector allowlists
or a report-only filesystem sandbox.

## Scientific loop

1. **Hypothesis:** PI reads code, prior experiments and goals; distinguishes facts,
   assumptions and inference; specifies a mechanism, competing explanations and
   falsifiable predictions with refutation/success criteria.
2. **Minimal experiment:** Choose the cheapest discriminating experiment. Register
   an immutable protocol for the run: source/config/input versions and hashes,
   split/sample identities, calibration/test separation, baselines, primary scorer,
   all conditions/seeds, budget fairness, uncertainty/failure policy, exact commands,
   finite timeout, artifacts and audit destination. Non-ML projects register their
   corresponding independence/uncertainty controls; justified N/A is explicit.
3. **Execute:** Reserve a round and worst-case resources in BUDGET before spawning
   native experimenter. Charge the formal round when execution begins. Require raw
   logs, exit codes, actual commit/snapshot, dirty diff, configs, all seeds/failures,
   raw observations, metrics and hashes. Numerical claims are unaudited at this step.
4. **Independent audit:** Native auditor reads/recomputes raw evidence, checking
   leakage, fairness, seeds, scorers, uncertainty and provenance. PI checks evidence
   preservation independently. Missing independent evidence is not an accepted result.
5. **Implementation failure:** Assign a bounded repair to experimenter. Preserve
   failed artifacts and lineage. Code-only CPU repairs consume no new formal round;
   an experimental rerun consumes another round and the lineage retry allowance.
6. **Insufficient hypothesis evidence:** Design a targeted diagnostic/ablation
   within the remaining allowance. Avoid promoting noisy/single-run negative evidence
   to a rejection of an entire research direction.
7. **Supported refutation:** After sufficient registered independent checks and
   alternatives, invoke native literature_researcher for live verified methods,
   theory and author code. Open supporting sources, record dates and separate
   VERIFIED / AUTHOR_REPORTED / INFERENCE / UNTESTED claims.
8. **New mechanism:** PI compares existing methods and evidence, proposes a new
   falsifiable mechanism and cheapest discriminator, records the route proposal and
   its reasoning, then registers the next round if authorized and within budget.

Audits use PASS, IMPLEMENTATION_ERROR, INSUFFICIENT_EVIDENCE,
PROTOCOL_VIOLATION or SUPPORTED_REFUTATION. PASS validates evidence, not the truth
of the hypothesis. Protocol violations block scientific acceptance.

## Budget and stopping

Read current ceilings from CONFIG and usage/reservations from BUDGET. A formal
batch covering registered conditions/seeds consumes one round; failures, retries,
diagnostics and ablations are counted, never refunded. Route proposals consume an
allowance even when rejected. Never start unbounded jobs. Charge allocated GPU
count times elapsed hours, including device-bound setup and failed work. Reserve
training updates/tokens and reconcile actual use. Release reservations only after
confirmed termination. Do not exceed active GPU or child-agent concurrency.

At limits, major protocol changes or a changed core question, pause scientific
execution and request concrete user authorization. Silence is not approval.
Never change locked evaluation inputs, primary metric, seed list, scientific model
or training/compute budget autonomously. Never select favorable seeds as the sole
main result. Persist evidence and remaining allowance before the turn ends.

## Memory and native Goal

Maintain the five memory files and a complete index of every attempt/audit/decision.
Each run records config revision/hash; config changes preserve all used counters.
With a user-started native Goal, continue authorized useful work through the same
loop until its success criteria are met or a concrete gate needs user input.
Report native Goal status honestly and obey its budget/status rules; research
ceilings remain additional limits. Resume by reconciling processes, artifacts and
reservations before work. Do not repeat completed runs or discard negative evidence.

An explicitly requested zero-GPU smoke is SIMULATED and confined to a new
research/smoke directory; it is not hypothesis evidence and consumes no formal
rounds or route proposals. Its success alone cannot authorize real research.
