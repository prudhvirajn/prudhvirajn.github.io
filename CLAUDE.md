# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal website/blog repository hosted on GitHub Pages at prudhvirajn.github.io. The site is built using Hugo static site generator and contains academic publications and blog posts.

## Architecture

- **Static Site Generator**: Hugo (version 0.110.0)
- **Output Directory**: `docs/` - Contains all generated static files (HTML, CSS, JS)
- **Hosting**: GitHub Pages (configured to serve from `docs/` directory)
- **Content Structure**:
  - Publications page with academic papers
  - Blog posts including "The Perfect State" series
  - Profile image and site assets

## Key Directories

- `docs/` - Generated static site files (HTML, CSS, JS, images)
  - `posts/` - Generated blog post pages
  - `publications/` - Academic publications page
  - `assets/` - CSS and JavaScript files
  - `images/` - Site images including profile picture

## Important Notes

- This repository contains only the generated Hugo output in `docs/`
- The Hugo source files (content, themes, config) are not present in this repository
- Any content changes would need to be made in the Hugo source project
- The site uses PaperMod theme (evident from CSS structure)
- GitHub Pages serves directly from the `docs/` directory on the `master` branch

## Deployment

The site is automatically served by GitHub Pages from the `docs/` directory. Any changes to files in `docs/` will be reflected on the live site at prudhvirajn.github.io.

## Content Management

Since this repository only contains the generated output, content updates should be made in the original Hugo source project and then the generated files should be copied to this repository's `docs/` directory.