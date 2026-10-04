# DJ Dizzy — landing page

One-page portfolio for DJ Dizzy. Static files only: no build step, no framework.

```
index.html          the whole site (markup, styles, scripts)
assets/
  img/              photos as AVIF + WebP in several sizes
  fonts/            Unbounded 900 (latin, woff2); body text uses the system font
  og.jpg            link preview image (1200×630)
  favicon.svg       browser tab icon
  apple-touch-icon.png
README.md           this file
```

GSAP and ScrollTrigger load from cdnjs with pinned versions and integrity hashes. Everything else is in this folder.

## Publish on GitHub Pages

The site is built for `https://dj-dizzy.github.io`. A GitHub "user site" takes its address from the account name, so the account has to be called `dj-dizzy`.

1. Sign in to GitHub as `dj-dizzy` (create the account at github.com/signup if needed).
2. Create a new repository: github.com/new. Name it exactly `dj-dizzy.github.io`, keep it **Public**, do not add a README or .gitignore. Click **Create repository**.
3. On the empty repository page click **uploading an existing file**.
4. Drag `index.html`, `README.md` and the whole `assets` folder into the drop zone. Drag the folder itself, not its contents, so the `assets/` path is kept.
5. Click **Commit changes**.
6. Open **Settings → Pages**. Source should read "Deploy from a branch", branch `main`, folder `/ (root)`. Save if it is not already set.
7. Wait one to two minutes, then open `https://dj-dizzy.github.io`. The first deploy can take up to ten minutes.

Later changes: edit or re-upload `index.html` the same way. Pages redeploys on every commit.

### Using git instead of the browser

```bash
cd path/to/this/folder
git init
git add index.html README.md assets
git commit -m "DJ Dizzy site"
git branch -M main
git remote add origin https://github.com/dj-dizzy/dj-dizzy.github.io.git
git push -u origin main
```

### If the account name is different

If `dj-dizzy` is taken and the site lives at another address, search `index.html` for `https://dj-dizzy.github.io` and replace all occurrences. They are the canonical link, the Open Graph tags, the JSON-LD block and the booking form's redirect.

## After the first deploy

1. **Activate the booking form.** The form posts to FormSubmit. Submit it once from the live site. FormSubmit sends an activation email to `dj.dizzy.m@gmail.com`. Click the link in that email once and every later submission arrives in the inbox. Submissions come as a table and the sender receives an automatic reply.
2. **Check the link preview.** Paste the site URL into a WhatsApp or Instagram chat with yourself. The preview should show the festival photo with the name and tagline (`assets/og.jpg`).
3. **Open it on a phone.** The WhatsApp button follows the visitor as a round red button once the hero scrolls away.

## Editing content

Everything lives in `index.html`. Search for the text you want to change.

- **Venues:** the `<ol class="venue-list">` block. Each row is a number, a venue name and a city.
- **Rider:** the three `<details class="acc">` blocks (Technical, Travel, Press).
- **Contact:** the WhatsApp number appears in the `wa.me` links, the email in `mailto:` links and in the form `action`.
- **SoundCloud:** the profile link is `https://soundcloud.com/marwan-sanad-338259448` and the player uses user id `1044314455`. If the profile changes, update both.
- **Photos:** each `<picture>` lists an AVIF source and a WebP fallback in several widths. To swap a photo, export the new one at the same widths (for example 540, 720, 1086 px) as `.avif` and `.webp` and replace the files in `assets/img/`. Squoosh (squoosh.app) does this in the browser. Keep the `width` and `height` attributes in step with the new image so nothing shifts while loading.

## Behaviour notes

- The hero swirl is a small WebGL shader driven by scroll speed. It switches off for `prefers-reduced-motion`, on devices with 2 GB of memory or fewer, when data saver is on, or when WebGL is unavailable; the plain photo shows instead.
- Scroll reveals are CSS transitions switched on by an IntersectionObserver. Scroll-linked moves (hero drift, the pinned festival shot, the gallery parallax) use GSAP ScrollTrigger, loaded after the page has painted. If the CDN is unreachable the page still works without those moves.
- The SoundCloud player is loaded only when the visitor taps play, so no third-party script runs before that.
