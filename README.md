# JWL Merge

> **⚠️ DISCLAIMER: This is an independent, community-made tool. It is NOT
> affiliated with, endorsed by, or connected to JW.ORG or the Watch Tower
> Bible and Tract Society of Pennsylvania in any way. "JW Library" is a
> trademark of the Watch Tower Bible and Tract Society. Use at your own risk.
> Always keep your original backup files before attempting a merge or restore.**

---

A browser-based tool to merge two JW Library backup (`.jwlibrary`) files into one.

**Everything runs client-side — your files never leave your device.**

---

## Live site

Once deployed, your site will be at:
`https://<your-username>.github.io/<repo-name>/`

---

## Setup (one-time, ~5 minutes)

### 1. Create a GitHub repository

Create a new **public** repository on GitHub (private repos require GitHub Pro for Pages).

### 2. Upload these files

Either clone the repo and push, or use GitHub's web UI to upload:

```
jwl-merge/
├── index.html
├── README.md
└── .github/
    └── workflows/
        └── deploy.yml
```

> **Note:** GitHub's web UI won't let you create `.github/workflows/` directly.
> Use the UI to create the file at path `.github/workflows/deploy.yml` and GitHub
> will create the directories automatically.

### 3. Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions**
3. Save

### 4. Trigger a deployment

Push any commit (or go to **Actions** → **Deploy to GitHub Pages** → **Run workflow**).
The site will be live at the URL shown in the Pages settings within ~30 seconds.

---

## How to use

1. Open your Pages URL in a browser
2. Drop your **primary** backup into the left zone (this one wins on tie-breaks)
3. Drop your **secondary** backup into the right zone
4. Click **Merge Backups**
5. Download the merged `.jwlibrary` file
6. In JW Library on your device: **Settings → Backup & Restore → Restore**

---

## Conflict resolution

| Data type              | Rule                                                        |
|------------------------|-------------------------------------------------------------|
| Highlights (UserMark)  | Higher `Version` number wins                                |
| Notes                  | Most recently modified wins                                 |
| Bookmarks              | Primary wins (deduped by publication + slot)                |
| Study guide answers    | Primary wins (deduped by location + field tag)              |
| Tags                   | Merged by name; no duplicates                               |
| Playlist items         | Full-content dedup; identical items collapsed               |
| Media files            | Deduped by SHA-256 hash; file copied once                   |

---

## Technical notes

- Uses [sql.js](https://github.com/sql-js/sql.js) (SQLite compiled to WebAssembly) for in-browser SQLite
- Uses [fflate](https://github.com/101arrowz/fflate) for ZIP read/write
- Both libraries load from cdnjs on first use (~1 MB total); requires internet access
- Compatible with JW Library backup schema v14 (tested); validates schema version
  match between the two files before merging
