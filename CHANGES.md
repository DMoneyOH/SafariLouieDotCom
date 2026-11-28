# Changes

Newest entry first. Add an entry for every change to the site: the date, what changed, and why.

## 2026-11-28: Tour summary styled as a lead paragraph

**What changed.**

- **Tour pages:** the `tour-summary` paragraph under each tour's title now reads as a lead. It is
  set in Bitter at 1.2rem, a little heavier than the body text, with a gold line down its left
  edge. Before, it looked the same as the body text (Lora, 15.5px). On narrow phones (480px wide
  or less) it drops to 1.08rem so it does not crowd the screen.
- Changed in `assets/theme.css` only. No page text changed, and the home page does not use this
  style.

**Why.** The summary is the hook for each tour, so it should stand apart from the post text.

**What it means for future edits.** `SITE-GUIDE.md` has a new "The tour summary" part: one to
three first-person sentences, and the first body paragraph must not repeat them. Do not restyle
the summary inline in a page.

## 2026-11-27: Photo framing: Louie's photos shown whole, captions below the photo

**What changed.**

- **Tour pages:** each photo now shows whole, in its own shape. Before, every photo was cut to a
  wide 16:9 frame, so a tall photo such as Lewis the tiger on the Earth Day page showed only his
  forehead and eyes. Wide photos still fill the page width. Tall photos are limited to 80% of the
  window height, so they never run off the screen.
- **Captions:** the caption now sits below the photo. Before, it sat in a fixed strip, so on a
  phone a long caption (for example on the Akron Zoo page) wrapped up over the photo.
- **Home cards:** the photo frame is now 16:9, centred, instead of 4:3 cut from near the top. Most
  photos are 16:9, so the sides are no longer cut off. The old frame turned Louie's labels into
  "non Hippopotamus", "r Tiger" and "ted Gibbon". The Earth Day card has its own setting so
  Lewis's face shows in the frame.
- Small photos now show at their real size instead of stretched. The Africa and Wolf Woods photos
  are 240 pixels wide, so they look small on their pages. The fix for that is a bigger photo.
- Changed in `assets/theme.css` and in the home page's inline copy of the same rules. A second
  photo inside the post text is now centred like the first.

Only photo and caption framing changed. Colours, fonts, wording and the tape strip and tilt are
the same.

**Why.** Louie burns a species label and his tiger mark into his photos, and the old crops cut
them off.

**What it means for future edits.** `SITE-GUIDE.md` has a new "How photos are shown" part under
"Photos". New posts need no extra markup: use `<figure class="photo">` and a `polaroid` card as
before. A tall photo on a home card needs an `object-position` on its `<img>`.

## 2026-11-27: Text cleanup: photo credit, build notes, sitemap

**What changed.**

- The home-page gorilla slide said "Photo by Louie". The photo's own details credit Columbus Zoo
  and Aquarium, so the credit now says "Photo: Columbus Zoo and Aquarium".
- Removed build notes that showed to visitors: "Clean original: no title or watermark on the
  photo itself." under the Lewis hero photo, "Alternate hero, one tap away, the landing view is
  always Lewis." under the red panda and gorilla slides, and "No title across the bottom, no
  watermark. Just the tiger." in the Animal of the Month text.
- `sitemap.xml` no longer lists the seven `?page=` addresses. They show the same page as the
  home page. It now has the home page and the 64 tour pages.
- Removed the old copy of the sitemap hidden in the home page's `<head>`. Search engines ignore
  it and it was out of date.

Only wording and the sitemap changed. The layout and design did not.

**Why.** Visitors were reading notes meant for the builder, one photo credit was wrong, and the
sitemap pointed search engines at duplicate addresses.

**What it means for future edits.** `SITE-GUIDE.md` has new rules under "Voice, credits, captions
and the sitemap". New posts are written in the first person ("I", not "Louie"), following the voice
of Louie's own Facebook posts. Older pages that still say "Louie posted" are not changed in this
entry and will be converted separately.

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
