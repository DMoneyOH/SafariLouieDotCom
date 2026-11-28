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
   the tour's own URL, the share-preview image tags (see "Share previews" below), the `Article`
   JSON-LD, the Google Fonts link, and `<link rel="stylesheet" href="../../assets/theme.css" />`.
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
- The `"image"` in each `blogPost` entry is the same full URL as that tour page's `og:image`.

## Share previews (Facebook and other sites)

When someone shares a page on Facebook, Facebook reads tags in the page's `<head>` to build the
preview card: the title, the description and a photo. Without the photo tags the card has no
picture.

**Every tour page carries each of these tags exactly once**, in the `<head>`, next to the other
`og:` tags:

| Tag | What goes in it |
| --- | --- |
| `og:type` | `article` |
| `og:title` | the same text as the page's `<title>` |
| `og:description` | the same text as the page's meta description |
| `og:url` | the tour's full address, the same as the canonical link |
| `og:image` | the full address of the tour's main photo (the photo in `<figure class="photo">`) |
| `og:image:width`, `og:image:height` | that photo's real size in pixels |
| `og:image:alt` | the same text as that photo's `alt` |
| `twitter:card` | `summary_large_image` |
| `twitter:image` | the same address as `og:image` |

Copy this block and change the parts in angle brackets. Keep the page's other tags, such as
`article:published_time` and `article:author`, where they are:

```html
<meta property="og:type" content="article" />
<meta property="og:title" content="<Tour title> | Safari Louie" />
<meta property="og:description" content="<the meta description>" />
<meta property="og:url" content="https://dmoneyoh.github.io/SafariLouieDotCom/tours/<tour-slug>/" />
<meta property="og:image" content="https://dmoneyoh.github.io/SafariLouieDotCom/assets/images/<tour-slug>.jpg" />
<meta property="og:image:width" content="<width in pixels>" />
<meta property="og:image:height" content="<height in pixels>" />
<meta property="og:image:alt" content="<the main photo's alt text>" />
<meta property="og:site_name" content="Safari Louie" />
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:image" content="https://dmoneyoh.github.io/SafariLouieDotCom/assets/images/<tour-slug>.jpg" />
```

Rules for the image address:

- Write the **full** address starting `https://`, never `../../assets/...`. Share previews
  need the full address.
- Match the file name exactly, including `.jpg` or `.webp` and lowercase letters. A wrong letter
  means no picture on Facebook.
- Facebook needs a photo at least 200 pixels wide **and** 200 pixels tall, and works best at
  1200 x 630 or larger. If the tour's only photo is smaller than 200 x 200, save an enlarged copy
  named `<tour-slug>-share.jpg`, use it in `og:image`, `twitter:image` and the home page's
  `blogPost` `"image"`, and leave the photo on the page as it is.

The home page uses `assets/images/home-hero-lewis.jpg`, the Lewis photo that opens the hero, for
its `og:image` and `twitter:image`. Keep those pointing at a real file in `assets/images/`.

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
