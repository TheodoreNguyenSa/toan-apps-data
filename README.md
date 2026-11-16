# toan-apps-data

Data files for the Toan Nguyen In Oz TV apps page (https://toannguyeninoz.pp.ua/).

The page itself is only a shell: it fetches these files from GitHub at load time,
so content changes here go live without rebuilding the server.

## Files

- `apps.json` — the app list: names, descriptions (vi/en), repo, Downloader code,
  screenshots, and fallback version/size/APK link. The page still live-syncs the
  latest version + APK link from the GitHub API; this file is the fallback and
  the source of names/descriptions/codes/screenshots.
- `counts.json` — total GitHub download counts per app repo. Updated daily by the
  07:37 counts job (it reads the GitHub API and pushes this file). `tncointv`
  appears here once the job has counted it.
- `shots/` — the 2 screenshots per app shown on the cards.

## How to change the page content (no server rebuild needed)

- **Add an app:** append an entry to `apps.json` (copy an existing one), add its
  2 screenshots to `shots/`, commit. The card appears on the next page load
  (the page also auto-discovers any repo with a released APK, but without the
  Vietnamese name, screenshots or Downloader code).
- **Edit a name, description or Downloader code:** edit `apps.json`, commit.
- **New screenshots:** replace the files in `shots/`, commit.
- **Download counts:** do not edit by hand — the daily job rewrites `counts.json`.

## Notes

- Served via `https://raw.githubusercontent.com/TheodoreNguyenSa/toan-apps-data/main/<file>`
  (GitHub raw caches ~5 minutes, so edits appear within minutes).
- Counts include a few verification downloads by the assistant; see the note in
  `counts.json`.
