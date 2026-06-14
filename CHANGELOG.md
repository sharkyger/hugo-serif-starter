# Changelog

All notable changes to this project are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2026-06-14

### Added

- **Blog** section at `/blog/`: a newest-first list of cards (preview image,
  date, title, teaser, "Read the article" link) and a single-post view with an
  optional top `feature_image`, full article, and a "← Back to all posts" link.
  Includes an optional, consistent per-post call-to-action (`[params.blog.cta]`,
  off by default), a `blog` archetype, and a `Blog` main-menu entry. New files:
  `content/blog/`, `layouts/blog/{list,summary,single}.html`,
  `layouts/partials/blog-cta.html`, `archetypes/blog.md`,
  `assets/scss/components/_blog.scss`.
- **Linked phone number** on the contact box: `data/contact.yaml` gains a
  `phone_tel` field (international, no spaces) used for a `tel:` link, while the
  visible text stays the human-readable `phone`.

### Changed

- Footer copyright now renders `© <current year> | <name>` automatically;
  `[params.footer].copyright_text` is just the name/brand.
- CI hardening: all GitHub Actions are now pinned to commit SHAs (with `# vX.Y.Z`
  comments) instead of mutable tags, and a Dependabot config keeps the actions
  and dev dependencies current. CI runs on Node 22 (required by the pinned pnpm).
- **Dev tooling moved from npm to pnpm** (Corepack-managed): pinned
  `packageManager` (pnpm 11.5.2 with integrity hash) in `package.json`, a
  `pnpm-workspace.yaml` with an explicit `minimumReleaseAge` supply-chain
  freshness hold, a committed `pnpm-lock.yaml` (replacing `package-lock.json`),
  and CI switched to `corepack enable` + `pnpm install --frozen-lockfile`. The
  Hugo site itself remains zero-dependency.
- Bumped the SHA-pinned CI dependencies (via Dependabot): `actions/checkout` v6,
  `actions/setup-node` v6, `actions/upload-artifact` v7, `actions/download-artifact`
  v8, and `stylelint` 17.13.0.

### Fixed

- **Contact box no longer missing**: the `contact` layout was never applied
  (the page fell back to `_default/single.html`), so the `.call` box with phone
  and email was absent. Moved `layouts/page/contact.html` →
  `layouts/_default/contact.html` so the layout resolves and the box renders.
- Social links now use `target="_blank"` with `rel="noopener noreferrer"`
  (previously `target="blank"`, a named tab, with no `rel`).
- Feature cards now emit a meaningful `alt` (used `.Title`, which is empty for a
  data map; corrected to `.title`) — previously `alt=" logo"`.
- Corrected an invalid `font-width: bold` declaration to `font-weight: bold` in
  the content styles.

## [0.1.0] - 2026-06-08

Initial release. A standalone Hugo starter derived from the MIT-licensed
[Serif](https://github.com/zerostaticthemes/hugo-serif-theme) theme by Robert
Austin (Zerostatic Themes), hardened for personal-brand sites.

### Added

- **Mobile hero fix** (the headline change): the hero photo now stays visible on
  mobile and stacks **title-first, photo-below**, instead of being hidden by
  upstream's `display: none`. Implemented across `layouts/index.html`
  (text `order-1`), `layouts/partials/intro-image.html` (image `order-2`),
  `assets/scss/components/_intro-image.scss` (override + regression note), and
  `content/_index.md` (`intro_image_hide_on_mobile: false`). Verified at 375 px.
- OSS quality floor:
  - GitHub Actions CI — pinned **Hugo extended 0.162.1** build, stylelint, and an
    offline lychee link check on the built site.
  - `stylelint` + `stylelint-config-standard-scss` with a project config
    (`.stylelintrc.json`, `.stylelintignore`) scoped to the project's own SCSS.
  - `.github/FUNDING.yml`.
- Documentation shipped with the code: README (purpose → usage → install →
  system requirements → license) with a generic "rebrand for a client" guide,
  this CHANGELOG, and a regression note in the hero SCSS.

### Changed

- **Flattened** the upstream theme + `exampleSite` into a single standalone Hugo
  site (layouts/assets/archetypes at the root; content/data/static/config merged).
- Modernized for current Hugo so the site builds **warning-free** on 0.158+:
  `languageCode` → `locale`, and `.Site.Data` → `hugo.Data`.
- Genericized all branding to neutral placeholders (site title, SEO handles, OG
  image, footer copyright, demo social links) so the starter carries no
  third-party or downstream identity.
- Fixed one duplicate `transition` declaration in `assets/scss/components/_buttons.scss`.

### Fixed

- Renamed two feature illustrations that contained spaces in their filenames
  (`noun_The Process_…`, `noun_3d modeling_…`) to `kebab-case`, eliminating
  `%20`-encoded asset URLs that break on some hosts.

### License

- Retains Robert Austin's upstream MIT copyright and notice; adds Sharky's
  copyright line. Project remains MIT.

[Unreleased]: https://github.com/sharkyger/hugo-serif-starter/compare/v0.2.0...HEAD
[0.2.0]: https://github.com/sharkyger/hugo-serif-starter/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/sharkyger/hugo-serif-starter/releases/tag/v0.1.0
