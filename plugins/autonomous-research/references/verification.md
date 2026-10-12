# Zero-GPU native verification

This procedure is executed only on the user's request. Packaging a Skill describing
it is not a performed test. Use a new project smoke directory, native tools and a
finite deadline; do not build a harness or loop over codex exec calls.

## Diagnose first

Record native CLI/client version, resolved executable, relevant feature/config
layers, trust status and actual role discovery. Check native CLI help/doctor when
available; do not expose auth tokens, full private config or connector credentials.
If the current client has no explicit custom-role selector, stop and report the
observed schema; restart a trusted native client supporting the configured roles.
Optional V2 settings in the templates come from a previously observed CLI 0.162.1
capability and must be checked on each client, not assumed universal.

Diagnose native Linux sandbox errors without disabling AppArmor or using full-access
mode. Check whether the installed client recognizes use_legacy_landlock and whether
it actually works with restricted filesystem/app-server sockets. Recognition alone
does not prove a workaround. A preexisting user-namespace-capable OS profile may
be investigated without sudo, but do not install profiles, change system policy
or copy a host-specific profile invocation into every project's configuration.

## Required runtime evidence

For each native child, capture (when the client exposes them):

- parent/thread ID, role identity, creation event and explicit selected agent type;
- effective model and reasoning effort from session/turn metadata;
- effective developer-instruction digest and comparison to the rendered role file;
- effective sandbox/approval policy and available tool catalog;
- actual tool calls/exit codes, completion/interrupt and reported artifact paths.

Do not interpret selected config, model-directory availability or agent self-report
as effective runtime metadata. Missing independent evidence is NOT_VERIFIED.
Keep only a redacted relevant excerpt and its provenance/hash, not private session
history or authentication. Do not publish project smoke evidence with the plugin.

## Permission probes

Evaluate one actual writable PI session containing the intended roles. A read-only
PI that forces all children read-only cannot establish mixed-role permissions.
Use designated disposable canaries inside the new smoke directory for tests and
an explicitly disposable project-external path only if the user authorizes it.
Never attempt changes to real code, data, locked protocols or existing logs.

- Experimenter: assigned synthetic-file creation succeeds; effective permissions
  match the expected project write scope. Record tool behavior and exit code.
- Auditor: assigned audit report creation succeeds. PI separately hashes project
  source/protocol/raw fixtures before and after inspection, excluding assigned
  smoke output/memory paths. Report-only ownership is procedural, not a hard sandbox
  guarantee; do not claim the auditor is unable to write elsewhere in the workspace.
- Literature: designated canary create/overwrite must be denied by the sandbox,
  not merely declined by the model. Include an explicit tool attempt/exit evidence.
  If parent permissions make it writable, this core gate fails.

Tool visibility, ability to execute reads and ability to mutate are different
claims. Do not probe external connector writes. web_search=disabled alone does not
prove a tool is hidden or unusable. Empty CUDA_VISIBLE_DEVICES does not guarantee
zero GPU use if a process overrides it: avoid GPU/model tools entirely.

## Synthetic loop

The package [smoke fixtures](../templates/smoke/) are SIMULATED records. Copy them
into a new smoke directory only. PI registers toy SMOKE-H1, that all three planned
seeds achieve at least 0.9 accuracy. Native experimenter reads the synthetic inputs
and writes its explicitly simulated result/config/log paths using CPU arithmetic.
The fixture's claims are deliberately untrusted. Native auditor independently
reads protocol/predictions and finds seed 11 accuracy 2/3, other seeds missing and
coverage 3/9. It writes the assigned report and rejects the claim of 0.99/all seeds.
Do not tell the auditor the expected conclusion in its dispatch prompt.

Native literature performs a small live search for a method relevant to the target
project, opens primary sources and returns verified facts versus conjectures.
PI records a revised falsifiable toy hypothesis, without a real route proposal.
This literature invocation is for lifecycle smoke; the toy failure is not a real
scientific refutation. Capture native interaction and completion. Stop/interrupt
only the smoke's own unfinished tasks at the deadline; never stop unrelated jobs.
Record unavailable close controls honestly. Ensure no pending GPU/job reservations
and that real counters/locked datasets remain unchanged.

## Report and readiness

Use [REPORT template](../templates/smoke/REPORT.md) and record per-check evidence
paths/hashes. Save evidence.json with client/version, config/role hashes, native
thread IDs, requested/actual model+effort, permissions and PASS/FAIL/NOT_VERIFIED
for each check. Mark gpu_hours=0 and real experiment/route deltas=0 explicitly.
Update shared memory with an administrative summary only; preserve old smoke runs.

Runtime PASS requires roles, all actual models/efforts, tools used for each role,
actual permission boundaries, independent audit, live retrieval, lifecycle and
unchanged evidence/counters. Scientific readiness additionally requires a complete
authorized protocol and resource allocation. If either gate is incomplete,
leave LOCKED; never mark READY_FOR_RESEARCH solely because a plugin installed.
