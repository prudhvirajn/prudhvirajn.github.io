# Prudhviraj Naidu's Personal Website

This repository contains the Hugo source for [prudhvirajn.github.io](https://prudhvirajn.github.io), plus the generated `docs/` output that GitHub Pages serves.

## Stack

- Hugo Extended
- PaperMod as a git submodule
- GitHub Pages serving from `docs/`

## Active Structure

```text
.
├── assets/                # Repo-level CSS overrides for the active Hugo site
├── content/               # Homepage, CV, posts, and other Hugo content
├── docs/                  # Generated site output committed for GitHub Pages
├── layouts/               # Hugo partial overrides
├── static/                # Images and static assets copied into the build
├── themes/PaperMod/       # Theme submodule kept close to upstream
├── legacy/jekyll/         # Archived pre-Hugo site, not used by the current build
└── hugo.toml              # Site configuration
```

## Development

Initialize the theme submodule if needed:

```bash
git submodule update --init --recursive
```

Run the local dev server:

```bash
hugo server -D
```

Build the deployable site into `docs/`:

```bash
hugo --cleanDestinationDir
```

## Editing Content

- Homepage content lives in `content/_index.md`.
- Blog posts live in `content/posts/`.
- Static images belong in `static/images/` and are referenced as `/images/<filename>`.
- Repo-specific styling belongs in `assets/css/extended/custom.css`, not inside the theme submodule.

## Notes

- The current site is Hugo-only. The older Jekyll site is archived under `legacy/jekyll/` for reference.
- GitHub Pages serves the committed contents of `docs/`.
- `public/` is treated as disposable local output and is ignored.
- GitHub Pages docs: [docs.github.com/pages](https://docs.github.com/pages)

## 📄 License

This website is built using the Hugo PaperMod theme. Content is personal academic work.

---

*Last updated: 2024*
