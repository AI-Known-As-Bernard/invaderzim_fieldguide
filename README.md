# A Field Guide to Invader ZIM

**Student:** Lastname, Firstname
**Course:** Web Development — HTML Unit
**Folder:** `lastname-firstname-fieldguide/`

## Topic

A field guide to the characters of *Invader ZIM* (Nickelodeon, 2001–2006), catalogued the way a birding guide catalogues birds: species, home range, identification notes, and observed behaviour. Every entry in the guide is a named character from the television series — no ships, gadgets, snacks, or locations.

The nine characters are Zim, GIR, Dib Membrane, Gaz Membrane, Professor Membrane, Ms. Bitters, Almighty Tallest Red, Almighty Tallest Purple, and Tak. Red and Purple are filed separately rather than as a combined "Almighty Tallest" entry, because they behave differently and the contrast between them is the point.

All content is real writing. There is no placeholder text anywhere in the project.

## Pages

Eleven HTML pages: a home page, a contribute form, and one full detail page per character.

| File | Character / purpose |
| --- | --- |
| `index.html` | Home — hero, stats, featured character, nine-card collection grid, guide notes + sidebar, email signup |
| `entry.html` | **Zim** |
| `entry-gir.html` | GIR |
| `entry-dib.html` | Dib Membrane |
| `entry-gaz.html` | Gaz Membrane |
| `entry-membrane.html` | Professor Membrane |
| `entry-bitters.html` | Ms. Bitters |
| `entry-red.html` | Almighty Tallest Red |
| `entry-purple.html` | Almighty Tallest Purple |
| `entry-tak.html` | Tak |
| `contribute.html` | Submission form |

**On the filename `entry.html`:** the brief lists `entry.html` as a required deliverable, so the Zim page keeps that exact name and the other eight follow the `entry-<name>.html` pattern. If consistent naming matters more than matching the brief's file list, rename it to `entry-zim.html` and update the links that point at it.

**All nine entry pages use identical markup.** They were generated from one template, so the structure is the same on every page: breadcrumb → `article.entry` → `header.entry__header` → `figure`/`figcaption` → `dl.spec-list` (7–8 pairs) → four `section.entry__section` blocks → `aside.entry-related`. The list lives in section two and the blockquote in section three, on every page. One CSS rule set will style all nine.

---

## Image Credits

**Read this before you submit.** The `images/` folder currently contains no image files. The filenames below are the ones the HTML expects. You must supply them yourself and then fill in this table.

There is a real conflict to solve here: the assignment requires images you have the right to use, and screenshots or promotional art from *Invader ZIM* are copyrighted by Nickelodeon/Viacom and are **not** licensed for reuse. Downloading a screenshot from a wiki does not make it usable. Three routes that actually satisfy the rule:

1. **Draw them yourself.** Nine character illustrations, photographed or scanned, used for both the thumbnail and the full-size image. You hold the copyright, so you can credit yourself. This is the cleanest option and the one I would pick.
2. **Wikimedia Commons cosplay and convention photography.** Search Commons for "Invader Zim cosplay" and check each file's license — CC BY or CC BY-SA is fine as long as you credit the photographer and name the license.
3. **Swap to thematic stock photos.** Unsplash or Pexels images of suburban streets at night, CRT televisions, lab equipment, and handheld consoles, used as mood images rather than character portraits. Fully licensed, but you would want to loosen the alt text to match what is actually pictured.

Whichever route you take, update the `alt` attributes so they describe the image you actually used. Alt text describing a picture you did not include is worse than no alt text.

| Filename | Used on | Source / photographer | License | Link |
| --- | --- | --- | --- | --- |
| `hero-banner.jpg` | index.html — hero | *fill in* | *fill in* | *fill in* |
| `featured-gir.jpg` | index.html — featured | *fill in* | *fill in* | *fill in* |
| `zim-thumb.jpg` / `zim-full.jpg` | card + entry.html | *fill in* | *fill in* | *fill in* |
| `gir-thumb.jpg` / `gir-full.jpg` | card + entry-gir.html | *fill in* | *fill in* | *fill in* |
| `dib-thumb.jpg` / `dib-full.jpg` | card + entry-dib.html | *fill in* | *fill in* | *fill in* |
| `gaz-thumb.jpg` / `gaz-full.jpg` | card + entry-gaz.html | *fill in* | *fill in* | *fill in* |
| `membrane-thumb.jpg` / `membrane-full.jpg` | card + entry-membrane.html | *fill in* | *fill in* | *fill in* |
| `bitters-thumb.jpg` / `bitters-full.jpg` | card + entry-bitters.html | *fill in* | *fill in* | *fill in* |
| `red-thumb.jpg` / `red-full.jpg` | card + entry-red.html | *fill in* | *fill in* | *fill in* |
| `purple-thumb.jpg` / `purple-full.jpg` | card + entry-purple.html | *fill in* | *fill in* | *fill in* |
| `tak-thumb.jpg` / `tak-full.jpg` | card + entry-tak.html | *fill in* | *fill in* | *fill in* |

That is twenty files: nine thumbnails, nine full-size, plus the hero and the featured shot. Each `<figcaption>` currently points readers back to this file for the credit — replace that sentence with the real one once you have it.

**Sizing note:** the `width` and `height` attributes are 600×400 for card thumbnails, 1000×667 for entry-page images, 900×600 for the featured image, and 1200×675 for the hero. Either crop to those ratios or update the attributes to the real pixel dimensions. The numbers exist to reserve layout space and prevent the grid from jolting as images load, so they need to match reality.

---

## Layout Plan

**CSS Grid** does the heavy structural work in five places. `.card-grid` is the main event — `grid-template-columns: repeat(auto-fit, minmax(260px, 1fr))` on the `<ul>` turns nine identical `<li>` siblings into a responsive card grid that goes one-up, two-up, and three-up on its own with no media query at all. `.hero` becomes a two-column grid (text left, image right) because its text block and image are siblings; `.guide-notes` becomes `2fr 1fr` for the article-plus-aside pairing; `.spec-list` on every entry page becomes `max-content 1fr` so the `<dt>` labels and `<dd>` values line up as a clean spec sheet; and `.footer-cols` is a four-column grid. `.contribute-form` is a two-column grid where `.form-row--full` spans both via `grid-column: 1 / -1`.

**Flexbox** handles the one-dimensional rows. `.site-header`'s `.wrap` flexes the logo against the nav; `.nav-list` flexes four `<li>`s into a horizontal bar in one line; `.stats-list` is a flex row with `justify-content: space-between`; `.breadcrumb-list` is a flex row; `.signup-form` flexes so the input grows with `flex: 1` while the button keeps its natural width; and `.footer-bottom` is a flex row. Each `.card` also becomes `display: flex; flex-direction: column` with `.card__body` set to `flex: 1`, which pushes `.card__link` to the bottom of every card so all nine links align across the grid regardless of description length.

**Media queries** should be needed in only three or four spots, since `auto-fit` and `flex-wrap` cover most of the responsive behaviour for free. I expect one breakpoint around 768px to collapse `.hero` and `.guide-notes` from two columns to one and to stack `.signup-form` and `.footer-bottom` vertically; one around 600px to switch `.contribute-form` to a single column and stack `.stats-list`; and one at the same width to turn `.site-header` into a stacked block with a wrapping nav. The card grid should need no breakpoint at all — if it does, something has gone wrong with the `minmax()` values rather than with the markup.

**The payoff of nine identical entry pages:** one `.entry` rule set styles all of them. Because the pages came from a single template, there is no card-five-has-an-extra-paragraph problem to work around later.

---

## Notes on Structural Choices

Places where the brief left room for judgement, and what I decided:

- **`.wrap` inside sections that are also layout containers.** The brief asks for a `.wrap` in every full-width section, and also asks for the hero's text block and image to be siblings so Grid can position them. Both hold: the `.wrap` sits inside `.hero`, and the text block and image are siblings inside it. Grid gets applied to `.hero .wrap` rather than to `.hero`. Same pattern in `.guide-notes`.
- **`.footer-cols` wrapper.** The four `.footer-col` blocks are wrapped so they can be a four-column grid without `.footer-bottom` becoming a fifth grid item. Load-bearing, not decorative.
- **Nav anchor hrefs.** The in-page anchors are written `index.html#collection` and `index.html#guide-notes` rather than bare `#collection`, so the identical header works on all eleven pages. On `index.html` the browser resolves them as same-page jumps, so behaviour is unchanged.
- **`aria-current` on entry pages.** No main-nav link points at a character page, so `aria-current="page"` sits on the final breadcrumb item, which is the correct place for it on a detail page. `index.html` and `contribute.html` mark it in the main nav as normal.
- **`.visually-hidden` on the stats heading.** `.stats` has no visible heading, so it gets an `<h2 class="visually-hidden">` — real text for screen readers, hidden with CSS next unit. That is what the class is in the shared vocabulary for.
- **Footer columns link to real entries.** Rather than dead category links, two of the footer columns link to actual character pages, which also means several entry pages are reachable from every other page in one click.

## Facts and Sources

Air dates, episode counts, and voice credits were checked against the series page on Wikipedia and the full cast list on IMDb. The series ran 27 episodes (46 segments) across two seasons, premiering with *The Nightmare Begins* on March 30, 2001.

Blockquotes on the entry pages are original in-universe field observations attributed to invented researchers (Marla Vex, Hollis Renn, P. Okonjo) rather than quoted dialogue from the show. That keeps the project clear of reproducing copyrighted script material while still satisfying the `<blockquote>` + `<cite>` requirement.

## Validation

All eleven pages are written to pass the W3C validator with zero errors. Run each through <https://validator.w3.org/#validate_by_upload> before submitting, since anything you edit — especially image credits and alt text — is a chance to introduce one.
