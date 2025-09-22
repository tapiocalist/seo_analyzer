# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a client-side SEO analysis tool built as a single HTML file containing CSS and JavaScript. The tool analyzes web pages for SEO elements including Title, Description, H-tags, keyword density, and provides batch download functionality.

## Architecture

- **Single File Application**: All functionality contained in `seo_analyzer.html`
- **Client-Side Only**: No backend required, runs entirely in browser
- **CORS Proxy Support**: Uses multiple proxy services for fetching external URLs
- **File Processing**: Supports local HTML file upload and analysis

## Core Features

### SEO Analysis
- **Basic Elements**: Title, Description, H1 tags with status evaluation
- **Page Statistics**: Word count (content only, not code), character count, heading count (H1-H6), image count, link count
- **Heading Structure**: H1-H3 tags displayed in hierarchical indented format
- **Keyword Density**: 1-5 word combinations with frequency and density percentages

### Batch Processing
- **Bulk URL Input**: Multi-line textarea for URL lists
- **Progress Tracking**: Real-time download progress with status feedback
- **Auto-Analysis**: Optional automatic analysis of first downloaded file
- **File Naming**: Format: `hostname_timestamp_index.html`

## Technical Implementation

### Text Analysis
- Extracts visible content from `document.body.textContent` (excludes code)
- Filters words with minimum 2 characters
- Supports both English and Chinese characters (`\u4e00-\u9fff`)
- Calculates keyword density as percentage of total words

### Proxy Configuration
Currently uses two CORS proxy services:
1. `https://api.allorigins.win/get?url=`
2. `https://corsproxy.io/?`

### Status Evaluation Criteria
- **Title**: Good (30-60 chars), Warning (<30 or >60), Error (missing)
- **Description**: Good (120-160 chars), Warning (<120 or >160), Error (missing)
- **H1**: Good (exactly 1), Warning (multiple), Error (missing)

## Development Commands

No build process required - open `seo_analyzer.html` directly in browser for testing.

## File Structure
```
seo_analyzer/
├── seo_analyzer.html          # Main application file
├── seo_tool_requirements.md   # Requirements documentation
├── settings.local.json        # Permissions configuration
└── CLAUDE.md                 # This file
```

## Browser Compatibility

Supports modern browsers (Chrome, Firefox, Safari, Edge) with ES6+ features:
- `fetch()` API for HTTP requests
- `DOMParser` for HTML parsing
- `URL` constructor for validation
- `async/await` syntax

## Color Scheme

- Primary: `#644a40` (brown)
- Background: `#f9f9f9` (light gray)
- Cards: `#fcfcfc` (white)
- Borders: `#d8d8d8` (gray)
- Good status: `#ffdfb5` background, `#582d1d` text
- Warning status: `#ffe6c4` background, `#582d1d` text
- Error status: `#e54d2e` background, `#ffffff` text