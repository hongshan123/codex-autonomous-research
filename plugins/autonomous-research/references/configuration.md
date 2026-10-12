# Configuration and budget contract

## Sources and synchronization

`research/CONFIG.toml` contains plugin parameters, not native Codex settings.
Setup/configure Skills read it and explicitly merge native settings; there is no
automatic watcher, config loader executable or orchestration controller.
`research/BUDGET.toml` holds PI-only usage/reservations; `STATE.md` summarizes them.
Protocol paths and hashes describe the locked scientific experiment independently.

Precedence: latest explicitly authorized project settings → existing project
settings adopted from evidence → plugin defaults for missing fields. Native
administrator requirements still apply. Never overwrite user-global configuration.
Do not copy host trust, authentication, session IDs or AppArmor profiles to another
server. Each target project must be trusted through supported native controls.

## Parameters

| Key | Constraint | Meaning |
| --- | --- | --- |
| schema_version | integer, currently 1 | Unknown versions block activation until migrated |
| config_revision | positive integer | Increment once per applied change |
| models.<role>.model | nonempty string | Exact native model identifier; role is pi/experimenter/auditor/literature_researcher |
| models.<role>.reasoning_effort | nonempty supported string | Check against selected model/client; no silent fallback |
| budget.max_experiment_rounds | integer >= 0 | Cumulative formal execution starts |
| budget.max_route_adjustments | integer >= 0 | Cumulative scientific route proposals, including rejected ones |
| budget.max_repair_retries_per_round | integer >= 0 | Experimental repair descendants per initial lineage |
| budget.max_parallel_subagents | integer >= 1 | Concurrent native child threads, excluding PI |
| budget.max_parallel_gpu_experiments | integer >= 0 | Concurrent GPU jobs, separate from Agent threads |
| budget.max_experiment_wall_seconds | integer >= 1 | Finite cap for each experimental job |
| budget.total_gpu_hours | finite number >= 0 | Cumulative allocated devices × elapsed hours |
| budget.max_training_updates | integer >= 0 | Cumulative charged optimizer updates across jobs/conditions |
| budget.max_training_tokens | integer >= 0 | Cumulative charged training tokens across jobs/conditions |
| smoke.max_wall_seconds | integer >= 1 | Finite verification deadline |
| smoke.gpu_hours | exactly 0 | Smoke can never authorize GPU work |
| permissions.* | fixed v1 policy | Not a configurable permission bypass |
| protocol.* | complete before execution | UNSET blocks research; justified N/A permitted |

v1 permission policy is experimenter=workspace-write, auditor=workspace-write
for assigned reports, literature=read-only, procedural evidence-integrity checks.
Changing it requires a separately authorized policy revision and native verification.
Model configurability does not imply all model IDs/effort levels are available.
Use live official documentation and actual account/client capabilities.

## Native mapping

| Project parameter | Native destination |
| --- | --- |
| models.pi.model | `.codex/config.toml`: root `model` |
| models.pi.reasoning_effort | `.codex/config.toml`: root `model_reasoning_effort` |
| models.<child>.model | `.codex/agents/<child>.toml`: `model` |
| models.<child>.reasoning_effort | `.codex/agents/<child>.toml`: `model_reasoning_effort` |
| max_parallel_subagents | `.codex/config.toml`: `agents.max_concurrent_threads_per_session` |
| Experimental/route/GPU/training limits | PI Skills and project ledger; no equivalent native GPU scheduler |

Render both child model and effort, retaining role name, instructions and
permissions. Changes do not alter running sessions. Confirm native runtime values
in a fresh session; config file values alone are not proof of model use.

## Ledger transitions

Before launching, register an immutable run ID/protocol and reserve one round plus
worst-case GPU/training resources. Reservations include config/protocol hashes,
job owner, devices, timestamps, PID/job/session IDs, ceilings and stop evidence.
Verify `used + reserved + proposed allocation <= ceiling` for every applicable
resource. PI is the single writer; parallel children cannot mutate the ledger.

When formal execution starts, move the round from reserved to used exactly once.
All registered conditions/seeds of that batch share the round. Experimental
failures, interrupted starts and failed audits do not refund it. Cancellation
before execution may release a reservation only with evidence that no job started.
An experimental repair rerun uses a new ID/round and increments the root lineage's
repair count; it is subject to both ceilings. CPU code-only fixes do not consume
formal rounds but remain bounded by the job/task deadline.

GPU time includes allocated devices during setup, compilation, evaluation,
checkpointing and failure. Reconcile actual training updates/tokens independently
of Agent token usage. Reconcile elapsed resources on completion/interruption, but
retain conservative outstanding reservations when process state is unknown.
Release active-job reservations only after confirmed stop. A confirmed budget
violation stays recorded and blocks new execution; do not edit usage to fit.

Route proposals are charged when PI proposes a scientific mechanism/direction
change, including rejected proposals. Administrative configuration changes, initial
hypothesis registration and SIMULATED smoke revisions are not route proposals.
Do not rename repeated direction changes to avoid the cap.

## Changing ceilings

User-requested named changes authorize those settings. PI cannot expand them
autonomously. Never apply a ceiling below used+reserved totals. To stop further
work after prior consumption, pause the research; do not reset usage or set an
inconsistent zero ceiling. A 3→5 round increase with 2 used leaves 3 rounds.
Training/GPU default to zero; real allocations require explicit user authorization
and scientific protocol registration. A finite configured ceiling is not, by
itself, authorization to start jobs.

## Revisions and recovery

Record parameter diffs, user instruction reference, timestamp, hashes and native
file snapshots in config-history/<revision> and DECISIONS. Keep CONFIG_PENDING /
LOCKED during partial sync. No parallel config changes beneath active assignments.
PROJECT managed_files tracks only framework-owned policy/config/role/skill files;
never use it to overwrite mutable memory, ledger or experiment artifacts.
For a new host with identical config hashes, old runtime verification still cannot
prove the new sandbox. Reverify and preserve existing usage and protocols.
