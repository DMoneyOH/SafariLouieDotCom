# Changes

Newest entry first. Add an entry for every change to the site: the date, what changed, and why.

## 2026-11-27: Share previews now show a photo

**What changed.**

- Every tour page now tells Facebook (and other sites) which photo to show when the page is
  shared: its main photo, with the photo's size and description. The preview card is now the
  large-photo kind.
- The home page used to point its share photo at `assets/logo.jpg`, a file that never existed.
  It now uses `assets/images/home-hero-lewis.jpg`, the Lewis photo that opens the home page.
- The list of tours hidden in the home page for search engines (the JSON-LD) pointed at 65
  photo files that never existed. Each one now points at the real photo in `assets/images/`.
- Two tours, Africa and Wolf Woods, only have a photo 240 pixels wide and about 135 tall. That is
  below Facebook's 200 x 200 minimum, so each got an enlarged copy used only for sharing:
  `africa-share.jpg` and `wolf-woods-share.jpg`. The photos on the pages did not change.

Only hidden tags in each page's `<head>` changed. Nothing you see on any page changed.

**Why.** Facebook is where every tour gets posted, and until now a shared tour showed up as a
text-only card with no photo.

**What it means for future edits.** Every new tour page needs the share-preview tags. The rule
and a block to copy are in `SITE-GUIDE.md` under "Share previews".

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
