# Fernbank LINKS Robotics — website

Static site for Fernbank LINKS (FRC Team 4468 / BEST Team 701). Plain HTML, CSS,
and one small JavaScript file — no build step, no framework, no dependencies to
keep updated. Drop it in a repo and GitHub Pages serves it as-is.

```
index.html            all page content
assets/css/style.css  all styling
assets/js/main.js     mobile menu, scroll reveals, footer year
assets/img/           images and placeholders
CNAME                 custom domain for GitHub Pages
.nojekyll             tells Pages to serve files as-is
```

---

## Put it online

1. **Create the repo.** On GitHub, make a new repository. If you want the URL to
   be `https://<org>.github.io`, name the repo exactly `<org>.github.io`.
   Otherwise any name works and the site lands at `https://<org>.github.io/<repo>/`.

2. **Upload the files.** Either drag the contents of this folder into the
   repo's upload page, or from a terminal:

   ```bash
   cd fernbank-links-site
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/<org>/<repo>.git
   git push -u origin main
   ```

   Upload the *contents* of this folder, not the folder itself — `index.html`
   must sit at the top level of the repo.

3. **Turn on Pages.** Repo → **Settings** → **Pages** → Source: *Deploy from a
   branch* → Branch: `main`, folder: `/ (root)` → **Save**. First build takes
   about a minute.

4. **Point the domain at it.** See below.

---

## Using fernbanklinks.com

The `CNAME` file in this repo already contains `fernbanklinks.com`. Two things
have to line up:

**At GitHub:** Settings → Pages → Custom domain → `fernbanklinks.com` → Save.
Once DNS resolves, tick **Enforce HTTPS**.

**At your DNS provider** (whoever manages the domain — this is separate from
whoever hosted the old site), create these records:

| Type  | Name  | Value                    |
|-------|-------|--------------------------|
| A     | `@`   | `185.199.108.153`        |
| A     | `@`   | `185.199.109.153`        |
| A     | `@`   | `185.199.110.153`        |
| A     | `@`   | `185.199.111.153`        |
| CNAME | `www` | `<org>.github.io.`       |

Remove any old A or CNAME records for `@` and `www` first, or they'll conflict.
DNS changes can take a few hours to propagate; the HTTPS certificate is issued
automatically after that.

> If you can't get into the domain registrar either, that's the piece to chase
> down first — the site can go live on the `github.io` URL immediately and the
> domain can be attached later without touching the code.

---

## Editing the site

Everything is in `index.html`, in plain HTML with comments marking each section.
Edit on GitHub directly (click the file → pencil icon → Commit) and the site
rebuilds in about a minute.

**Adding a robot to the build log.** Find the `<ol class="roster">` block, copy
one `<li class="roster-item">` and change four things — the year, the image path,
the robot name, and the game name:

```html
<li class="roster-item reveal">
  <span class="roster-year">2026</span>
  <div class="roster-plate">
    <img class="roster-photo" src="assets/img/robot-2026.jpg" alt="Our 2026 robot, Name.">
    <h3 class="roster-name">Name</h3>
    <p class="roster-game">Game name</p>
  </div>
</li>
```

The roster currently ends at 2019 because that's where the old site stopped —
2020 onward still needs to be filled in.

**Swapping in real photos.** Put your image files in `assets/img/`, then change
the `src` on the matching `<img>` tag. Keep the file names lowercase with no
spaces (`robot-2019.jpg`, not `Robot 2019.JPG`). Resize photos to roughly
1600px wide before uploading so pages stay fast. Always update the `alt` text to
describe what's actually in the photo — screen readers and search engines both
use it.

The `assets/img/placeholder-*.svg` files are stand-ins. Once every one has been
replaced you can delete them.

**Changing colors.** The palette lives at the very top of
`assets/css/style.css`, in the `:root` block. Change a hex value there and it
updates everywhere it's used.

**Social links.** In the footer. Check each one before launch — some of the old
handles may have moved.

---

## Adding a working contact form

The site currently uses `mailto:` links, which work everywhere with no setup. If
you'd rather have a real form, [Formspree](https://formspree.io) has a free tier
that works on static sites. Sign up, get your form ID, and add this inside the
contact section:

```html
<form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
  <label>Your email <input type="email" name="email" required></label>
  <label>Message <textarea name="message" required></textarea></label>
  <button type="submit">Send</button>
</form>
```

---

## Before you launch — checklist

- [ ] Replace all placeholder images
- [ ] Add robots from 2020 to now
- [ ] Verify the phone number, email, and street address
- [ ] Check every social link opens the right account
- [ ] Link the actual Impact Report (currently points back to Contact)
- [ ] Read the site on a phone
