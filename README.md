# Prudhviraj Naidu's Personal Website

This repository contains the source code for my personal academic website, hosted at [prudhvirajn.github.io](https://prudhvirajn.github.io).

## 🏗️ Architecture

- **Static Site Generator**: Hugo (version 0.110.0+)
- **Theme**: PaperMod (customized)
- **Hosting**: GitHub Pages
- **Output Directory**: `docs/` (contains all generated static files)
- **Deployment**: Automatic via GitHub Pages from `docs/` directory on `master` branch

## 📁 Project Structure

```
prudhvirajn.github.io/
├── content/                 # Hugo content files
│   ├── _index.md           # Homepage content
│   ├── cv.md               # CV page
│   └── posts/              # Blog posts
├── themes/                 # Hugo themes
│   └── PaperMod/          # PaperMod theme (customized)
├── docs/                  # Generated static site (served by GitHub Pages)
├── static/                # Static assets (images, files)
├── layouts/               # Custom Hugo layouts
├── hugo.toml             # Hugo configuration
└── CLAUDE.md             # AI assistant instructions
```

## 🚀 Getting Started

### Prerequisites

- [Hugo Extended](https://gohugo.io/installation/) (version 0.110.0 or higher)
- Git

### Local Development

1. **Clone the repository**:
   ```bash
   git clone https://github.com/prudhvirajn/prudhvirajn.github.io.git
   cd prudhvirajn.github.io
   ```

2. **Initialize theme submodule** (if needed):
   ```bash
   git submodule update --init --recursive
   ```

3. **Start local development server**:
   ```bash
   hugo server -D
   ```
   Visit `http://localhost:1313` to view the site locally.

4. **Build for production**:
   ```bash
   hugo --destination docs
   ```

## ✏️ Content Management

### Homepage Updates

The main homepage content is in `content/_index.md`. Key sections include:

- **Profile Information**: Name, title, email, social links
- **About Me**: Research interests and background
- **Publications**: Academic papers and research

### Adding Blog Posts

1. Create a new markdown file in `content/posts/`:
   ```bash
   hugo new posts/my-new-post.md
   ```

2. Edit the front matter and content:
   ```yaml
   ---
   title: "My New Post"
   date: 2024-01-01T00:00:00Z
   draft: false
   tags: ["research", "machine-learning"]
   ---
   
   Your post content here...
   ```

3. Rebuild the site:
   ```bash
   hugo --destination docs
   ```

### Updating Publications

Edit the publications section in `content/_index.md`:

```markdown
- **Authors.** "Paper Title." *Conference/Journal*, Year. [DOI](https://doi.org/...)
```

### Adding New Pages

1. Create new content file:
   ```bash
   hugo new page-name.md
   ```

2. Add to navigation menu in `hugo.toml`:
   ```toml
   [[menu.main]]
   name = "Page Name"
   url = "/page-name/"
   weight = 40
   ```

## 🎨 Customization

### Theme Customization

The PaperMod theme has been customized with:

- **Light theme permanently enabled** (dark mode toggle removed)
- **Custom CSS** for social icons and styling in `themes/PaperMod/assets/css/extended/custom.css`
- **Modified layouts** for header and footer

### CSS Customization

Add custom styles to `themes/PaperMod/assets/css/extended/custom.css`:

```css
/* Your custom styles here */
.custom-class {
    /* styles */
}
```

### Adding Images

1. Place images in `static/images/`
2. Reference in markdown: `![Alt text](/images/filename.jpg)`

## 🚀 Deployment

### Automatic Deployment

The site deploys automatically when you push changes to the `master` branch:

1. **Make changes** to content or configuration
2. **Rebuild the site**:
   ```bash
   hugo --destination docs
   ```
3. **Commit and push**:
   ```bash
   git add .
   git commit -m "Update content"
   git push origin master
   ```

GitHub Pages will automatically serve the updated site from the `docs/` directory.

### Manual Deployment

If you need to deploy manually:

1. Ensure `docs/` contains the latest build
2. Push to the `master` branch
3. GitHub Pages will update within a few minutes

## 🔧 Configuration

### Hugo Configuration (`hugo.toml`)

Key configuration options:

```toml
baseURL = "https://prudhvirajn.github.io"
languageCode = "en-us"
title = "Prud's Log"
theme = "PaperMod"

[params]
  author = "Prudhviraj Naidu"
  description = "PhD student in Computer Science with focus on machine learning and software engineering"
  # Other PaperMod parameters...
```

### GitHub Pages Configuration

- **Source**: Deploy from `docs/` folder on `master` branch
- **Custom Domain**: None (using GitHub Pages default)
- **HTTPS**: Enabled

## 📝 Content Guidelines

### Writing Style

- Use clear, academic tone
- Include proper citations for research work
- Optimize for readability and accessibility

### SEO Best Practices

- Use descriptive titles and meta descriptions
- Include relevant keywords in content
- Optimize images with alt text
- Use proper heading hierarchy (H1, H2, H3...)

## 🔍 Troubleshooting

### Common Issues

1. **Site not updating**: 
   - Ensure you've run `hugo --destination docs` after changes
   - Check that changes are committed and pushed to `master`

2. **CSS not loading**:
   - Clear browser cache
   - Rebuild site with `hugo --destination docs`

3. **Theme issues**:
   - Check if PaperMod submodule is properly initialized
   - Verify custom CSS syntax

### Build Errors

If Hugo build fails:

1. Check syntax in markdown files
2. Verify front matter formatting
3. Ensure all required files exist
4. Check Hugo version compatibility

## 🔄 Maintenance Tasks

### Regular Updates

- **Monthly**: Review and update publications
- **Quarterly**: Update CV and research interests
- **As needed**: Add new blog posts and research updates

### Backup

- Repository is backed up on GitHub
- Consider periodic local backups of the entire repository

### Performance

- Periodically audit site performance
- Optimize images for web
- Monitor site loading times

## 📞 Support

For issues or questions:

- Check Hugo documentation: [gohugo.io/documentation](https://gohugo.io/documentation/)
- PaperMod theme docs: [github.com/adityatelange/hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod)
- GitHub Pages docs: [docs.github.com/pages](https://docs.github.com/pages)

## 📄 License

This website is built using the Hugo PaperMod theme. Content is personal academic work.

---

*Last updated: 2024*