# dt-design-system — Deploy mirror, NOT the working repo

> **2026-11-10:** la raíz de este sitio ahora sirve el DS nuevo (React + Tailwind, build de `dt-design-system-package`, ruta `#/docs`). El DS anterior en HTML quedó intacto en `/legacy/`. `colors_and_type.css` sigue en la raíz porque los prototipos del portafolio lo linkean.


**Do not design or build screens directly in this repo.** This is the deploy
target for Vercel. The actual working repo — where the design system is
developed, where `sections/*.json` and `renderers.js` live, where DES-XXX
ticket work happens — is:

```
https://github.com/diegolavandero-lgtm/dt-design-system-package  (branch: main)
```

That repo is owned by a different GitHub account (`diegolavandero-lgtm`, not
`diegolavandero`), which is why the two can't be merged into one git remote —
syncing between them is a deliberate copy step, not a git operation.

## What this repo is for

- Vercel is connected to this repo (`vercel.json` rewrites `/` → `/index.html`).
  A push to `main` here deploys automatically.
- Its `wrangler.jsonc` (Cloudflare) is legacy — an earlier CLAUDE.md in this repo
  claimed the live deploy was Cloudflare Pages at `dt-design-system-package.pages.dev`.
  That's stale: Diego confirmed Vercel is the current live target. Don't trust the
  Cloudflare claim if you see it referenced elsewhere (e.g. in the package repo's
  copy of this file) until it's corrected there too.
- This repo's own `Diego_Designs/` folder (not `Charlie_Designs/` — an earlier
  version of this file had that name wrong) holds already-shipped prototypes,
  copied here from the working repo once they're ready to be live.

## Workflow

1. Do the actual design/build work in `dt-design-system-package`.
2. When something is ready to go live, copy the relevant files here
   (`dt-design-system.html`, `colors_and_type.css`, `changelog.js/json`,
   `i18n.js/json`, updated prototypes) — do not hand-edit this repo's copies
   independently, they'll just diverge again.
3. Commit and push to `main` here. Vercel deploys automatically.

## Before relying on anything in this repo being current

Both `dt-design-system.html` in this repo and in the package repo may be out of
sync with each other right now — this hasn't been reconciled yet. Confirm which
is newer before treating either as ground truth.
