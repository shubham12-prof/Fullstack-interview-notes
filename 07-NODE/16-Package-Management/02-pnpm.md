# pnpm

A drop-in alternative package manager focused on disk space efficiency and speed, using a different storage strategy than npm/Yarn.

**Key difference — content-addressable storage:**
Instead of copying package files into every project's `node_modules` (npm's default approach), pnpm stores each package version **once** in a global content-addressable store on disk, and uses **hard links** (or symlinks) to reference it from each project's `node_modules`.

```bash
pnpm install               # install dependencies (much faster on repeat installs, less disk usage)
pnpm add express               # add a dependency
pnpm add -D jest                  # add a devDependency
pnpm remove express                  # remove a dependency
pnpm run dev                            # run a script
```

**Strict, non-flat `node_modules` structure by default:** unlike npm's historically flat `node_modules` (which allowed accidentally importing packages that weren't directly declared as dependencies — "phantom dependencies"), pnpm creates a nested structure via symlinks that only exposes packages a project explicitly depends on.

```
node_modules/
├── express -> .pnpm/express@4.18.2/node_modules/express   (symlink)
└── .pnpm/                                                     (actual content-addressable store links)
```

**Monorepo support (`pnpm workspaces`)** is a major reason teams adopt pnpm — efficient, first-class handling of multi-package repositories:
```yaml
# pnpm-workspace.yaml
packages:
  - "packages/*"
  - "apps/*"
```

**npm vs pnpm — key tradeoffs:**

| | npm | pnpm |
|---|---|---|
| Disk usage | duplicates packages per project | shared global store, minimal duplication |
| Install speed | slower (especially on repeat installs) | notably faster |
| Phantom dependencies | possible (flat node_modules) | prevented by design (strict linking) |
| Ecosystem/default | universal default, ships with Node | requires separate install, growing adoption |

**Interview note:** pnpm's main selling points are disk space savings (critical when many projects/branches share dependencies) and stricter dependency isolation that catches "phantom dependency" bugs npm's traditional flat structure could hide.
