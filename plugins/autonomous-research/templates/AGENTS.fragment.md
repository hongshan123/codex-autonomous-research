<!-- autonomous-research:begin -->
## Autonomous scientific research

The primary agent is the PI. Read `research/CONFIG.toml`, `research/BUDGET.toml`,
`research/STATE.md`, and all five scientific memory files before research work.
Use `.agents/skills/autonomous-research/SKILL.md` for the scientific loop.
Models and limits come from the project configuration; no model is hardcoded here.

Use only native Codex Custom Agents, Skills, AGENTS.md and Goal Mode for control.
Delegate implementation/execution to the native `experimenter`, independent audit
to a fresh native `auditor`, and live literature verification to the native
`literature_researcher`. Children must not delegate. Explicitly select custom roles;
never substitute a default Agent for a requested role/model.

Keep real research LOCKED until current runtime checks and a complete protocol
pass. Auditor may write its assigned report; it cannot edit audited code, raw
evidence, configuration or shared memory. PI independently checks hashes/diff.
This is procedural ownership, not a directory-level sandbox. Literature requires
an actual read-only sandbox; parent permission inheritance is a possible blocker.
Filesystem permissions do not enforce read-only access to external connectors.
External messages, uploads and mutations require explicit user authorization.

PI alone maintains shared memory and budget reservations. Count failed formal
experiments and experimental reruns; preserve all seeds and failure artifacts.
No unbounded GPU work. Every run has registered resources, finite timeout and
stop evidence. No single negative result refutes an entire research direction.
Changing locked inputs, test sets, primary metrics, seeds, scientific model,
training/compute budgets or the core question requires explicit user authorization.
Stop at configured limits. Resume without resetting counters or repeating finished
work. Plugin installation is not authorization to train or execute experiments.
<!-- autonomous-research:end -->
