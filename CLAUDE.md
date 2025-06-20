# CLAUDE.md - Development Guide for Social Insight Tools

## Site Architecture

### Theme Information
- **Theme**: `digital-garden-hugo-theme` 
- **Source**: https://github.com/apvarun/digital-garden-hugo-theme
- **Production**: Using Hugo modules (go.mod) for automatic updates
- **Development**: Local reference copy in `theme-reference/` (gitignored)
- **Version Management**: Theme updates via `hugo mod get -u`


## Development Shortcuts

### Development Workflow
1. **Reference theme files**: Check `theme-reference/layouts/` for patterns
2. **Copy and modify**: Start with existing template (e.g., articles/list.html)
3. **Test locally**: Use `hugo server` for live reload
4. **Search theme code**: Use grep/find to locate specific functionality

### Quick Commands
```bash
# Start development server
hugo server

# Update theme
hugo mod get -u

# Update local theme reference
cd theme-reference && git pull

# Build site
hugo

# View current theme version
hugo mod graph

# Search theme files locally
grep -r "search" theme-reference/layouts/
find theme-reference/ -name "*.html" | xargs grep "article"

# Identify which layouts are used by content files
hugo list all
```

## Layout Identification Method

Hugo determines which layout to use based on content structure:

1. **Section-based layouts**: For content in `content/maps/`, Hugo looks for:
   - `layouts/maps/list.html` (section list pages like `/maps/`)
   - `layouts/maps/single.html` (individual pages like `/maps/prosperity/`)
   - Falls back to `layouts/_default/list.html` or `layouts/_default/single.html`

2. **Use `hugo list all`** to see content structure and section assignments
3. **Check theme reference** in `theme-reference/layouts/` for existing patterns
4. **Layout lookup order**: Hugo follows a specific precedence (section > type > default)

## Maintenance Strategy
### Layout Philosophy
- Override only what you need to change
- Reuse theme partials wherever possible
- Follow theme's CSS/JS conventions
- Document departures from theme patterns