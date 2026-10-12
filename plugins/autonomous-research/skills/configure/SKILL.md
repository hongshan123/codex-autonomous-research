---
name: configure
description: Use when choosing or changing research agent models, reasoning efforts, experiment or route limits, concurrency, timeouts or compute budgets in an initialized project.
---

# Configure models and research limits

Read CONFIG, BUDGET, STATE, PROJECT metadata and the latest protocol before changes.
Use the [configuration contract](../../references/configuration.md). Resolve only
the requested changes; preserve other keys and existing native config. User choices
take precedence over plugin defaults. Model strings are configurable; do not
silently choose a different available model or reasoning level.

## Apply a revision

1. Build a before/after parameter diff. Determine whether the user's instruction
   already authorizes the change. A direct request to increase a named limit is
   authorization for that limit, not for changing locked evaluation criteria.
   PI-proposed budget increases or protocol changes require explicit confirmation.
2. Check live jobs/agents and outstanding reservations. Do not alter configuration
   beneath running work. Preserve its original revision and account/stop it through
   the native tools before activating new settings. Do not kill unrelated jobs.
3. Validate types/ranges, model-effort support and used+reserved totals. Reject an
   active ceiling below already used/reserved amounts; report the conflict. Zero
   experiment/route/GPU/training budgets intentionally disable those activities.
   Agent concurrency and job timeouts must remain positive and finite.
4. Snapshot old CONFIG and affected native files under config-history. Increment
   config_revision exactly once. Mark STATE as LOCKED with CONFIG_PENDING before
   mutation, then update CONFIG and merge PI/role model+effort and agent concurrency
   into the native files. Never copy the whole fragment over existing config.
5. Check that selected values agree in CONFIG and all affected native files. Record
   actual hashes and the revision in PROJECT metadata, config-history and DECISIONS.
   If any write/check fails, keep CONFIG_PENDING/LOCKED, preserve both snapshots,
   and report which files disagree; never report successful activation.
6. A model/effort, role instruction, permissions, client or selector change
   invalidates corresponding runtime verification. Resume only in a fresh session
   after verification. A budget-only change may retain valid runtime evidence if
   model/role/native permissions are unchanged and the protocol remains authorized;
   record that decision rather than automatically clearing LOCKED.

Never reset BUDGET, failures, retry lineage or route counts during configuration.
An increase from 3 to 5 rounds with 2 used gives 3 remaining, not 5. Count usage
and reservations before launching work. GPU concurrency is separate from child
Agent concurrency and is not a native GPU scheduler. Do not modify test sets,
primary metrics, scientific model/data revisions or seed policy as a side effect.

Return the applied revision, parameter diff, remaining allowance and exact next
action. The current PI's model does not change until the native client applies it.
