# Publish to your GitHub repository

The plugin has a local repo marketplace, so the same tree can be distributed from
GitHub without rewriting the marketplace to a host-specific absolute path.
Codex resolves its local source path relative to the fetched marketplace root.
Both the portable root manifest and compatibility manifest use version 0.1.0.

## Before publication

1. Choose the GitHub owner, repository name and public/private visibility.
2. Review the package and BUILD_REPORT. This version has no verified cross-server
   or fresh role/model/permission smoke claim; preserve those limitations.
3. Choose an open-source license before advertising reuse under that license.
   No license grant has been assumed on the user's behalf.
4. Commit the package, configure the exact remote, and push when the user authorizes
   that destination. Do not copy target project's research records into this repo.
5. Create/push tag v0.1.0 only once the user accepts that release. Keep both manifest
   versions synchronized for later releases and document migration effects.

## Installation on another server

```bash
codex plugin marketplace add OWNER/codex-autonomous-research --ref v0.1.0
codex plugin add autonomous-research@research-tools
```

Do not use a sparse checkout containing only `.agents/plugins`: this marketplace
references `./plugins/autonomous-research`, so that plugin directory must also be
present. A full checkout is the simplest initial distribution.

After installation, initialize each scientific repository independently, select
models/limits, restart the trusted native project session and run zero-GPU
verification. Keep old usage and experimental protocols when migrating projects.
The plugin's v0.1.0 defaults do not override an adopted project's authorized limits.

## Upgrades

Use native marketplace help to inspect refresh/pinned-ref behavior. Install/update
the intended release source, restart the client and explicitly run setup migration
in each project. Compare managed hashes; preserve local edits and all research
memory. No automatic experiment/Goal starts during installation or upgrade.
