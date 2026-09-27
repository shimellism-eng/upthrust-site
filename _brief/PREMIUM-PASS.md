# Upthrust website: premium pass

A review of the first build (branch `site-v1`, commits `6bbbaa0` and `32a0c63`), written as a brief the next session can apply without asking. Read `SITE-BRIEF.md` first: every rule in its section 0 still holds (no-reply author, never touch `CNAME` or `main`, relative paths, no scripts that touch the network, no prices, no sign-ups, no names, no board logos, no em dashes, British English). Where this file and `SITE-BRIEF.md` disagree, this file wins: it is the later decision.

Work on a new branch `site-v2` started from `origin/site-v1`, and refresh the pull request from it. Keep every page working on the branch preview (`raw.githack.com`) on a real phone.

The verdict, in one paragraph. The build is complete, correct and honest. It is not premium, and the reasons are all craft rather than content: the phones are drawn as thick black wireframes, every screenshot is the light theme even when the page is dark, every phone is shown whole so the page is nine screens long on a phone, the page is flat (no depth behind the hero, no shadow on anything, no motion anywhere), section headings swap between centred and left, and the Screens gallery repeats four screens already shown above it at a size nobody can read. Fix those and the same words and screens read as a finished product.

---

## 1. The screenshots to use (new ones are in `_brief/screens/`)

Fourteen real captures were taken from the app on 27 September 2026 at 402 points wide, in both themes, from the same sample student as before (AQA, separate physics, Higher, made-up practice). They were taken at 3x and are saved here at 2x (804 pixels wide) as WebP, to match the six already in `assets/screens/`. Twelve are used; move them into `assets/screens/` on the build branch. They carry no exam board quotation and no personal data. The band pair is cropped at 640 points, above the list of specification points, on purpose: keep that crop.

| File (light / dark) | Shows | Size | Alt text |
|---|---|---|---|
| `home-light.webp` / `home-dark.webp` | Home: days to Paper 1, days this week, "Working at 6 to 7" band with "Estimate, never a prediction", Today card with a lesson to carry on | 804 x 1748 | `Upthrust Home screen: days to the first exam, practice this week, a grade band of 6 to 7 marked as an estimate, and today's lesson.` |
| `home-locked-light.webp` / `home-locked-dark.webp` | Home before the band has unlocked: Today card with four questions back from earlier lessons and a lesson to carry on, then a "Grade band, 1 of 4 unlocked" card with four rings | 804 x 1748 | `Upthrust Home screen before the grade band has unlocked: four questions back from earlier lessons, today's lesson, and four rings showing what the band still needs.` |
| `question-light.webp` / `question-dark.webp` | The bar magnet question, unanswered, four options | 804 x 1748 | `A question asking where a bar magnet's field is strongest, with field lines drawn round the magnet and four marked points.` |
| `why-light.webp` / `why-dark.webp` | The same question answered right, Why? open | 804 x 1748 | `The answer marked right, with a Why? panel explaining that the field is strongest at the poles.` |
| `coil-light.webp` / `coil-dark.webp` | The magnet being pushed into the coil, needle swung | 804 x 1748 | `An animation: a magnet being pushed into a coil of wire, with the meter's needle swinging.` |
| `band-light.webp` / `band-dark.webp` | Top of "Your band, explained": what the band rests on, as bars | 804 x 1280 | `Your band, explained: bars for practised and secure, higher-only work, explain questions and paper practised.` |

Where each one goes:

- Hero: `home-light` / `home-dark`.
- How a lesson works, step 1: `question-light` / `question-dark`, cropped to the top.
- Step 2: `why-light` / `why-dark`, cropped to the bottom (the green panel).
- Step 3: `home-locked-light` / `home-locked-dark`, cropped to the Today card.
- Drawings section: `coil-light` / `coil-dark`, cropped to the drawing.
- Grade band section: `band-light` / `band-dark`, and a crop of the Grade band card from `home-locked-light` / `home-locked-dark`.
- Light or dark section (new, replaces Screens): `home-light` beside `home-dark`, each shown in its own theme whatever the page theme.
- Open Graph image: rebuild with `home-light` in the new frame (section 3).

The six older files: `home-grade-band.webp` and `topics.webp` are no longer placed on the page (see section 9 for why Topics goes), and the other four are replaced by their new pairs. Delete all six from `assets/screens/` on the build branch so the site stays light; they remain in this branch's history. The two unused new captures (a resting coil, and a Topics pair) were left out on purpose.

The rule from section 4 of `SITE-BRIEF.md` still holds: never place an image of the app that was not captured from the real app, and crop only with CSS, never by editing the files (the band crop above is the one exception, made once so the specification points never reach the site).

---

## 2. Dark captures in dark mode

Every phone on the page shows the light capture even when the page is dark, so in dark mode the site is a black page with bright white slabs on it. That single mismatch is the biggest reason the dark site looks like a template and the light one looks like a draft.

Change: every screenshot becomes a `<picture>` that swaps with the page theme.

```html
<picture>
  <source srcset="assets/screens/home-dark.webp" media="(prefers-color-scheme: dark)">
  <img src="assets/screens/home-light.webp" width="402" height="874" alt="…">
</picture>
```

Keep `width`, `height`, `alt`, `loading="lazy"` and `fetchpriority="high"` on the `<img>` exactly as now. The only exception is the Light or dark section (section 9), where each phone is fixed to its own theme and does not swap.

Why it reads as premium: the page and the product agree. A student who keeps their phone dark sees the app they would get.

---

## 3. The phone frame

Now: a 5px solid `--ink` border with a percentage radius, no bezel, no shadow, no depth. It reads as a wireframe, and in dark mode as a grey outline round a white box.

Change: one `.phone` component, drawn in CSS, used everywhere a whole phone appears.

```css
.phone-wrap { container-type: inline-size; }
.phone {
  position: relative;
  padding: 10px;                              /* the bezel */
  background: var(--frame);                   /* light: --ink; dark: --line2, as now */
  border-radius: 44px;                        /* fallback */
  border-radius: 12cqw;                       /* circular corners at any width */
  box-shadow:
    inset 0 0 0 1.5px rgba(255, 255, 255, 0.10),   /* a lip on the bezel */
    0 32px 64px -32px rgba(43, 43, 43, 0.40),      /* long soft shadow */
    0 12px 24px -16px rgba(43, 43, 43, 0.25);      /* short contact shadow */
}
.phone > picture, .phone > img { display: block; border-radius: calc(12cqw - 10px); overflow: hidden; }
.phone img { width: 100%; height: auto; }
@media (prefers-color-scheme: dark) {
  .phone { box-shadow: inset 0 0 0 1.5px rgba(255, 255, 255, 0.06), 0 32px 64px -32px rgba(0, 0, 0, 0.80), 0 12px 24px -16px rgba(0, 0, 0, 0.60); }
}
```

Rules:

- The shadows are the ink colour (`#2B2B2B`) or black at low opacity, not a new hue. That is the only place the site uses transparency, and it is allowed for shadows only.
- No notch, no camera, no side buttons, no brand hardware: a plain rounded slab is honest and does not imitate anyone's device.
- Wrap each `.phone` in a `.phone-wrap` that sets the width (the hero, feature and pair widths below). The container unit `cqw` needs that wrapper; the 44px fallback covers old browsers.
- The screenshots have square corners, so the inner radius on `picture` or `img` is what makes them look like a screen. Do not round the files.
- Drop `.phone.short`: the band sheet gets the same frame, cut at the bottom by its panel (section 7).

Why it reads as premium: a bezel with a lip and a two-part shadow is what every good app site does to put a screen on a page; a flat black stroke is what a wireframe tool does.

---

## 4. The hero

Now: text, then a whole phone on a flat page. On a phone the first screen is words only; the product arrives after a scroll. On a desktop the phone is a small outlined box in a wide empty column.

Change, in order:

1. Put a panel behind the hero: a rounded block in `--violet-soft` (radius 32px), inside `.wrap`, padding 40px 24px on a phone and 64px inside on a desktop. The app's own Today card is this colour, so the page opens on the app's own ground.
2. The phone rises out of the panel. Set `.hero-panel { overflow: hidden }` and let the phone's bottom run past the panel's bottom edge: on a phone show the top 560px of the phone (`.hero-phone { height: 560px }` with the frame inside it, `margin-bottom: -1px`), on a desktop the top 640px. The frame keeps its rounded top; its bottom is simply cut by the panel. This is the Superpower pattern from `SITE-BRIEF.md` section 6, and it means the product is on the first screen of every phone.
3. Hero phone width: 300px on a phone (as now), 400px on a desktop. Desktop columns `1.1fr 1fr`, gap 48px, phone column `justify-self: end` so the phone sits against the panel's right padding.
4. Headline: `clamp(40px, 7.5vw, 64px)`, line-height 1.05, letter-spacing -0.025em, weight 800, `text-wrap: balance`. Keep headline A. Lede: 19px, line-height 1.5, `--ink2`, max-width 28em.
5. The status chip is styled like a button and does nothing. Make it a status line: no icon, 15px, weight 800, `--violet-ink` on `--violet-soft`, padding 6px 14px, and a 8px dot in `--violet` before the words (`::before`, `border-radius: 999px`). A dot reads as status; a phone icon in a pill reads as a link.
6. Under the chip, one line of small print in `--muted` 14px: `For AQA, Edexcel, OCR A and OCR B. Separate and combined science. Foundation and Higher.` This is the two-second "it fits me" check, so it belongs on the first screen, and it lets the "Who it is for" panel move down and change shape (section 8).
7. Motion: see section 11. The hero is the only place with an entrance animation.
8. On a phone, left-align the hero text (eyebrow, headline, lede, chip, small print) and left-align every section below it. Centred hero text over a left-aligned page is the alignment clash the page has now. On a desktop the hero is already left; keep it.

Why it reads as premium: depth (panel, bezel, shadow), the product in the first frame, and one status line instead of a fake button.

---

## 5. Section rhythm and alignment

Now: headings are centred in "How a lesson works", "What else it does" and "Screens", and left in "Drawings", "An honest grade band" and "Questions". The gap between sections is the same 64px whether a section is a quiet list or a large tinted panel.

Change:

1. Every section opens with the same head: eyebrow (12px, uppercase, `--violet-ink`), then `h2`, then an optional one-line lede in `--ink2`. Gaps 12px inside the head, 40px from the head to the content. Left-aligned on a phone; on a desktop the same, except sections whose content is a centred pair (section 9), which centre the head too.
2. Eyebrows, in order down the page: `HOW A LESSON WORKS` (h2: `Answer. See why. Come back.`), `DRAWINGS YOU CAN MOVE` (h2 as now), `THE GRADE BAND` (h2 as now), `YOUR OWN COURSE` (the moved "Who it is for", section 8), `WHAT ELSE IT DOES` (h2: `The rest, in one look`), `LIGHT OR DARK` (h2: `Follows your phone`), `QUESTIONS` (h2 as now).
3. Section spacing: `--section: 72px` on a phone, `120px` on a desktop, applied as `padding-block` split half and half as now. Tinted panels (hero, band) get the full gap; do not let two tinted panels touch.
4. `h2`: `clamp(28px, 4.5vw, 40px)`, line-height 1.15, letter-spacing -0.02em. Card and step titles: 20px, weight 800, letter-spacing -0.01em (700 at 20px is too close to body weight to read as a title next to 17px body). Step titles 22px.
5. Page length on a phone: the build measures 7,987px at 402 wide, about nine screens. After sections 4, 6, 7, 9 and 10 it should be under 5,500px. Measure it (`document.documentElement.scrollHeight` at 402 wide) and put the number in the pull request.

Why it reads as premium: one head pattern, one alignment, one rhythm. The eye learns the page in the first two sections and stops working after that.

---

## 6. How a lesson works: three equal windows

Now: three cards whose crops are different heights, bottom-aligned, so card 3 has a blank band above its crop on a desktop. The crops have the same heavy 5px border as the phones and a 20px radius, so they look like a third kind of object.

Change:

1. All three crops share one box: `aspect-ratio: 402 / 380`, `border-radius: 16px`, `overflow: hidden`, no border, no shadow. The screenshot's own page colour (`#F4F3F0` light, `#121211` dark) sits on the white card and gives the window its edge; that is the "no divider lines" rule doing the work.
2. Object positions: step 1 `50% 0%` (question and field drawing); step 2 `50% 100%` (the green Why? panel and Continue); step 3 about `50% 33%` on `home-locked` so the TODAY eyebrow sits 12px from the top and the Start button is inside the window. Adjust by eye at 402 wide in both themes.
3. Card padding 24px, gap 8px, crop `margin-top: 20px`, `align-self: end` stays. With equal aspect ratios the three windows line up on a desktop and the blank band goes.
4. Step numbers: keep the 36px `--violet-edge` disc, white numeral.

Why it reads as premium: three identical windows onto three moments of one lesson. Equal boxes are what makes a "how it works" row read as a sequence rather than three cards.

---

## 7. Feature sections: show the part, not the whole phone

Now: the Drawings section shows the entire coil screen, 610px tall on a phone, two thirds of it empty page below the drawing. The band section shows the whole sheet.

Change:

1. Drawings: put the phone in a `--soft` panel (radius 26px, `overflow: hidden`) with the phone rising from the panel's bottom edge exactly as in the hero, and crop the visible part to the top 520px of the phone at 300px wide (question text and the whole drawing with the S N pills; the empty part of the screen never shows). On a desktop, text left and the panel right with the phone at 320px wide showing its top 560px.
2. Grade band: keep the `--violet-soft` panel. Inside it, two things side by side on a desktop and stacked on a phone: the `band` sheet in the phone frame, rising from the panel bottom, showing its top 480px (the title, the sentence, and the first three bars); and beside it a plain window (same style as section 6, `aspect-ratio: 402 / 300`) onto the Grade band card of `home-locked` (`object-position: 50% 62%`, adjust so the four rings and "1 of 4 unlocked" fill it). Caption under the window in `--muted` 14px: `Before there is enough practice, Home says what is still needed instead of guessing.` This is the honesty claim shown, not just said.
3. Text columns in both: eyebrow, h2, one paragraph, as now. Paragraph max-width 30em.

Why it reads as premium: a crop says "look at this"; a whole phone says "here is a phone". The page also loses about 900px on a phone.

---

## 8. Who it is for: move it down and label it

Now: a large white card second on the page, a full sentence as its heading, chips in three centred rows that make a ragged pyramid on a phone, and a fourth card in "What else it does" ("Your own course") saying the same thing again.

Change:

1. Move the section to after the grade band, with the eyebrow `YOUR OWN COURSE` and h2 `Set once, in your board's own words`. Lede: `Choose your board, course and tier the first time you open the app. Every lesson, keyword and practical name is then the one your own exam uses.`
2. Show the choices as three labelled rows, each a label in eyebrow style over (on a phone) or beside (on a desktop, label column 120px) a single row of chips: `BOARD` AQA · Edexcel · OCR A · OCR B; `COURSE` Separate science · Combined science; `TIER` Foundation · Higher. Chips left-aligned, 8px gap, `flex-wrap: wrap`. Give these chips their own class (`.pick`), not the hero's status class: `--soft` ground, `--ink` text, weight 700, 15px, padding 8px 14px. They are options, not a status.
3. Keep the small print `Upthrust is independent and is not endorsed by any exam board.` under the rows.
4. Remove the "Your own course" card from "What else it does" (it is now this section). That list becomes five items.

Why it reads as premium: it looks like the app's own Settings, which is exactly what it describes, and the page no longer says the same thing twice.

---

## 9. Replace the Screens gallery with Light or dark

Now: five whole phones in a row. On a desktop each is about 200px wide, so the screen text is 6px and unreadable; four of the five screens already appeared higher up the page; the Topics screen shows a lesson count, which `SITE-BRIEF.md` section 1 asks the site not to quote because it differs by board and changes.

Change:

1. Delete the Screens section, its `role="region"` scroller and its captions.
2. In its place, a section with eyebrow `LIGHT OR DARK`, h2 `Follows your phone`, lede `Or choose light or dark in Settings.` Content: two phones side by side, `home-light` on the left always light and `home-dark` on the right always dark (plain `<img>`, no `<picture>`, because the point is to show both at once). On a desktop 300px each, 32px apart, centred, each rising from a `--soft` panel that cuts them at 520px. On a phone the two sit side by side at 47% width each in the same panel, cut at 300px, so the header, the two stat cards and the band card are visible on both; they are illustrations of the theme and are not meant to be read. Alt text: `The Home screen in the light theme.` and `The Home screen in the dark theme.`
3. This section is the one whose head is centred on a desktop (section 5, rule 1), because its content is a centred pair.

Why it reads as premium: it shows something not yet shown, at a size that can be seen, and it stops the page repeating itself.

---

## 10. What else it does: rows on a phone, grid on a desktop

Now: six tall cards stacked on a phone, each with a 28px icon on its own line, about 260px each, 1,560px in all for six short lines of text.

Change:

1. Five items after section 8: Instant feedback, Spaced practice, Your exam dates, No account, Stays on your phone. Add one: `Paper by paper` / `Topics are grouped by your exam papers, with the days to each.` (this replaces the Topics screenshot). That makes six again, so the desktop grid stays 3 x 2.
2. On a phone, each card is a row: the icon (28px, `--teal`) left, title and line right, 16px gap, padding 16px 20px. About 84px a row.
3. From 600px wide, the grid as now (two columns, then three from 900px), icon above the title.
4. Icons: keep the drawn line icons. Make them 28px in `--teal` with a 44px `--soft` disc behind each (radius 999px), so the icon has weight on the card.

Why it reads as premium: dense where it should be dense. A feature list is a list, not six posters.

---

## 11. Motion, small and CSS only

Now: none. The page does not move at all, and the FAQ snaps open.

Change (all inside `@media (prefers-reduced-motion: no-preference)`; the existing reduced-motion rule already turns animation and transitions off):

1. Hero entrance, once, on load: eyebrow, headline, lede, chip and small print fade up 12px over 500ms with `ease-out`, staggered 60ms apart using `animation-delay` on `:nth-child`; the phone fades up 20px over 700ms starting at 200ms. Nothing else on the page animates on load.
2. Cards and FAQ rows: `transition: transform 180ms ease, box-shadow 180ms ease`; on `:hover` only under `@media (hover: hover)`, `transform: translateY(-2px)` and the short contact shadow from section 3. No hover on a phone.
3. FAQ: the plus in `summary::after` becomes two bars that rotate 45 degrees when open (`transition: transform 200ms`), instead of the second bar disappearing. The answer fades in: `details[open] .answer { animation: fade 200ms ease-out }` from opacity 0 and `translateY(-4px)`.
4. Links: underline thickness already changes on hover; add `transition: text-decoration-thickness 120ms`.
5. No scroll-jacking, no parallax, no autoplay, nothing pinned. If you add scroll-linked reveals with `animation-timeline: view()`, wrap them in `@supports (animation-timeline: view())` and keep them to opacity and 12px of travel.

Why it reads as premium: the page acknowledges the visitor without performing for them.

---

## 12. Header on a phone

Now: the three links wrap under the wordmark as a second row of 16px bold text. It looks like a mobile menu that failed to collapse.

Change: one row at every width. On a phone, hide `How it works` (`display: none` under 600px; the section is one scroll away) and show `Privacy` and `Support` right-aligned at 15px, weight 700, `--ink2`, min-height 44px. Wordmark 32px mark and 20px word on a phone, 36px and 22px from 600px. Header padding 12px 0 on a phone. Still nothing pinned.

---

## 13. FAQ, closing block, footer, inner pages

1. FAQ: summary 17px weight 700, min-height 56px, padding 16px 20px; answer 16px `--ink2`, padding 0 20px 20px, max-width 34em. The plus disc 32px. One open at a time stays (`name="faq"`).
2. Closing block: keep the wordmark and the status chip (the section 4 style). Add one line between them in `--ink2` 17px: `Written by a physics teacher, for students in England.` This fact is in `SITE-BRIEF.md` section 1 and is allowed in exactly this form. No name, no button.
3. Footer: unchanged.
4. Support page: the three topic cards are uneven because `Getting started` wraps. Set `.topics a { white-space: nowrap; justify-content: center }` and let the grid be `repeat(auto-fit, minmax(160px, 1fr))`.
5. Privacy page: keep. Give the "At a glance" table's caption the section-head style (eyebrow above it: `AT A GLANCE`), and give the short-version card the same 32px radius as the hero panel so the two pages share one shape.
6. 404: unchanged.
7. Open Graph image: rebuild `assets/og.png` with the new frame and `home-light`, wordmark, headline A, nothing else, in the site's own colours.

---

## 14. Before you open the pull request

Everything in `SITE-BRIEF.md` section 10, plus:

1. Both themes checked at 402 and 1280 wide on the branch preview, and at 320 wide with no sideways scroll.
2. Page height at 402 wide under 5,500px; put the number in the pull request.
3. Every `<picture>` swaps in dark mode; the Light or dark pair does not.
4. No request leaves the site (fonts, images, CSS all relative).
5. Lighthouse mobile still 95 or more on every page; the new images add about 400KB across the site but the landing page's first load (fonts, CSS, hero image) must stay under 400KB.
6. `assets/screens/` holds only the twelve files in section 1; the six older files are deleted on the build branch.
7. `git config user.email` is the no-reply address; `CNAME` untouched; no em dashes (`grep -rn "$(printf '\342\200\224')" --exclude-dir=.git .` prints nothing).
8. Open decisions for the owner, in the pull request, recommended answer first: whether the hero small print naming the boards may sit on the first screen (recommended yes; it is plain fact); whether the closing line `Written by a physics teacher, for students in England.` is wanted (recommended yes); whether to keep the Grade band "before it unlocks" window (recommended yes).
