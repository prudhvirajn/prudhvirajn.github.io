# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal website/blog repository hosted on GitHub Pages at prudhvirajn.github.io. The live site is built with Hugo and the PaperMod theme.

## Architecture

- **Static Site Generator**: Hugo
- **Theme**: PaperMod (git submodule in `themes/PaperMod`)
- **Deploy Output**: `docs/`
- **Hosting**: GitHub Pages serving from `docs/`

## Key Directories

- `content/` - Hugo content for the homepage, CV, posts, and pages
- `static/` - Static assets copied into the final site
- `assets/` - Repo-level CSS overrides for the active Hugo site
- `layouts/` - Hugo partial overrides
- `docs/` - Generated output committed for GitHub Pages
- `legacy/jekyll/` - Archived pre-Hugo site, not used by the current build

## Important Notes

- Make source changes in the Hugo project files, then rebuild `docs/`.
- Keep custom CSS and layout overrides in the repo, not inside the PaperMod submodule.
- Treat `public/` as disposable local output.
- GitHub Pages serves directly from the committed `docs/` directory.

## Deployment

Rebuild the site with:

```bash
hugo --cleanDestinationDir
```

Any committed changes in `docs/` will be reflected on the live site at prudhvirajn.github.io.

## PaperMod Theme Tips

- **Centering Images**: To center images in markdown posts, add `#center` to the end of the image URL:
  ```markdown
  ![Alt text](/images/image.jpg#center)
  ```
  The PaperMod theme has built-in CSS that automatically centers images with this suffix.
