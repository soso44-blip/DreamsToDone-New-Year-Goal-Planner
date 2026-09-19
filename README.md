# Dreams to Done — Goal & Resolution Planner (PWA)

This folder is the **hosted, installable version** of the planner — the link you sell to
customers. It works in any browser, installs to home screens, and runs **fully offline**
after the first visit. Everything is self-contained; there are no external dependencies.

## Files
- `index.html` — the planner (customer version)
- `manifest.webmanifest` — makes it installable ("Add to Home Screen")
- `sw.js` — service worker (offline cache)
- `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`, `apple-touch-icon.png`, `favicon.svg`, `favicon-32.png` — app icons
- `.nojekyll` — tells GitHub Pages to serve the files as-is

## Deploy on GitHub Pages (≈2 minutes)
1. Create a new **public** repository (e.g. `goal-resolution-planner`).
2. Upload **all files in this folder** to the repository (drag-and-drop works). Keep them
   together — the paths are relative, so root or a subfolder both work.
3. In the repo: **Settings → Pages → Build and deployment**. Set **Source** =
   "Deploy from a branch", **Branch** = `main`, **Folder** = `/ (root)`, then **Save**.
4. Wait ~1 minute, then refresh. Your live link appears at the top of the Pages settings:
   `https://<your-username>.github.io/<repo-name>/`
   That URL is what you share/sell.

GitHub Pages serves over HTTPS automatically, which is required for install + offline.

## Updating it later (important)
When you change `index.html`, **bump the cache version** so customers get the update:
1. Open `sw.js` and change `const CACHE = 'd2d-goal-planner-v1';` to `...-v2`, `-v3`, etc.
   (Or re-run `build.py`, which sets it — increment `CACHE_VERSION` there first.)
2. Commit the changed files. On each customer's next visit the new version installs
   automatically and the old cache is cleaned up.

If you skip the version bump, some customers may keep seeing the old cached version.

## Good to know
- **Data is per-device**: each customer's entries are saved in their own browser at this
  URL. Nothing is uploaded or tracked. They can move devices with the built-in
  **Backup / Restore** buttons.
- **Keep the URL stable.** Saved data is tied to the exact web address, so avoid changing
  the repo/URL after customers start using it.
- A custom domain is optional (Settings → Pages → Custom domain).
