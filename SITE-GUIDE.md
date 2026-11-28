# Safari Louie site guide (for the site builder)

Follow these rules every time you add or edit a page. They describe how the site already works.
Do not redesign it.

## Folder layout

```
index.html                    home page: hero, tour cards, By Zoo, Lewis & Clark, About
tours/<tour-slug>/index.html  one page per photo tour
assets/theme.css              shared colours and fonts for the tour pages
assets/images/                every photo on the site
sitemap.xml, robots.txt       search-engine files
CHANGES.md                    change log
```

`<tour-slug>` is the tour title in lowercase, punctuation dropped, words joined by hyphens. For
example, "Fiona the Hippo" is `fiona-the-hippo` and "Tyler's Request" starts `tylers-request`. The slug is the folder name, the home card's `id` and
the start of the photo's file name.

## Photos

- **Never put a photo inside the HTML as base64** (`src="data:image/..."`). Every photo is a
  separate file in `assets/images/`.
- Save the photo as JPEG (`.jpg`) or WebP (`.webp`).
- Name it after the tour: `<tour-slug>.jpg` for the tour's main photo,
  `<tour-slug>-2.jpg` for a second photo, `<tour-slug>-3.jpg` for a third.
- If the home card shows a different photo from the tour page, name it `<tour-slug>-card.jpg`.
  If the card shows the same photo, reuse the tour's file. Do not save a second copy.
- Home-page photos that belong to no tour start with `home-`, for example `home-hero-lewis.jpg`.
- Use lowercase letters, digits and hyphens only. No spaces. The site is case-sensitive, so
  `Fiona.JPG` and `fiona.jpg` are different files.
- Keep `alt` text on every photo, describing what the photo shows.

How to reference a photo depends on which page it is on:

| Page | Write the path like this |
| --- | --- |
| Home page (`index.html`) | `<img src="assets/images/fiona-the-hippo.jpg" alt="..." loading="lazy" />` |
| Tour page (`tours/fiona-the-hippo/index.html`) | `<img src="../../assets/images/fiona-the-hippo.jpg" alt="..." />` |

The tour page needs `../../` because it sits two folders down, the same way it links
`../../assets/theme.css`.

## Tour page template

Copy a tour page that already has a `<p class="tour-summary">` (the current format, for example
`tours/kilimanjaro-safaris/index.html`) and change its content. Keep this structure:

1. `<head>`: title `<Tour title> | Safari Louie`, meta description, canonical and `og:` tags with
   the tour's own URL, the `Article` JSON-LD, the Google Fonts link, and
   `<link rel="stylesheet" href="../../assets/theme.css" />`.
2. `<header class="top">`: text logo plus Photo Tours, About Louie and Facebook links.
3. `<main>`, in this order: `<p class="date">` with a `<time>`, `<h1>` title, `<p class="where">`
   with the zoo and tour number, `<p class="tour-summary">` (a short first-person summary), the
   main photo in `<figure class="photo">` with a handwritten `<figcaption>`, then
   `<div class="tour-body">` with the post text.
4. Extra photos inside the body use `<figure class="photo tilt-l">` or `tilt-r`. Put a
   `<p class="credit">` under any photo that is not Louie's.
5. End the body with `<p class="on-fb">` linking the original Facebook post, then
   `<p class="back">` linking back to all tours.
6. The same `<footer>` as every other tour page.

## Home page patterns

- Each tour has one card: `<article id="<tour-slug>" class="tour" data-zoo="...">` holding
  `<a class="tour-link" href="tours/<tour-slug>/">`, a `polaroid` photo with a `hand` caption, and a
  `tour-body` with date, zoo and tour number, `<h3>` title, summary and "Read the full tour".
- `data-zoo` is one of `columbus`, `cincinnati`, `louisville`, `newport`, `disney` or `more`.
- The newest tour card goes first.
- The hero slides at the top use the `home-hero-*` photos.
- When you add a tour, also add it in three more places, copying the shape of the entries already
  there: the `blogPost` list and the `ItemList` (raise `numberOfItems` by one) in the JSON-LD near
  the top of `index.html`, and a `<url>` line for `tours/<tour-slug>/` in `sitemap.xml`.

## Colours and fonts

They live in `assets/theme.css` (the home page carries its own copy inline; keep the two in step).
Night-safari palette: background `#14213d`, text `#f5f0e1`, soft text `#c9c0a3`, lines `#35507f`,
gold accent `#fca311`, green accent `#8ac926`, polaroid paper `#f5f0e1`, footer `#0c1526`.
Fonts: Lora (body), Bitter (headings), Public Sans (labels and navigation), Caveat (handwritten
captions and dates).

## Publishing

- GitHub Pages publishes the `main` branch to https://dmoneyoh.github.io/SafariLouieDotCom/.
  Anything on `main` is live.
- Never change `main` directly. Make every change on a new branch.
- The owner previews the branch before anything is merged. Nothing goes live until he approves.
- Add an entry to `CHANGES.md` for every change: the date, what changed, and why.
