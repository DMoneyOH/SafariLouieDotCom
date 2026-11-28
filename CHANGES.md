# Changes

Newest entry first. Add an entry for every change to the site: the date, what changed, and why.

## 2026-11-27: Photos moved out of the HTML into image files

**What changed.** Every photo used to sit inside the HTML pages as base64 text
(`src="data:image/..."`). Each one is now a normal image file in `assets/images/`, and the
pages point to it. 138 embedded photos became 90 files, because the 48 photos that appear on
both a home card and its tour page are now stored once. The files are the original photos, byte
for byte: nothing was resized or recompressed. No wording, layout, styling or class changed.

**Why.** The home page was 19.1 MB, almost all of it photo data, so it loaded slowly and the
browser could not reuse a photo between the home page and a tour page. It is now 0.23 MB.
Real image files are also what share previews and search results need, which later fixes
depend on.

**What it means for future edits.**

- Add every new photo as a file in `assets/images/`. Never paste a photo into the HTML as
  base64.
- From the home page, reference a photo as `assets/images/<name>.jpg`. From a tour page,
  reference it as `../../assets/images/<name>.jpg`.
- File naming and the rest of the conventions are in `SITE-GUIDE.md`.
