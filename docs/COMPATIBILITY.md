# Compatibility and limits

## Delivery state

The source host has Codex CLI 0.162.1. This is an observed client, not a claimed
universal minimum version. CLI command/manifest checks do not prove runtime model,
sandbox or scientific readiness. See BUILD_REPORT for actual performed checks.

Native features are evolving. Inspect each client rather than assuming version
numbers alone guarantee role selectors, Goal Mode, model access or permissions.
The optional V2 fragment must not be applied to clients that reject its keys.

## Native Custom Agents

The documented discoverable directories are user `~/.codex/agents/` and project
`.codex/agents/`. v1 distributes role templates and uses setup to render project
files. The plugin manifest does not invent an agents registration field.
PI model selection lives in native project config and requires a newly configured
session. The plugin cannot switch an already running PI's model by editing files.

## Permissions

Parent live permissions can override role defaults. Previous observations on the
source host showed writable children under a writable PI, even for a read-only
literature role. New plugin roles have not passed a runtime smoke solely by being
packaged. Auditor intentionally uses workspace-write for its own report; immutable
evidence is enforced procedurally by independent checks. Do not call this hard
report-directory isolation. If literature is writable, keep research LOCKED.

Read-only local filesystems do not imply read-only connectors. The plugin supplies
no mutually exclusive tool allowlists and performs no external mutation probes.

## Linux sandboxes

AppArmor/user namespace policies can prevent native bubblewrap startup. Diagnose
the actual error. Do not disable AppArmor globally or choose unrestricted Codex
permissions. Legacy Landlock feature recognition does not establish restricted
execution compatibility. Host-specific preexisting profile workarounds are not
portable defaults; no sudo/system modifications are bundled in this plugin.

## Budgets and scientific scope

The native runtime does not turn these Skills into a GPU scheduler or accounting
service. PI reservations and finite job limits constrain authorized work; model
instructions alone are not a hard operating-system quota. GPU/training start at
zero. Protocols must specify corresponding resource enforcement/stop evidence.
For a non-ML project adapt metrics/inputs/uncertainty criteria explicitly; the
plugin does not guarantee any hypothesis will succeed or be novel.

## Privacy and distribution

Only generic templates/docs/Skills belong in this distribution. No auth.json,
global config, actual scientific data/logs, private native sessions or model files.
Per-project evidence remains in that project's research directory. A plugin update
does not carry Goal state across servers; project memory and native sessions have
different recovery mechanisms.
