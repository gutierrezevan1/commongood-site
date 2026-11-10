# CommonGood website

The CommonGood landing page: one hand-coded page (HTML + CSS, a few lines of JavaScript), with no framework or build step. It follows the designer's Figma file at desktop (1440px), tablet (1024px) and phone (375px) widths.

```
index.html          the page: all copy lives here
css/styles.css      all styling (colors and sizes are variables at the top)
js/main.js          phone menu toggle
assets/brand/       CommonGood and Curava logos
assets/logos/       partner logos (white, for the taupe panel)
assets/team/        headshots
```

## Previewing

Open `index.html` in a browser. Or, from this folder, run `python3 -m http.server` and visit http://localhost:8000.

## Still to fill in

Search `index.html` for `data-todo` and for text in [square brackets]:

| What | Where |
| --- | --- |
| Curava link | "See how Curava works" button (`data-todo="curava-url"`) |
| Newest Substack post: date, read time, title, summary, link | Latest Thinking card (`data-todo="substack-post"`) |
| Substack subscribe link | Subscribe button, and Substack in the footer |
| Contact email | Footer button: use `href="mailto:you@commongooded.com"` and change the button text if you like |
| LinkedIn, Instagram URLs | Footer |
| Roane's one-line bio | Team section |

## Swapping in photos

Each headshot is a `<div class="person__photo person__photo--placeholder">`. Replace it with:

```html
<img class="person__photo" src="assets/team/evan-gutierrez.jpg" alt="Evan Gutiérrez" width="448" height="520" loading="lazy">
```

Use black-and-white photos at least 900 × 1040px, so they look sharp on high-resolution screens. Photos are cropped to a 448 × 520 frame (343 × 400 on phones) automatically. Stephanie's current photo came from the Figma file at 448 × 520, so swap in the original file when you have it.

## Swapping in illustrations

Each illustration spot is a dashed placeholder: `<div class="illo illo--placeholder …" data-label="…">`. Keep the other class names and replace the element with an image:

```html
<img class="illo hero__illo" src="assets/illustrations/pointing.svg" alt="" aria-hidden="true">
```

Use transparent PNG or SVG files with the lines in Ink (#292522). The slot sets the width, so keep each image roughly the same proportions as its placeholder: hero 281×120, about 500×282, team 449×164, Curava 233×85, thinking 236×157.

### Animated illustration (About section)

For a looping video, provide two files: a transparent `.webm` for Chrome, Edge and Firefox, and an `.mp4` on a white background for Safari. Then:

```html
<div class="illo about__illo">
  <video autoplay muted loop playsinline poster="assets/illustrations/magnifier.png" aria-hidden="true">
    <source src="assets/illustrations/magnifier.webm" type='video/webm; codecs="vp9"'>
    <source src="assets/illustrations/magnifier.mp4" type="video/mp4">
  </video>
</div>
```

Add `.about__illo video[src$=".mp4"], .about__illo video { mix-blend-mode: multiply; }` to hide the white background in Safari. Also add a `prefers-reduced-motion` rule that pauses the video, or swaps in the still image, for visitors who've turned off motion.

## Fonts

Newsreader (headings) and DM Sans (everything else) are free Google Fonts, loaded in `<head>`.

## Publishing (Netlify)

1. Create a free account at netlify.com → **Add new site → Import an existing project → GitHub** and choose this repository.
2. Leave the build command empty and set the publish directory to `/`. Deploy.
3. Every change pushed to GitHub republishes automatically.
4. When you're ready, add `commongooded.com` under **Domain settings** and update the domain's DNS records where it's registered.
