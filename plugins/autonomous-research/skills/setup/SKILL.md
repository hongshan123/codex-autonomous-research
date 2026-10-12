---
name: setup
description: Use when initializing this autonomous research plugin in a scientific project, adopting an existing research setup, or upgrading project templates while preserving configuration and evidence.
---

# Initialize a research project

Work in the user's intended scientific repository, not the plugin/cache directory.
Read existing AGENTS.md, native configuration/roles, research memory and Git status
first. Use package resources relative to this Skill: [templates](../../templates/)
and [configuration contract](../../references/configuration.md).

## Incremental initialization

1. Establish the target root and inspect existing research goals and budgets.
   Preserve user/global config, experiment code, data, results and other plugins.
   Installing this plugin does not authorize external mutations or experiments.
2. Choose default model/effort and limits from `templates/research/CONFIG.toml`,
   applying explicit user choices. If adopting existing research, import its actual
   limits and usage; do not replace them with plugin defaults. If usage cannot be
   reconstructed from evidence, keep LOCKED and report the missing ledger.
3. Validate values using the configuration contract. Create missing research
   templates only; never overwrite GOAL/STATE/EXPERIMENTS/DECISIONS/LITERATURE or
   an existing BUDGET. Legitimate UNSET protocol fields remain blocking gates.
4. Render the three role templates into `.codex/agents/`, setting both model and
   effort from CONFIG. Merge supported native config keys from the config fragment,
   including the PI model and maximum concurrent child threads. Inspect native
   CLI help/version before adding the optional V2 fragment. Do not weaken existing
   permissions. Root PI remains read-only during initialization.
5. Add the managed AGENTS fragment once using its markers. Inspect contradictory
   existing rules and same-name roles before edits: leave conflicts intact and
   present concrete differences for resolution. Do not create duplicate TOML tables.
6. Create `.agents/skills/autonomous-research/SKILL.md` from the sibling workflow
   Skill and `research/CONFIG_REFERENCE.md` from the configuration contract. Preserve
   existing versions; adopt/merge them only when the user authorizes the difference.
7. Create `research/PROJECT.json` with schema_version=1, plugin name/version,
   config revision/hash and a managed_files mapping of project-relative paths to
   actual SHA-256 digests. Track only files this setup owns; exclude mutable shared
   memory and the budget ledger. Record actual hashes, not placeholders. Store
   model verification as pending, not passed. No machine-specific cache paths.
8. Record setup provenance in STATE/DECISIONS. Snapshot configuration under
   `research/config-history/0001/` (or the existing next revision), including native
   roles/config fragments and hashes. For adoption, retain the previous files and
   distinguish preexisting work from plugin initialization.

## Completion and upgrades

Report created/merged/skipped/conflicting files and keep status LOCKED. Require a
fresh trusted native Codex session for newly rendered models/roles; editing files
does not hot-reload the current PI. Explain how to invoke verify-environment.
Do not launch a smoke test or real experiment merely because initialization ran.

On repeat setup or upgrade, compare managed hashes to detect local edits. Use an
explicit diff-based migration; update the managed marker/version only after all
authorized changes succeed. Preserve configuration revision history, budgets,
scientific decisions and locked protocols. Partial initialization stays LOCKED.
