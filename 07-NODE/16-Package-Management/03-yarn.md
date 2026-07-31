# yarn

An alternative package manager originally created by Facebook to address early npm limitations (deterministic installs, speed) — npm has since closed most of that gap, but Yarn remains widely used, especially Yarn Classic (v1) and the newer Yarn Berry (v2+).

```bash
yarn init -y
yarn add express                  # install and save to dependencies
yarn add --dev jest                  # install as a devDependency
yarn remove express                     # uninstall
yarn install                               # install everything from yarn.lock
yarn run dev                                  # or simply: yarn dev
yarn upgrade                                     # update dependencies within semver ranges
```

**`yarn.lock`** serves the same purpose as npm's `package-lock.json` — locking exact dependency versions for reproducible installs. The two lock file formats are NOT interchangeable; a project uses one or the other, not both.

**Yarn Classic (v1) vs Yarn Berry (v2+):** Berry introduced **Plug'n'Play (PnP)** — an alternative resolution strategy that can skip creating a `node_modules` folder entirely, instead generating a single `.pnp.cjs` file mapping packages directly to their location in a cache, which can significantly speed up installs and reduce disk usage (conceptually similar in spirit to pnpm's efficiency goals, via a different mechanism).

**Workspaces (monorepo support) — a long-standing Yarn feature, also adopted by npm/pnpm since:**
```json
// package.json (root of a monorepo)
{
  "private": true,
  "workspaces": ["packages/*", "apps/*"]
}
```

**High-level comparison across all three:**

| | npm | Yarn | pnpm |
|---|---|---|---|
| Default with Node? | Yes | No | No |
| Lock file | package-lock.json | yarn.lock | pnpm-lock.yaml |
| Disk efficiency | lowest (duplication) | moderate (Classic) / high (Berry PnP) | highest (content-addressable store) |
| Notable feature | universal default, huge ecosystem | Plug'n'Play (Berry), mature workspaces | strict dependency isolation, fastest installs |

**Interview note:** in practice, all three package managers are largely interchangeable for basic dependency management (`install`, `add`, `remove`, scripts) — the meaningful differentiators interviewers care about are disk/install-speed efficiency (pnpm), monorepo tooling maturity (Yarn, pnpm), and whether a team needs zero extra tooling (npm, since it ships with Node).
