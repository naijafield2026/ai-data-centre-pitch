# AI GPU Data Centre — Nigeria | Investor Pitch

A single-page, self-contained investor pitch site for an AI GPU data centre venture in Nigeria, featuring an interactive financial calculator with multiple deployment pathways.

**Live site:** deployed on [Render](https://render.com) as a static site (see [Deployment](#deployment) below).

## Contents

- [`AI_Data_Centre_Pitch.html`](AI_Data_Centre_Pitch.html) — the entire pitch: markup, styles, and calculator logic in one file. No build step, no dependencies.
- [`render.yaml`](render.yaml) — Render Blueprint that provisions the static site and rewrites `/` to the pitch page.
- [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) — CI/CD: validates the HTML on every push and triggers a Render deploy on pushes to `main`.

## Run locally

No tooling required — open the file directly:

```sh
open AI_Data_Centre_Pitch.html
```

Or serve it:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000/AI_Data_Centre_Pitch.html
```

## Deployment

### One-time Render setup

1. Sign in at [dashboard.render.com](https://dashboard.render.com) and connect your GitHub account.
2. Click **New → Blueprint**, select this repository, and click **Apply**. Render reads `render.yaml` and creates the static site.
3. That's it — Render auto-deploys every push to `main`.

### CI/CD via GitHub Actions (optional deploy hook)

The workflow in `.github/workflows/deploy.yml` runs on every push and pull request:

1. **Validate** — lints the HTML with `htmlhint`.
2. **Deploy** — on pushes to `main`, calls the Render deploy hook if the `RENDER_DEPLOY_HOOK_URL` repository secret is set.

To enable the explicit deploy step (useful if you turn off Render's auto-deploy so deploys only happen after CI passes):

1. In the Render dashboard, open the static site → **Settings → Deploy Hook** and copy the URL.
2. In GitHub, go to the repo → **Settings → Secrets and variables → Actions** and add a secret named `RENDER_DEPLOY_HOOK_URL` with that URL.
3. (Optional) In Render **Settings → Build & Deploy**, set **Auto-Deploy** to *No* so the Action is the only deploy trigger.

## Editing the pitch

Everything lives in `AI_Data_Centre_Pitch.html`. Edit, commit, push to `main`, and the site redeploys automatically.
