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

https://para0056.github.io/jwl-backup-merge/

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
