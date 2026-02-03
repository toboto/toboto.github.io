# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal technical blog built with Jekyll and hosted on GitHub Pages. The blog is written in Chinese and focuses on technical topics including MongoDB, Linux, Python, and various development tools. The site uses the Cayman theme and is deployed at https://toboto.github.io.

## Development Commands

### Setup
```bash
# Install dependencies
script/bootstrap
# or manually:
gem install bundler
bundle install
```

### Local Development
```bash
# Run local development server (http://localhost:4000)
script/server
# or manually:
bundle exec jekyll serve
```

### Build and Validation
```bash
# Full build with validation (used for CI)
script/cibuild

# Individual steps:
bundle exec jekyll build              # Build site to _site/
bundle exec htmlproofer ./_site --check-html --check-sri
bundle exec rubocop -D                # Lint Ruby code
bundle exec script/validate-html      # Validate HTML/CSS with W3C
```

## Site Architecture

### Directory Structure
- `_posts/` - Blog posts in Markdown with YAML front matter
- `_layouts/` - HTML templates (default.html for pages, post.html for blog posts)
- `_sass/` - Sass stylesheets
- `script/` - Build and deployment scripts
- `assets/` - Static assets (CSS, images)

### Post Format
Blog posts must follow this naming convention: `YYYY-MM-DD-title.md`

Required front matter:
```yaml
---
layout: post
title: "Post Title"
subtitle: "Optional subtitle"
date: YYYY-MM-DD
author: "toboto"
tags:
    - Tag1
    - Tag2
---
```

### Layouts
- **default.html**: Base layout for pages (index, about). Includes site header, footer with ICP registration number (京ICP备19023853号-1), and Baidu analytics.
- **post.html**: Layout for blog posts. Extends default layout with utteranc.es commenting system integrated (uses `toboto/toboto.github.io` repo, pathname-based issue terms).

## Configuration

The `_config.yml` file controls site settings. Important: After changes to `_config.yml`, you must restart the Jekyll server (it does NOT auto-reload this file).

Key configuration:
- Theme: `jekyll-theme-cayman`
- GitHub Pages compatibility: Uses `github-pages` gem v203
- Plugins: `jekyll-feed`

## Important Notes

- The site is configured for GitHub Pages deployment
- Changes to `_config.yml` require server restart
- HTML validation uses W3C NuValidator for HTML and CSSValidator for CSS
- The site includes Baidu analytics tracking
- Post layout includes utteranc.es comments (configured to create GitHub issues in this repo)
