# Serif Starter

A hardened, mobile-first Hugo starter for **personal-brand sites** — coaches,
mentors, beauty, tattoo, barber, and other people-led businesses. Built on the
excellent [Serif](https://github.com/zerostaticthemes/hugo-serif-theme) theme
by Robert Austin (Zerostatic Themes), with the one fix that vertical needs most:
**the hero photo stays visible on mobile.**

---

## Why this starter

Stock Serif treats the hero image as decorative and **hides it on phones**
(`display: none` at the mobile breakpoint), stacking the image *above* the title
on the rare screens where it shows. For a personal brand, the person's face is
the primary conversion driver — hiding it on mobile (where most visitors are)
throws away the strongest reason someone keeps reading.

This starter changes that. On mobile the hero now **stacks title-first, with the
photo directly below the title — always visible**. On desktop the original
side-by-side layout is preserved. See [Mobile hero](#mobile-hero) for the details
and the regression guard.

On top of that it ships a small OSS quality floor: pinned reproducible builds,
SCSS linting, an offline link check, and clean (warning-free) output on modern
Hugo.

---

## Usage

This is a starter, not a dependency — you **fork it and edit it directly**.

1. **Create your project** from this repo
   - Click **"Use this template"** on GitHub, or
   - `git clone https://github.com/sharkyger/hugo-serif-starter.git my-site && cd my-site && rm -rf .git && git init`

2. **Set your content and branding** (all of it lives in plain config/markdown —
   see [Rebrand for a client](#rebrand-for-a-client) for the full map):
   - **Site name / SEO** → `config.toml` → `title`, `[params.seo]`
   - **Colors** → `config.toml` → `[params.colors]`
   - **Fonts** → `config.toml` → `[params.fonts]`
   - **Logo** → `config.toml` → `[params.logo]` + `static/images/logo/`
   - **Hero photo** → `content/_index.md` → `intro_image` + `static/images/`
   - **Pages / services / team** → `content/`
   - **Features, social, contact** → `data/`

3. **Preview locally**

   ```bash
   hugo server
   # open http://localhost:1313
   ```

4. **Deploy** the built site. Any static host works (Netlify, Cloudflare Pages,
   GitHub Pages, Vercel, S3, …):

   ```bash
   hugo --gc --minify          # outputs to ./public
   ```

   Point your host at the build command `hugo --gc --minify` and the publish
   directory `public/`. Set `baseURL` in `config.toml` to your real domain.

### Mobile hero

The headline customization. Three coordinated changes keep the hero photo
visible and correctly ordered on small screens:

| Where | Change |
| --- | --- |
| `layouts/index.html` | Text column is `order-1` → **title first** on mobile |
| `layouts/partials/intro-image.html` | Image column is `order-2` → **photo below the title** |
| `assets/scss/components/_intro-image.scss` | `.intro-image-hide-mobile` is `display: block` → **never hidden**; negative top-margin only applies on desktop |
| `content/_index.md` | `intro_image_hide_on_mobile: false` |

**Regression guard:** verified at a 375 px viewport. If you re-introduce
`display: none` on the hero image, or flip the column order, the face disappears
on phones — the exact bug this starter exists to fix. The SCSS override carries a
comment saying so; please keep it.

### Rebrand for a client

Everything brand-specific is a config value, a data file, or an asset — there is
no need to touch templates for a normal rebrand.

| Knob | File | Notes |
| --- | --- | --- |
| Site title & meta | `config.toml` → `title`, `[params.seo]` | Twitter handles + OG share image |
| Brand colors | `config.toml` → `[params.colors]` | `primary`, `black`, `white`, `white_offset`, `grey` — compiled into the CSS |
| Fonts | `config.toml` → `[params.fonts]` | `google_fonts` link + `heading` / `base` family names |
| Logo | `config.toml` → `[params.logo]` + `static/images/logo/` | Separate desktop/mobile SVGs and heights |
| Footer copyright | `config.toml` → `[params.footer].copyright_text` | HTML allowed |
| Navigation | `config.toml` → `[menu]` | `main` and `footer` menus |
| Hero photo & headline | `content/_index.md` | `intro_image`, plus the markdown body is the H1/intro |
| Contact details | `data/contact.yaml` | Phone, email, contact-button link |
| Social links | `data/social.json` | Replace the `your-username` / `your-handle` placeholders |
| Feature cards | `data/features.json` | Title, description, icon path |
| Services / Team / About | `content/services/`, `content/team/`, `content/about.md` | Standard Hugo content |

> Keep image filenames free of spaces (use `kebab-case`) — spaces become `%20`
> in URLs and break on some hosts.

---

## Install

You need the **Hugo extended** binary (the SCSS pipeline requires it). The Node
tooling below is only needed if you want to run the SCSS linter locally; it is
not required to build or serve the site.

```bash
# 1. Get the code
git clone https://github.com/sharkyger/hugo-serif-starter.git
cd hugo-serif-starter

# 2. (optional) install lint tooling
npm install

# 3. Run it
hugo server
```

Lint and build commands:

```bash
npm run lint          # stylelint over the project SCSS
npm run lint:scss:fix # auto-fix what stylelint can
hugo --gc --minify    # production build into ./public
```

---

## System requirements

| Tool | Version | Required for |
| --- | --- | --- |
| **Hugo (extended)** | **v0.158.0 or newer** | Building and serving the site. Built and tested on **v0.162.1 extended**. The extended build is mandatory (Sass/SCSS). |
| Node.js + npm | v20 or newer | Optional — only for running stylelint locally / in CI. |

Install Hugo extended: <https://gohugo.io/installation/>. Confirm the **extended**
edition with `hugo version` (the output must contain `+extended`).

---

## License & credits

Released under the [MIT License](LICENSE).

This project is a derivative of the **Serif** Hugo theme by **Robert Austin**
(Zerostatic Themes), used and redistributed under the MIT License. The upstream
copyright notice is retained in [`LICENSE`](LICENSE) as the license requires.

- Upstream theme: <https://github.com/zerostaticthemes/hugo-serif-theme>
- Zerostatic Themes: <https://www.zerostatic.io>

Demo content (example business copy, illustrations, and stock photography) is
inherited from the upstream theme's example site and is intended to be replaced.
