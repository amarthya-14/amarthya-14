# Setup Instructions

## 1. Push this folder's contents to your profile repo

```bash
# If you haven't cloned it yet:
git clone https://github.com/amarthya-14/amarthya-14.git
cd amarthya-14

# Copy in the contents of this folder (README.md and .github/) then:
git add -A
git commit -m "feat: rebuild dashboard with metrics + 3D contribution graph"
git push
```

If `snake.yml` or a `dist/` folder exist in your repo from an earlier version, delete them — they're no longer used.

## 2. Enable workflow write permissions

Repo → **Settings → Actions → General → Workflow permissions** → select **"Read and write permissions"** → Save.

## 3. Create the METRICS_TOKEN secret

The metrics workflow needs a personal access token (the default token doesn't have enough scope for full language stats).

1. GitHub (top-right avatar) → **Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token**
2. Scopes: check `repo` and `read:user`
3. Generate, then copy the token
4. Go to the **amarthya-14** repo → **Settings → Secrets and variables → Actions → New repository secret**
   - Name: `METRICS_TOKEN`
   - Value: paste the token
5. Save

## 4. Confirm repo visibility

Repo → **Settings → General** → make sure visibility is **Public** (required for the profile README to render on github.com/amarthya-14).

## 5. Run the workflows manually the first time

Repo → **Actions tab** → click into "Generate Metrics Dashboard" → **Run workflow** button → same for "3D Contribution Graph".

Wait ~1–2 minutes for each to finish (green checkmark).

## 6. Verify

- Check the repo root for a new `github-metrics.svg` file
- Check for a new `profile-3d-contrib/` folder with SVG files inside
- Visit `github.com/amarthya-14` and hard-refresh (Ctrl/Cmd+Shift+R)

## Troubleshooting

| Symptom | Fix |
|---|---|
| Metrics workflow fails with auth error | Recheck `METRICS_TOKEN` secret has `repo` + `read:user` scopes |
| `github-metrics.svg` never appears | Workflow permissions not set to read-write (step 2) |
| 3D graph image broken on profile | Check the actual filename generated inside `profile-3d-contrib/` — the action can output slightly different filenames; update the README's `<img src>` to match exactly |
| Profile shows old cached images after a successful run | Wait a few minutes — GitHub's raw content CDN caches briefly, then hard-refresh |
