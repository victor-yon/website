# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About This Project

This is an **al-folio** academic website built with Jekyll - a static site generator for creating personal, professional, and academic portfolio websites. The site is configured for Victor Yon and includes support for publications, CV, projects, blog posts, news, and more.

## Development Commands

### Local Development with Docker (Recommended)

```bash
# Pull latest image and start development server
docker compose pull
docker compose up

# Access site at http://localhost:8080
```

### Code Quality

```bash
# Format with Prettier
npx prettier --write .

# Check for broken links (requires lychee)
# Run via GitHub Actions or install lychee locally
```

## Architecture Overview

### Jekyll Site Structure

This is a standard Jekyll site with custom plugins and extensive configuration:

- **Content Collections**: `_posts/` (blog), `_projects/`, `_news/`, `_books/`, `_bibliography/` (publications)
- **Pages**: `_pages/` contains standalone pages (about, CV, publications, etc.)
- **Layouts**: `_layouts/` defines page templates (post, distill, bib, cv, etc.)
- **Includes**: `_includes/` contains reusable components (header, footer, social links, etc.)
- **Styling**: `_sass/` contains SCSS files organized by component (_themes.scss, _variables.scss, _base.scss, etc.)
- **Custom Plugins**: `_plugins/` contains Ruby plugins for citations, bibliography processing, and more

### Key Configuration

All site configuration is in `_config.yml`:
- Site metadata (title, description, URL)
- Theme customization (colors, dark mode)
- Plugin settings (Jekyll Scholar, pagination, feeds)
- Third-party library versions and integrity hashes
- Collection definitions

### Content Management

**Publications**: Managed via BibTeX in `_bibliography/papers.bib`. Jekyll Scholar processes this into formatted publication lists. Custom keywords in BibTeX entries add buttons (PDF, Code, Slides, etc.).

**CV**: Two formats supported:
1. JSON Resume format: `assets/json/resume.json` (preferred)
2. YAML format: `_data/cv.yml` (fallback)

**Blog Posts**: Markdown files in `_posts/` with `YYYY-MM-DD-title.md` naming convention. Supports Distill-style academic posts with special formatting.

**Projects**: Markdown files in `_projects/` displayed in responsive grid layout.

**News**: Short announcements in `_news/`, displayed on the about page.

### Custom Plugins

Ruby plugins in `_plugins/`:
- `google-scholar-citations.rb`: Fetches citation metrics
- `inspirehep-citations.rb`: HEP citation data
- `hide-custom-bibtex.rb`: Filters internal BibTeX fields
- `external-posts.rb`: Integrates external blog posts
- `cache-bust.rb`: Adds cache busting to assets
- `details.rb`: Custom details/summary elements
- `download-3rd-party.rb`: Downloads third-party libraries

### Deployment

Automated deployment via GitHub Actions (`.github/workflows/deploy.yml`):
1. Builds site on push to main branch
2. Deploys to `gh-pages` branch
3. Served via GitHub Pages

Manual deployment: Build locally and copy `_site/` contents to hosting server.

## Common Customization Tasks

**Change theme color**: Edit `--global-theme-color` in `_sass/_themes.scss`

**Modify CV**: Edit `assets/json/resume.json` (JSON Resume format) or `_data/cv.yml`

**Add publications**: Add BibTeX entries to `_bibliography/papers.bib`

**Update social links**: Edit `_data/socials.yml`

**Add co-author info**: Update `_data/coauthors.yml` for automatic linking

**Configure repositories page**: Edit `_data/repositories.yml`

## Important Notes

- Changes to `_config.yml` require site rebuild (restart server or push to GitHub)
- All edits should be made on the `main` branch - the `gh-pages` branch is auto-generated
- URL/baseurl settings in `_config.yml` are critical for correct link generation
- The site uses extensive third-party libraries (MathJax, Chart.js, Mermaid, etc.) - versions defined in `_config.yml`
- ImageMagick is required for responsive image generation (verify with `convert -version`)

## Jekyll Scholar Configuration

Publications are sorted by year (descending) by default. Configuration in `_config.yml` under `scholar:` controls:
- Author name matching (for highlighting your name)
- Bibliography file location
- Citation style (APA by default)
- Group by (year, type, etc.)
- BibTeX filters and keywords

## File Naming Conventions

- Blog posts: `YYYY-MM-DD-title.md` in `_posts/`
- Projects: Any name in `_projects/` (typically `#_project.md`)
- Pages: Any name in `_pages/` with `permalink:` in frontmatter
- News: `announcement_#.md` in `_news/`

## Dependencies

**Ruby Gems** (see Gemfile):
- jekyll (core)
- jekyll-scholar (bibliography)
- jekyll-paginate-v2 (pagination)
- Various other Jekyll plugins

**Python**: Required for Jupyter notebook support (nbconvert)

**Node.js**: Required for some build processes and Prettier formatting

**System**: ImageMagick for image processing
