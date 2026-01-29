# CLAUDE.md - Jekyll Academic Site

This is a Jekyll static site deployed to GitHub Pages, based on the Academic Pages theme (fork of Minimal Mistakes).

## Quick Reference

### Key Configuration Files

| File | Purpose |
|------|---------|
| `_config.yml` | Main Jekyll configuration - site settings, author info, plugins |
| `_config.dev.yml` | Development overrides (disables analytics, uncompressed CSS) |
| `Gemfile` | Ruby dependencies - uses `github-pages` gem for compatibility |
| `_data/navigation.yml` | Main navigation menu structure |
| `_data/authors.yml` | Author profile data |

### Important Directories

| Directory | Purpose |
|-----------|---------|
| `_posts/` | Blog posts (format: `YYYY-MM-DD-title-slug.md`) |
| `_pages/` | Static pages (about, CV, archives, etc.) |
| `_layouts/` | Page templates (single, archive, talk, splash) |
| `_includes/` | Reusable template partials |
| `_sass/` | SCSS stylesheets |
| `_data/` | YAML data files for navigation, authors, UI text |
| `assets/` | CSS, JS, fonts |
| `images/` | Image assets |
| `files/` | Downloadable files (PDFs, etc.) |

## Blog Post Guidelines

### Creating New Posts

1. **Filename format**: `YYYY-MM-DD-title-slug.md` in `_posts/`
2. **Required frontmatter**:
   ```yaml
   ---
   title: 'Post Title'
   date: YYYY-MM-DD  # MUST be actual date, not placeholder!
   permalink: /posts/YYYY/MM/post-slug/
   tags:
     - tag1
     - tag2
   ---
   ```

### CRITICAL: Date Format

- **ALWAYS use ISO 8601 format**: `date: 2025-12-17`
- **NEVER use placeholders** like `date: YYYY-MM-DD` - this breaks the build
- The date in frontmatter should match the filename date

### Future Posts

The site has `future: true` in `_config.yml`, so future-dated posts will be included in builds.

## Site Configuration

### Key _config.yml Settings

```yaml
# Site identity
title: "DieStoking the Academic Fire"
url: https://diestok.github.io/
timezone: Europe/Amsterdam

# Post behavior
future: true              # Include future-dated posts
words_per_minute: 160     # For read time calculation

# Collections (output: false = not generating pages)
collections:
  teaching: { output: false }
  publications: { output: false }
  portfolio: { output: false }
  talks: { output: false }

# Enabled plugins
plugins:
  - jekyll-paginate
  - jekyll-sitemap
  - jekyll-gist
  - jekyll-feed
  - jekyll-redirect-from
```

### Navigation

Edit `_data/navigation.yml` to enable/disable menu items. Currently only "Blog Posts" link is active.

## Deployment

### GitHub Pages Auto-Build

- Builds automatically on push to `master` branch
- Uses `github-pages` gem (includes Jekyll + all compatible plugins)
- No custom GitHub Actions workflow - uses default Pages build

### Local Development

```bash
# Install dependencies
bundle install

# Serve locally with live reload
bundle exec jekyll liveserve

# Or standard serve
bundle exec jekyll serve
```

Development config override: `bundle exec jekyll serve --config _config.yml,_config.dev.yml`

## Common Issues & Fixes

### Build Fails with "Invalid date"

**Cause**: Post frontmatter has invalid date format
**Fix**: Ensure `date:` field uses actual ISO date (e.g., `date: 2025-12-17`)

### Gemfile Dependency Issues

**Cause**: Gemfile conflicts with github-pages gem
**Fix**: Use minimal Gemfile that relies on `github-pages` gem for all plugins

### Posts Not Appearing

**Check**:
1. File is in `_posts/` directory
2. Filename follows `YYYY-MM-DD-title.md` format
3. Valid frontmatter with `date:` field
4. If future date, verify `future: true` in config

## Theme Customization

Based on **Minimal Mistakes v3.4.2** (Academic Pages fork)

### Layout hierarchy
```
compress.html → default.html → single.html/archive.html/talk.html
```

### Styling
- SCSS files in `_sass/`
- Main entry point: `assets/css/main.scss`
- Variables: `_sass/_variables.scss`

## What to Check First

When troubleshooting:

1. **_posts/** - Check date formats in frontmatter
2. **_config.yml** - Verify settings haven't been corrupted
3. **Gemfile** - Should only have `github-pages` gem + dev dependencies
4. **_data/navigation.yml** - For menu issues
5. **GitHub Actions logs** - For specific build errors

## Files to Never Edit Carelessly

- `_config.yml` - One typo breaks the whole site
- `Gemfile` - Dependency conflicts cause build failures
- `_layouts/default.html` - Base template for all pages
- `_includes/head.html` - Meta tags, CSS loading
