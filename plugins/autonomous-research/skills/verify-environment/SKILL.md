---
name: verify-environment
description: Use when verifying native custom-agent loading, actual models and reasoning efforts, sandbox permissions and a zero-GPU scientific smoke loop on a new project, server, client or configuration revision.
---

# Verify the native environment

Read project CONFIG, STATE, PROJECT metadata and the
[verification procedure](../../references/verification.md). Keep real research
LOCKED until every required gate passes. Use a new research/smoke/<id>/ directory
and preserve old reports. Verification is bounded by CONFIG smoke.max_wall_seconds.

Diagnose version/executable, config layers/trust, available role selector, sandbox
and tool permissions before creating agents. Use only an actual native named-role
selector; if unavailable, report NOT_SUPPORTED and stop, without ordinary Agent
substitution or an exec controller. Check actual model/effort, role identity and
instructions using native runtime metadata. Configuration and self-identification
alone cannot establish those facts.

For an explicitly requested smoke, sequentially create the three native roles
within the configured concurrency. Use only synthetic records and CPU arithmetic;
no model imports, inference, training, GPU queries/jobs, CUDA compilation or installs.
Verify permitted auditor report writing and independently preserved source/raw
evidence. Probe literature's actual read-only boundary with assigned disposable
canaries. Parent-permission inheritance is a failure if it violates that boundary.
Record tool visibility separately from allowed operations; never probe external
connector mutations. CUDA_VISIBLE_DEVICES is a precaution, not sandbox evidence.

Simulate PI hypothesis → experimenter synthetic results → auditor independent
recomputation → literature live verified prior method → PI revised toy hypothesis.
SIMULATED results do not enter the real experiment counter or scientific conclusions.
Update memory with an administrative smoke summary and unchanged real counters.
Capture creation, interaction, completion and available termination controls;
do not claim completed threads were closed if the client lacks close support.

Write per-run REPORT.md and evidence.json with actual evidence paths/hashes; PI
updates research/smoke/REPORT.md as an index/current gate summary. Missing metadata,
failed permissions or unavailable live search remain explicit blockers. Runtime
verification may pass while the scientific protocol/resources remain UNSET.
READY_FOR_RESEARCH requires both gates; report zero GPU usage in every outcome.
