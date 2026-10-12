---
name: resume-research
description: Use when recovering interrupted autonomous scientific work, restoring a native Goal session or reconciling unfinished experiments and budget reservations before continuing.
---

# Resume research without losing evidence

Read CONFIG, BUDGET, PROJECT metadata, the five memory files, latest runtime report
and every outstanding run/checkpoint directory. STATE is an index; raw artifacts
and the budget ledger determine actual progress. Preserve completed work/failures.

1. Find the recorded native PI thread and child session/job IDs. Prefer native
   `codex resume <thread-id>` or available client resume controls. A new conversation
   can recover project files but does not automatically recover an old thread's
   Goal. Ask the user to start a new /goal when the old native Goal cannot resume.
2. Check only identified project jobs and their actual process/job status. Do not
   kill unrelated jobs or clear reservations because a conversation ended. Treat
   a process as active until stop/completion is proven; retain worst-case resource
   reservations when exact usage is unknown.
3. Reconcile timestamps, exit codes, checkpoints, raw results and hashes. Charge
   actual resource consumption and check used+reserved against current ceilings.
   Preserve interrupted/failed artifacts and every retry lineage.
4. If execution completed but audit is missing, audit the existing evidence next.
   Resume a checkpoint only under its original registered protocol and remaining
   allocation. A new experimental rerun consumes a new round; do not rerun a finished
   batch simply to reconstruct its summary. Report missing evidence explicitly.
5. Confirm current config/native roles match the run history. Server/client/model,
   effort or permission changes invalidate affected verification. Keep LOCKED if
   re-verification or an authorized protocol change is needed.
6. Update STATE with reconciled counters, active reservations, native thread and
   the exact next action. Continue only work already authorized and within budget.

Respect a user's explicit Goal pause; resume only when the user requests it.
Never reset counters, discard negative evidence, silently change protocols or
start external orchestration during recovery. Report recovered versus unresolved
work and the remaining allowance before launching a new task.
