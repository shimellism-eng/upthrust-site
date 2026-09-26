# Upthrust website: build brief

For the session that builds upthrust.app. Read all of it before writing anything.

This file lives in `_brief/`. The underscore keeps it off the live site, because GitHub Pages runs Jekyll on this repository and Jekyll does not publish folders whose names start with `_`. The repository has no `.nojekyll` file. **Do not add one**: if you ever need it, move this folder out of the repository first.

---

## 0. Rules for the builder (follow exactly)

- Commit only as `232254431+shimellism-eng@users.noreply.github.com`. Run `git config user.email` and `git config user.name` first, and set them if they are not already `232254431+shimellism-eng@users.noreply.github.com` and `shimellism-eng`.
- Never edit `CNAME` or any GitHub Pages or repository setting.
- Never push to `main` (main is live). Work on branch `site-v1` and open a pull request.
- Make a preview the owner can tap on a phone before anything is merged.
- No prices, selling, sign-ups or personal names.

Also:

- Start `site-v1` from `origin/site-brief`, so it already has this brief and the screenshots. Open the pull request from `site-v1` into `main` and leave it open: the owner merges, nobody else.
- Preview: GitHub Pages only serves `main`, so give the owner a branch preview he can open on his phone, for example `https://raw.githack.com/shimellism-eng/upthrust-site/site-v1/index.html`. For that to work, **every link and asset path must be relative** (`privacy/`, `assets/css/site.css`), never starting with `/`. Put the preview link at the top of the pull request description. Check it on a real phone width before handing over.
- No email collection, no forms, no newsletter, no waiting list, no log in, no accounts, no "Get started" button.
- No analytics, no cookies, no tracking pixels, no third-party scripts, no embeds. The privacy page promises this, so it must be true.
- No logos of exam boards, Apple or Google. The four boards may be named as plain facts ("written for AQA, Edexcel, OCR A and OCR B"). Never say or imply any board endorses the app.
- The app shows an estimate, never a grade prediction. The site must never promise grades, results or improvement ("boost your grade", "guaranteed") in any form.
- British English. No em dashes anywhere, in copy or in code comments. Use a colon, a comma or a full stop instead.
- All copy below is a **draft for the owner to approve**. Do not add claims about the app that are not in this brief. If you need a fact that is not here, leave a visible `TODO(owner)` in the pull request description, not on the page.
- Behaviour and structure may be borrowed from the reference sites below. Their look, wording and images never. Do not download or commit any image from Mobbin or any other site.
- The current `index.html` is the live holding page. Replace it only on `site-v1`, never directly on `main`.

---

## 1. What the product is (facts you may use)

Upthrust is a GCSE Physics revision app for students in England.

- Written for all four exam boards (AQA, Edexcel, OCR A, OCR B), for separate and combined science, Foundation and Higher tier. Each student chooses their board, course and tier once, and every lesson, keyword and practical name is then in their own board's words.
- Lessons are short sequences of interactive questions: choices, numbers on a keypad, sorting, ordering, labelling, building a longer answer. Every answer gets instant feedback, and a **Why?** that explains the physics.
- Drawings are worked out from the physics, not pasted in: field lines, circuits, forces, rays, waves. Some are animations the student drives, such as pushing a magnet into a coil and watching the meter needle swing.
- Questions from earlier lessons come back on later days, so what was learned is practised again before it fades.
- A grade band, shown as an **estimate from practice, never a prediction**. It only appears once there is enough practice to base it on, it says what it rests on, and it says what would move it up.
- Three tabs: Home, Topics, Settings. Light and dark themes (dark follows the phone, or can be chosen).
- No account. Everything is kept on the phone. Nothing is sent anywhere.
- Coming to iPhone and Android. There is no release date to publish yet.
- Written by a physics teacher. (Say it this way. No name.)

Do not quote lesson or topic counts on the site: they differ by board, course and tier and they change as lessons are added.

---

## 2. Site map and files

```
index.html              landing page
privacy/index.html      privacy policy        (upthrust.app/privacy/)
support/index.html      support               (upthrust.app/support/)
404.html                small "page not found" with a link home
assets/css/site.css     one stylesheet, shared
assets/fonts/           Nunito, self-hosted (see section 5)
assets/screens/         the app screenshots (already here)
CNAME                   do not touch
_brief/                 this brief, not published
```

Plain HTML and CSS. No framework, no build step, no JavaScript needed. If you add any script, it must be tiny, inline, optional (the page works fully without it) and do nothing that touches the network.

Every page has the same header (wordmark, then links to Privacy and Support, and on the landing page "How it works") and the same footer. The header scrolls away with the page: **nothing is pinned** (no sticky header, no floating button).

---

## 3. Page by page

### 3.1 Landing page (`index.html`)

Section order, with the purpose of each and draft copy. Headings are sentence case.

**1. Header.** Wordmark (the violet rounded square with the white upward arrow from the current holding page, and "Upthrust" in Nunito ExtraBold). Links: How it works, Privacy, Support. On a phone, show them as plain text links on one row; no hamburger menu is needed for three links.

**2. Hero.** Purpose: say what it is in one breath, show the real app straight away.
- Eyebrow: `GCSE Physics revision app`
- Headline, pick one with the owner (recommended first):
  - A. `Physics revision that shows you why.`
  - B. `GCSE Physics, one question at a time.`
  - C. `Answer. See why. Come back stronger.`
- Lede: `Short interactive lessons written for your exam board, your course and your tier. Every answer gets instant feedback and a clear "Why?".`
- Status chip (not a button, not a link): `Coming soon to iPhone and Android`
- Image: one phone, `home-grade-band.webp`, centred under the text on a phone, to the right of the text on a wide screen.
- Do **not** use the official App Store or Google Play badges: they are for apps that are live and must link to the listing. A plain text chip is honest and needs no artwork.

**3. Who it is for.** Purpose: a student sees in two seconds that it fits them. One short line and three rows of plain text chips, no logos:
- Line: `Written for your own exam, in your board's own words.`
- Chips: `AQA` `Edexcel` `OCR A` `OCR B` / `Separate science` `Combined science` / `Foundation` `Higher`
- Small print under it: `Upthrust is independent and is not endorsed by any exam board.`

**4. How a lesson works** (`id="how-it-works"`). Purpose: show the loop, answer, understand, return. Three numbered cards, each with a cropped phone screen (top of the screen only, so the text stays large):
1. `Answer a question` / `Tap, type or drag. Many questions come with a drawing worked out from the physics.` Screen: `question-magnetic-field.webp`.
2. `See why` / `You find out straight away if you were right, and a Why? explains the physics behind the answer, right or wrong.` Screen: `why-explanation.webp` (crop to the green panel).
3. `Come back to it` / `Questions from earlier lessons return on later days, before they fade.` Screen: `home-grade-band.webp` cropped to the Today card, or `topics.webp`.

**5. Drawings you can move.** Purpose: the thing competitors do not have. A feature list beside one screen. Draft:
- Heading: `Drawings worked out from the physics`
- Body: `Field lines, circuits, forces and waves are drawn from the physics itself, so an arrow twice as long means twice the force. Some you move yourself: push a magnet into a coil and watch the needle swing.`
- Screen: `magnet-into-coil.webp`, with `question-magnetic-field.webp` as the second if you use a switcher.

**6. An honest grade band.** Purpose: trust. Draft:
- Heading: `An estimate, never a prediction`
- Body: `Once you have practised enough, Home shows the grades you are working at, from your own answers. It tells you what the band rests on and what would move it up. Until then it says so, rather than guessing.`
- Screen: `band-explained.webp` (already cropped).

**7. What else it does.** Purpose: scannable extras. A grid of six small cards (icon, bold title, one or two lines):
- `Your own course` / `Board, course and tier set once. Change them any time in Settings.`
- `Instant feedback` / `Know straight away if you were right, with the reason explained.`
- `Spaced practice` / `Questions from earlier lessons come back on later days.`
- `Your exam dates` / `Counts down to your physics papers, and you can set your own dates.`
- `No account` / `Open it and start. There is nothing to sign up for.`
- `Stays on your phone` / `Your answers never leave it. No adverts, no tracking.`

  `No adverts` is a claim: check it with the owner before publishing (`TODO(owner)` in the pull request).

**8. Screens.** Purpose: let people look around. A horizontal row of all five full phone screens with a short caption under each, scroll-snapping one at a time on a phone, all visible on a wide screen. Captions:
- Home: `Home, for a sample student. Every board sees its own course here.`
- Question: `A question with a drawing.`
- Why?: `The Why? after an answer.`
- Magnet and coil: `An animation you drive.`
- Topics: `Your topics, paper by paper.`

  The sample screens are from an AQA Higher student. Say "sample student" in the first caption so no Edexcel or OCR student feels it is not for them.

**9. Questions** (FAQ). Purpose: remove doubts. Accordion using `<details>` and `<summary>`. Drafts:
- `Which exam boards does it cover?` / `AQA, Edexcel, OCR A (Gateway) and OCR B (Twenty First Century), for GCSE Physics and the physics in combined science, Foundation and Higher.` (Owner to confirm the bracketed names.)
- `Do I need an account?` / `No. There is nothing to sign up for, and no email address is asked for.`
- `What does it know about me?` / `Only what you tell it on your own phone: your board, course and tier, and your answers. None of it leaves the phone.` Link to Privacy.
- `Is the grade band a prediction?` / `No. It is an estimate from your practice so far. It says what it rests on, and it only appears once there is enough practice to base it on.`
- `When can I get it?` / `It is coming to iPhone and Android. There is no date yet.`
- `Who writes it?` / `A physics teacher, question by question, from the exam boards' own specifications.`

  Do not add a question about price.

**10. Closing line.** A quiet final block: the wordmark, `Coming soon to iPhone and Android`, and nothing else. No button.

**11. Footer.** One quiet row: `Privacy` `Support`, then `© 2026 Upthrust`, then the small print `Not affiliated with or endorsed by AQA, Pearson Edexcel or OCR.` No social links.

### 3.2 Privacy policy (`privacy/index.html`)

Purpose: tell a 15-year-old and their parent, in plain words, that nothing is collected. The owner may want this reviewed before it goes live (see the note at the end of this section).

Structure:
1. Title `Privacy`, and `Last updated: [date of merge]`.
2. **The short version** (a highlighted card, first thing on the page): `Upthrust has no accounts and collects no personal data. Your progress is kept on your phone and is never sent anywhere. This website sets no cookies and uses no analytics.`
3. **At a glance** table (rows, two columns: what, and the answer):
   - Account or sign-up: `None`
   - Name, email, age, school, location: `Never asked for, never collected`
   - Your answers and progress: `Stored only on your phone`
   - Sent to us or anyone else: `Nothing`
   - Adverts or tracking: `None` (owner to confirm "adverts")
   - Cookies on this website: `None`
4. Contents list linking to the sections below (on a wide screen it may sit in a column beside the text; on a phone it sits at the top).
5. Sections:
   - **The app.** What it stores on the phone: the board, course and tier chosen; your answers, when you gave them and whether they were right; your progress through lessons; optional exam dates, target grade and sessions a week; the light or dark setting. Why: so the app can mark, bring questions back and estimate a grade band. None of it is sent anywhere. The app has no account, no server and no analytics.
   - **Deleting your data.** In Settings, "Start again" wipes your lessons and answers (your course stays). Deleting the app deletes everything it stored. Because nothing is kept anywhere else, there is nothing else to delete, and progress does not move to a new phone.
   - **Reporting a problem.** A "Report a problem" email option is planned but switched off. If it is switched on later, it will only open an email in your own mail app, with your course and the app version filled in, and nothing is sent unless you press Send yourself. This page will be updated first.
   - **This website.** No cookies, no analytics, no third-party scripts or fonts. The site is hosted by GitHub Pages; GitHub, as the host, may log visitors' IP addresses for security and operation. Link to GitHub's own privacy statement.
   - **Children.** The app is made for students aged about 14 to 16. It asks for no personal information and has no way to contact anyone.
   - **Changes.** If anything here changes, this page changes first, with a new date.
   - **Contact.** `TODO(owner)`: a contact route for privacy questions. Do not invent an address. The planned support address is not live yet (see 3.3), so until the owner confirms it, this section says: `A contact address will be added here before the app is released.`
6. Note for the owner (put this in the pull request, not on the page): *Before launch, have the policy checked against UK GDPR and the ICO's Children's code (Age Appropriate Design Code). App Store and Google Play will also ask for a privacy answer; "Data not collected" must match this page.*

### 3.3 Support (`support/index.html`)

Purpose: answer the common questions without a contact form.

Structure:
1. Title `Support`, one line: `Answers to the questions students ask most.`
2. Three small cards linking down the page: `Getting started`, `Your progress`, `Privacy`.
3. Grouped questions (`<details>` accordions, same component as the landing page):
   - Getting started: `How do I choose my board, course and tier?` (on first opening, and later in Settings) · `Can I change my tier or course later?` (yes, in Settings) · `Can I stop halfway through a lesson?` (yes: it picks up where you left off).
   - Your progress: `Where is my progress kept?` (on your phone only) · `I changed phone and my progress has gone` (it stays on the phone it was made on, because there is no account) · `How do I start again?` (Settings, Start again; your course stays) · `Why is there no grade band yet?` (it appears once there is enough practice across enough days and topics; Home says what is still needed) · `Can I set my own exam dates?` (yes, in Settings).
   - Privacy: short answer and a link to the privacy page.
   - Appearance: `Can I use dark mode?` (it follows your phone, or choose light or dark in Settings).
4. **Need more help?** `TODO(owner)`. The app has a planned support address on this domain that is **not live yet**. Do not publish any email address until the owner confirms it forwards somewhere a person reads. Until then: `A way to contact us will be added here before the app is released.`

### 3.4 404 page

One line (`This page does not exist.`), and a link back to the landing page. Same header and footer.

---

## 4. Screenshots (already in `assets/screens/`)

Real screens of the app, captured at phone size (402 points wide, light theme), from a sample student (AQA, separate physics, Higher) with made-up practice. Saved at 2x as WebP, 804 pixels wide. They carry no exam board source quotations.

| File | Shows | Size | Alt text |
|---|---|---|---|
| `home-grade-band.webp` | Home: days to Paper 1, days this week, "Working at 6 to 7" band with "Estimate, never a prediction", Today card | 804 x 1748 | `Upthrust Home screen: days to the first exam, practice this week, a grade band of 6 to 7 marked as an estimate, and today's questions.` |
| `question-magnetic-field.webp` | A question over a bar magnet's field lines, four answer options | 804 x 1748 | `A question asking where a bar magnet's field is strongest, with field lines drawn round the magnet and four marked points.` |
| `why-explanation.webp` | The same question answered right, with the Why? opened | 804 x 1748 | `The answer marked right, with a Why? panel explaining that the field is strongest at the poles.` |
| `magnet-into-coil.webp` | The student pushing a magnet into a coil, meter needle swung | 804 x 1748 | `An animation: a magnet being pushed into a coil of wire, with the meter's needle swinging.` |
| `topics.webp` | Topics tab: overall progress, topics grouped by paper, ticks and part-done rings | 804 x 1748 | `The Topics tab: lessons done so far and each topic grouped by exam paper.` |
| `band-explained.webp` | Top of "Your band, explained": what the band rests on, as bars | 804 x 1280 | `Your band, explained: bars for practised and secure, higher-only work, explain questions and paper practised.` |

How to use them:
- Always give `width` and `height` attributes (use 402 x 874, or 402 x 640 for `band-explained`) so nothing jumps while loading. `loading="lazy"` on every image except the hero.
- Put each in a simple drawn phone frame in CSS: a rounded rectangle (radius about 44px at full size) with a thin bezel in `--ink` (light) or `--line2` (dark). No device photographs, no Apple hardware mockups.
- In dark mode, keep the light screenshots (they are real) inside the frame. Dark-theme captures can be added later: note it in the pull request as owed, do not fake them.
- Cropping for the "How a lesson works" cards: crop with CSS (`object-fit: cover; object-position: top`) on a fixed-ratio box, never by editing the files.
- Never add another image of the app that was not captured from the real app.

---

## 5. Design system

The site must feel like the app. Use only these colours: no new ones.

### Colour tokens

Define as CSS custom properties on `:root`, swap under `@media (prefers-color-scheme: dark)`. Give `body` an explicit background.

| Token | Light | Dark | Use |
|---|---|---|---|
| `--page` | `#F4F3F0` | `#121211` | page background |
| `--card` | `#FFFFFF` | `#1B1B19` | cards, accordion rows |
| `--soft` | `#F2F1EE` | `#252523` | chips, quiet fills |
| `--ink` | `#2B2B2B` | `#EFEEEB` | headings, body |
| `--ink2` | `#58585D` | `#B4B2AC` | secondary text |
| `--muted` | `#6E6E73` | `#88867F` | captions, small print |
| `--line` | `#E7E5E0` | `#2C2C29` | card edges if needed |
| `--line2` | `#D6D3CC` | `#3E3D39` | phone frame in dark |
| `--violet` | `#8B5CF6` | `#9B7CFF` | brand fills, icons, focus ring |
| `--violet-edge` | `#6B3FDB` | `#6B4FD0` | deeper violet fill |
| `--violet-soft` | `#F3F0FE` | `#241F38` | tinted panels, chip ground |
| `--violet-ink` | `#6B3FDB` | `#C1ADFF` | **violet used as text** (links, eyebrows) |
| `--green` | `#58C65B` | `#4FC463` | a tick, sparingly |
| `--green-soft` | `#DEEFD6` | `#17291A` | the "right" panel, if echoed |
| `--green-ink` | `#2B722E` | `#7FDB8D` | green used as text |
| `--teal` | `#0E8A9E` | `#3FBDD1` | secondary accent: feature icons |
| `--teal-ink` | `#0A6274` | `#3FBDD1` | teal used as text |

Rules: violet is the identity, teal the second accent. Violet or teal **text** always uses the `-ink` token, never the fill token. Red is not needed on the site. White text only sits on `--violet-edge` or darker.

### Type

Nunito only, self-hosted as WOFF2 (latin subset) in weights 400, 600, 700 and 800, with `font-display: swap` and the SIL Open Font Licence file beside the fonts. Do **not** load it from Google Fonts: that would send every visitor's address to a third party and make the privacy page untrue. Fallback stack: `Nunito, "Avenir Next", system-ui, -apple-system, "Segoe UI", sans-serif`.

Scale (the app's own roles, scaled up for the web):

| Role | Size / line height | Weight | Notes |
|---|---|---|---|
| Hero headline | `clamp(34px, 8vw, 56px)` / 1.1 | 800 | letter-spacing -0.02em, `text-wrap: balance` |
| Section heading | `clamp(26px, 5vw, 36px)` / 1.2 | 800 | letter-spacing -0.015em |
| Card title | 20px / 1.3 | 700 | |
| Body | 17px / 1.6 | 400 | max line length about 34em |
| Lede | 19px / 1.55 | 400 | `--ink2` |
| Caption | 14px / 1.45 | 600 | `--muted` |
| Eyebrow | 12px / 1.35 | 800 | uppercase, letter-spacing 0.075em, `--violet-ink` |

Nothing smaller than 12px anywhere.

### Space and shape

- 4px grid: 4, 8, 12, 16, 20, 24, 32, 40, and 64 / 96 between landing sections on wide screens.
- Side gutter 20px on a phone; content max width about 1080px; text columns about 620px.
- Radius: 8 (small), 14 (chips, inputs), 20 (cards), 26 (large panels), 999 (pills).
- **No divider lines.** Separate things with space and card backgrounds, as the app does.
- Cards: `--card` on `--page`, radius 20, padding 20 to 24, no shadow or a very soft one.
- Chips: `--violet-soft` ground, `--violet-ink` text, radius 999, padding 8 x 16, weight 800.

### Icons

Simple line icons drawn inline in SVG (2px stroke, round caps), in `--teal` or `--violet`, 24 to 28px. Draw them; do not use an icon font or copy another product's icons.

---

## 6. Patterns to borrow (behaviour and structure only)

Each reference is on Mobbin. Borrow how it is arranged and how it behaves. Never its look, wording, illustration or images.

Hero
- Superpower, headline over one centred phone: https://mobbin.com/sites/sections/a66c7229-39c5-4f24-b34c-c09db551575d . Why it works: the product is the picture; one screen, no clutter. Use for the hero on a phone.
- Duolingo, short centred headline with the store row directly under it: https://mobbin.com/sites/sections/55f5773f-00e6-4a59-b2fe-dec6be97b22b . Why: the availability line sits where the eye already is. Our version is a text chip, not badges.
- Sana, several phones with a short paragraph and one availability line under them: https://mobbin.com/sites/sections/cf567c70-dd59-4cc6-99c9-a8d4e761bb55 . Why: works as the closing block or a wide-screen hero.

How it works
- Norma, three numbered cards, each with a cropped phone screen under a two-line explanation: https://mobbin.com/sites/sections/96f4183b-7eb5-437c-90ad-95d1306d320c . Why: the step number, the words and the real screen are read together; cropping keeps the text large. The best fit for "Answer, see why, come back".
- Airtasker, three steps as coloured tiles with a screen fragment inside and the caption beneath: https://mobbin.com/sites/sections/f826ae26-068d-4c62-a1a2-b7ee79a8ecbf . Why: shows only the part of the screen that matters.

Feature beside a screen
- Brilliant, a list of options beside one screen; choosing an option expands its text and changes the screen: https://mobbin.com/sites/sections/d54039d0-4bec-4308-a907-dc5d6d5e5be3 and https://mobbin.com/sites/sections/d260bf70-9ba7-479f-aef6-0efd036af6bd . Why: several features share one phone. On our site, build it without JavaScript first (stacked, each feature with its own screen on a phone); a switcher on wide screens is optional.

Feature grid
- Aboard, six cards in a 3 x 2 grid, small icon, bold title, two lines: https://mobbin.com/sites/sections/2385f307-1f61-4ae2-86ba-82c4456f1573 . Why: easy to scan, equal weight. One column on a phone, two on a tablet, three on desktop.
- Maze, four features in a single calm row with inline icons: https://mobbin.com/sites/sections/651ccfc2-deab-403f-9b8a-5b8f99e5753c . Why: lighter alternative if six cards feel heavy.

Screens gallery
- Wise, a row of phones with a bold caption and one line under each: https://mobbin.com/sites/sections/d8665778-9048-4363-9658-f35c691b75fa . Why: each screen is explained by its caption. On a phone make it a horizontal row with `scroll-snap-type: x mandatory`, with the next phone peeking in at the edge so it is obvious it scrolls.

FAQ
- Pangram, each question in its own rounded card with a plus that turns to a minus, one open at a time: https://mobbin.com/sites/sections/962b30a4-f4ca-49c0-8ee7-4047b75170b1 . Why: each question is a clear tap target, and the open answer sits in the same card as its question. Build it with `<details>` and `<summary>` so it works without JavaScript and with a screen reader.
- OpenPhone, big heading, one line pointing to more help, then the questions: https://mobbin.com/sites/sections/16077091-516c-4e22-b6d2-c6ad86b01432 . Why: the "cannot find it?" line lowers anxiety.

Footer
- VanMoof, one quiet row of legal links along the bottom: https://mobbin.com/sites/sections/6c8e5010-32b5-41ce-b912-2b5e64332568 . Why: we have only two pages to link, so a single row is right; no multi-column footer.

Privacy page
- Pi, a plain "snapshot" table before the full policy: https://mobbin.com/screens/43cb60c7-1579-4c98-9406-f7f99588f613 . Why: the answer ("nothing") is visible before any legal text.
- MasterClass, a contents list in a column beside the policy, with the effective date under the title: https://mobbin.com/screens/59ce80a7-3445-40cc-a1d5-5f32d8125987 . Why: easy to jump to one section; on a phone put the contents at the top instead.
- Fabric, a short statement of principles as bullets: https://mobbin.com/screens/1ec13580-1ac0-4ab7-a878-b174959ad6df . Why: plain promises read better than clauses.

Support page
- n8n, a row of topic cards, then common questions, then a "need more help?" block: https://mobbin.com/screens/9f7321b8-dc75-4c9c-8df2-a42a85ea34f8 . Why: the order matches how people look for help: browse, then read, then contact.

---

## 7. Accessibility (target: WCAG 2.2 AA, checked, not assumed)

- `lang="en-GB"` on every page. One `h1` per page, headings in order.
- A "Skip to content" link as the first focusable element.
- Contrast: body text `--ink` or `--ink2`; `--muted` only for captions and small print (it measures 4.57:1 on the light page, just over the bar, so never lighter). Violet and teal words always use the `-ink` tokens.
- Visible focus on every link and `summary`: a 2px `--violet` outline with a 2px offset. Never remove outlines.
- Tap targets at least 44 x 44px, including accordion rows and footer links.
- Every screenshot has the alt text given in section 4. Decorative icons get `aria-hidden="true"`.
- The screens row must be usable by keyboard (it is a scrollable region: give it `tabindex="0"`, `role="region"` and an `aria-label`).
- `prefers-reduced-motion`: no animation or smooth scrolling when it is set. Keep any motion small anyway.
- Text must still work at 200% zoom and at 320px wide, with no sideways scrolling of the page.
- Check both themes with the browser's dark mode on and off.

## 8. Performance (target: fast on a school-bus 4G phone)

- Lighthouse on mobile: 95 or more in Performance, Accessibility, Best practices and SEO, on every page.
- First load of the landing page under 400 KB in total, including fonts and the hero image.
- Largest contentful paint under 2 seconds on simulated 4G. The hero image is the only eagerly loaded image; give it `fetchpriority="high"`.
- One CSS file, no JavaScript, fonts self-hosted and preloaded (the 400 and 800 weights only; the others may load normally).
- No layout shift: every image has width and height; the font fallback is close to Nunito's metrics (`size-adjust` if needed).

## 9. Page metadata

- `<title>`: `Upthrust: GCSE Physics revision app` (landing), `Privacy · Upthrust`, `Support · Upthrust`.
- Meta description (landing, draft): `A GCSE Physics revision app for AQA, Edexcel, OCR A and OCR B: short interactive lessons with instant feedback and a clear "Why?". Coming soon to iPhone and Android.`
- Favicon: the existing violet rounded square with the white arrow (reuse the inline SVG from the holding page), plus a 180px `apple-touch-icon` drawn from the same shape.
- `theme-color` meta for light (`#F4F3F0`) and dark (`#121211`).
- An Open Graph image (1200 x 630) built only from the wordmark, the headline and one of the screenshots in section 4, in the site's own colours. No other imagery.
- No canonical URL or sitemap that points anywhere but `https://upthrust.app/`.

## 10. Before you open the pull request

1. Run `git config user.email` and confirm `232254431+shimellism-eng@users.noreply.github.com`.
2. `CNAME` is unchanged (`git diff origin/main -- CNAME` prints nothing).
3. No page contains a price, "free", "sign up", "log in", a form, an email address, a person's name, or an exam board logo.
4. No em dashes anywhere: `grep -rn "$(printf '\342\200\224')" --exclude-dir=.git .` prints nothing.
5. No request leaves `upthrust.app` when a page loads (check the browser's network panel: fonts, images and CSS all come from the site itself).
6. Every link works on the branch preview, on a phone, in light and dark.
7. The pull request description starts with the phone preview link, then lists every `TODO(owner)` decision as a short numbered list, recommended answer first.

Open decisions for the owner (copy these into the pull request):
1. Which headline (A recommended).
2. Can the site say "no adverts"?
3. The exam boards' qualification names in the FAQ (Gateway, Twenty First Century).
4. When the support address is live, and whether it also serves privacy questions.
5. Whether to have the privacy policy reviewed before launch (recommended).
6. Dark-theme screenshots: add later, or ship with light ones framed.
