# Re-Sync GitHub Pages Redeployment Guide

Live site: <https://tazrian08.github.io/Re_Sync/>

Repository: <https://github.com/tazrian08/Re_Sync>

Local deployment folder:

```text
D:\Games\RGP Maker Outputs\Re-Sync\Birthday
```

## 1. Export the updated game

Make your changes in the original RPG Maker MV project, then export/deploy the game for web or browser use.

The exported files must be copied so that `index.html` is directly inside the repository root:

```text
Birthday/
├── index.html
├── .nojekyll
├── audio/
├── css/
├── data/
├── effects/
├── fonts/
├── icon/
├── img/
└── js/
```

Do not place the export inside an extra folder such as `NewExport/`. GitHub Pages must be able to find `index.html` at the root.

If copying a fresh export over the deployment folder, preserve the empty `.nojekyll` file in the root.

## 2. Open the deployment folder

In PowerShell:

```powershell
cd "D:\Games\RGP Maker Outputs\Re-Sync\Birthday"
```

## 3. Review the changes

```powershell
git status
git status --short
```

Changed maps, events, JSON data, JavaScript, images, audio, plugins, and other game assets are normal after an update.

For text-based files, you can inspect the details with:

```powershell
git diff --stat
git diff
```

## 4. Commit the updated game

Use `git add -A` so new, modified, and deleted files are included:

```powershell
git add -A
git commit -m "Update game content"
```

Use a more specific message when appropriate, for example:

```powershell
git commit -m "Update forest map"
git commit -m "Add birthday event"
git commit -m "Fix battle animations"
```

If Git says there is nothing to commit, the exported files did not change or the changes are outside this repository folder.

## 5. Push to GitHub

```powershell
git push origin main
```

Do not run `git init` or `git remote add` again if this folder is already connected to GitHub.

For initial setup only, use:

```powershell
git init -b main
git remote add origin https://github.com/tazrian08/Re_Sync.git
git push -u origin main
```

## 6. Wait for GitHub Pages

After the push:

1. Open the repository's **Actions** tab.
2. Open the latest Pages deployment.
3. Wait for it to complete successfully.

The Pages settings should be:

- **Source:** Deploy from a branch
- **Branch:** `main`
- **Folder:** `/ (root)`

## 7. Test the live game

Open:

<https://tazrian08.github.io/Re_Sync/>

If the old version still appears, hard-refresh the browser with `Ctrl+F5` or use a private/incognito window. A temporary query string can also help bypass cached files:

<https://tazrian08.github.io/Re_Sync/?version=2>

Test the changed maps, events, plugins, images, audio, and save/load behavior on the deployed site.

## Troubleshooting

### Blank page or missing files

- Confirm `index.html` is at the repository root.
- Confirm the required `js/`, `data/`, `img/`, `audio/`, and other folders were committed.
- Keep the game paths relative, such as `js/main.js` and `data/System.json`.
- Check the browser developer console for the first failed file request.

### The update is not visible

- Confirm `git push origin main` completed successfully.
- Check the latest GitHub Pages deployment in **Actions**.
- Hard-refresh the page or use a private window.

### Large-file error

GitHub rejects individual files larger than 100 MB. Compress or reduce unusually large assets, or use Git LFS when appropriate.

Do not commit passwords, access tokens, or other secrets.
