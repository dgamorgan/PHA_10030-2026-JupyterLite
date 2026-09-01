# JupyterLite site scaffold

This is a minimal, working scaffold for deploying your Jupyter notebooks as a
browser-based, no-login Python environment via JupyterLite + GitHub Pages.

## What's in here

- `content/` — notebooks and data files that will be pre-loaded into the site
  for every visitor. `cPHA-10030_WS2_-_Linear_regression.ipynb` is already here
  (with the two fixes we made: reading `protein_assay.csv` from this same
  folder, and saving the output plot here too, instead of Colab's `sample_data/`).
  **You still need to add `protein_assay.csv` into this folder** — see
  `content/ADD_DATA_FILE_HERE.md`.
- `.github/workflows/deploy.yml` — builds the site and publishes it to GitHub
  Pages automatically, every time you push to `main`.
- `requirements.txt` — the Python packages needed to *build* the site (this is
  a build-time list, separate from whatever your notebooks import at runtime —
  numpy/pandas/scipy/sklearn get fetched by Pyodide when a student's browser
  runs the notebook, not installed here).

## One-time setup (do this once, in order)

1. **Create a new public repository on GitHub** (Settings you'll need to
   confirm: Public, not Private — Pages on a free personal account only
   publishes from public repos).
2. **Push this scaffold into it** — from inside this folder:
   ```
   git init
   git add .
   git commit -m "Initial JupyterLite scaffold"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo-name>.git
   git push -u origin main
   ```
3. **Enable GitHub Pages via Actions**, not the old branch-based method:
   - Go to your repo's **Settings → Pages**
   - Under "Build and deployment" → **Source**, select **GitHub Actions**
     (not "Deploy from a branch")
4. **Trigger the first build** — either push again, or go to the **Actions**
   tab and manually run the "Deploy JupyterLite site to GitHub Pages" workflow.
5. **Wait for it to finish** (a few minutes for the first build — it's
   installing Pyodide's build tooling, not just copying files). Check the
   Actions tab for progress and any errors.
6. **Find your URL** — once deployed, it'll be:
   ```
   https://<your-username>.github.io/<your-repo-name>/
   ```
   also shown on the Settings → Pages screen once live.

## Adding more worksheets later

Drop additional `.ipynb` files (and any data they need) into `content/`,
commit, and push to `main`. The workflow rebuilds and redeploys automatically
— no need to repeat the setup steps.

## Things worth testing once it's live, before relying on it in a session

- Open the URL yourself on a machine that's *not* your dev machine, ideally on
  the Keele lab network, and re-run the same checklist from the earlier
  campus test (imports, plot rendering, upload/download, persistence).
- The public demo site you tested against (`jupyterlite.github.io/demo`) and
  *this* site will be on a different URL/origin — a network policy could
  treat them differently, so don't assume yesterday's test result carries
  over automatically.
