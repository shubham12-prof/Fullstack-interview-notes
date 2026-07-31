# npm

Node's default package manager — installs, manages, and publishes JS packages, bundled with every Node.js installation.

```bash
npm init -y                    # create a package.json with defaults
npm install express               # install a package, save to dependencies
npm install --save-dev jest          # install as a devDependency (not needed in production)
npm install -g nodemon                  # install globally (available as a CLI command anywhere)
npm uninstall express                       # remove a package
npm update                                     # update packages within semver ranges
npm run <script-name>                             # run a script defined in package.json
npm audit                                            # scan for known vulnerabilities
```

**`package.json` — the manifest file:**

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "test": "jest"
  },
  "dependencies": { "express": "^4.18.2" },
  "devDependencies": { "jest": "^29.7.0" }
}
```

**Semantic versioning (semver) in dependency ranges:**

```
^4.18.2   -> compatible with 4.x.x (allows minor/patch updates, not major)
~4.18.2   -> compatible with 4.18.x (allows only patch updates)
4.18.2    -> exact version only
```

**`package-lock.json`** records the EXACT resolved version of every dependency (including nested/transitive ones), ensuring reproducible installs across machines — should always be committed to version control.

```bash
npm ci   # installs EXACTLY what's in package-lock.json (faster, stricter — used in CI pipelines)
```

**Interview note:** `npm install` vs `npm ci` — `install` can update `package-lock.json` and is more lenient; `ci` deletes `node_modules` first and installs strictly from the lock file, failing if `package.json` and the lock file are out of sync — making it the standard choice for CI/CD pipelines where reproducibility matters most.
