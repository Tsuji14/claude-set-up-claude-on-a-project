# Notes

## What went into CLAUDE.md, and what was left out

Included: a one-line description of the project, the four npm scripts (`install`, `dev`, `test`, `lint`) plus how to target a single test file, the three-layer architecture (`server.js` → `routes/` → `db/store.js`) with the key detail that `app` is exported without calling `listen`, and two conventions — CommonJS module style and the JSON error response shape.

Left out: file-by-file directory listings (discoverable by reading the code), generic Node/Express practices, and any one-off setup steps that belong in the README rather than in a context file for Claude.

## Permission rules and their purpose

- **Allow** `npm test`, `npm run lint`, `npm run dev` — these are safe, read-only or sandboxed operations run many times per session; auto-approving them avoids friction.
- **Ask** `git push` — pushing affects shared state (the remote), so I want to confirm each time rather than let it happen silently.
- **Deny** `Read(./.env)` — without this rule Claude could read real secrets if a `.env` file exists locally. The deny rule makes that impossible regardless of what is asked.
- **Deny** `git push --force` — a force-push can permanently overwrite remote history; blocking it outright prevents an accidental or misguided suggestion from causing data loss.
