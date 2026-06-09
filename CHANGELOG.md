# Changelog

All notable changes to this project are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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

[0.1.0]: https://github.com/sharkyger/hugo-serif-starter/releases/tag/v0.1.0
