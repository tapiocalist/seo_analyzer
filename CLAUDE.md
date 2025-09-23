# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a client-side SEO analysis tool built as a single HTML file containing CSS and JavaScript. The tool provides both **batch URL downloading** and **multi-file SEO analysis** capabilities with comprehensive data export functionality.

## Architecture

- **Single File Application**: All functionality contained in `index.html`
- **Client-Side Only**: No backend required, runs entirely in browser
- **CORS Proxy Support**: Uses multiple proxy services for fetching external URLs
- **Multi-File Processing**: Supports batch upload and analysis of multiple HTML files
- **Data Persistence**: Uses localStorage for file state and history management

## Layout Structure

### Two-Section Design (Vertical Layout)
1. **Section 1: Batch URL Download**
   - Multi-line URL input textarea
   - Batch download functionality with progress tracking
   - Automatic file naming: `hostname_timestamp_index.html`

2. **Section 2: Multi-File SEO Analysis**
   - Multiple HTML file upload (supports incremental addition)
   - Individual supplement information input per file
   - Batch analysis with progress tracking
   - Comprehensive Excel export functionality
   - Individual file detail viewing

## Core Features

### 1. Batch URL Download
- **Input**: Multi-line textarea for URL lists
- **Progress Tracking**: Real-time download progress with status feedback
- **File Naming**: Format: `hostname_timestamp_index.html`
- **Error Handling**: Individual URL failure tracking

### 2. Multi-File SEO Analysis
- **File Upload**: Supports multiple HTML files with cumulative addition
- **Duplicate Prevention**: Automatic detection of duplicate files (name + size)
- **File Management**: Individual file removal capability
- **Supplement Data**: Individual supplement information input per file

### 3. SEO Analysis Features
- **Basic Elements**: Title, Description, H1/H2 tags with status evaluation
- **Page Statistics**: Word count (content only, excluding code)
- **Keyword Density**: 1-4 word combinations with frequency analysis
- **SERP Competition**: Support for Google search result format parsing

### 4. Data Export & Viewing
- **Batch Excel Export**: Multi-row TSV format with comprehensive data
- **Individual Detail View**: Full analysis display using original interface
- **Data Persistence**: localStorage-based state management
- **History Tracking**: Recent analysis history (10 records)

## Technical Implementation

### File Processing
- **Multiple File Support**: FileReader API for reading HTML files
- **Cumulative Addition**: New files are added to existing list without replacement
- **Duplicate Detection**: Checks filename and file size to prevent duplicates
- **File Management**: Individual file removal with corresponding data cleanup

### Text Analysis
- **Content Extraction**: Uses `document.body.textContent` (excludes code)
- **Word Filtering**: Minimum 2 characters, supports English and Chinese (`\u4e00-\u9fff`)
- **Keyword Density**: 1-4 word combinations with frequency analysis
- **Statistics**: Word count, character count, heading analysis

### Supplement Data Parsing
- **Format Support**: Tab-separated keyword data and Google SERP format
- **Auto-Detection**: Intelligent detection of data type and format
- **Keyword Metrics**: Supports keyword, URL, traffic, search results, intitle, KD, KGR
- **SERP Format**: Google search results (title, site, URL, description)

### Data Storage & Persistence
- **localStorage API**: File state, analysis results, and history
- **State Management**: Maintains uploaded files across page refreshes
- **History System**: Recent 10 analysis records with website name display
- **Data Structure**: Organized storage for efficient retrieval

### Proxy Configuration
Currently uses multiple CORS proxy services:
1. `https://api.codetabs.com/v1/proxy?quest=`
2. `https://thingproxy.freeboard.io/fetch/`
3. `https://cors-anywhere.herokuapp.com/`
4. `https://crossorigin.me/`
5. `https://api.allorigins.win/get?url=`

### Status Evaluation Criteria
- **Title**: Good (30-60 chars), Warning (<30 or >60), Error (missing)
- **Description**: Good (120-160 chars), Warning (<120 or >160), Error (missing)
- **H1**: Good (exactly 1), Warning (multiple), Error (missing)

## User Interface Flow

### Multi-File Analysis Workflow
1. **Upload Files**: Select multiple HTML files (incremental addition supported)
2. **Add Supplement Data**: Individual supplement information per file
3. **Batch Analysis**: Click "分析全部" to process all files
4. **View Results**:
   - Click "复制全部到Excel" for batch export
   - Click "查看详情" for individual file analysis
5. **File Management**: Use "移除" to remove unwanted files

### Button State Management
- **Upload Phase**: Only "分析全部" button visible
- **Analysis Phase**: Progress display with file count (e.g., "分析中... 3/5")
- **Complete Phase**: "复制全部到Excel" and "查看详情" buttons enabled

## Development & Testing

### Local Development
```bash
# Method 1: Direct browser access
# Open index.html directly in browser

# Method 2: HTTP server (if needed)
npm install
npm run dev  # Starts http-server on port 8080
```

### File Structure
```
seo_analyzer/
├── index.html                 # Main application file (updated from seo_analyzer.html)
├── seo_tool_requirements.md   # Original requirements documentation
├── settings.local.json        # Claude Code permissions configuration
├── vercel.json               # Vercel deployment configuration
├── package.json              # Node.js project metadata
└── CLAUDE.md                 # This documentation file
```

## Excel Export Format

### Column Structure
The exported Excel data contains the following columns (TSV format):
1. **文件名** - Original HTML filename
2. **关键词** - Keyword from supplement data
3. **URL** - Target URL from supplement data
4. **获得流量** - Traffic data from supplement data
5. **搜索结果数量** - Search results count
6. **Intitle** - Intitle search count
7. **KD难度** - Keyword difficulty
8. **KGR** - Keyword Golden Ratio (intitle/results)
9. **页面标题** - Page title from HTML
10. **页面描述** - Meta description from HTML
11. **H1** - H1 tags (semicolon separated)
12. **H2** - H2 tags (semicolon separated)
13. **单词数** - Word count from content
14. **1词** - Single-word keywords with counts
15. **2词** - Two-word keywords with counts
16. **3词** - Three-word keywords with counts
17. **4词** - Four-word keywords with counts
18. **SERP竞争分析标题** - SERP competitor titles
19. **SERP竞争分析网址** - SERP competitor URLs

### Data Format Notes
- **Multi-value fields**: Separated by "; " (semicolon + space)
- **Keywords**: Format is "keyword(count)" for each entry
- **Missing data**: Empty strings for unavailable information
- **File format**: TSV (Tab-Separated Values) for Excel compatibility

## Supplement Data Formats

### Keyword Information Format (Tab-separated)
```
Keyword	URL	Search Volume	Traffic	Difficulty	CPC	Results	Intitle	Competition	Trend
example keyword	https://example.com	1000	500	45	1.2	50000	200	Medium	Stable
```

### Google SERP Format
```
Search Result Title 1
Search Result Title 2

Website Name 1
https://example1.com › path › to › page
Description of the search result...

Website Name 2
https://example2.com › another › path
Another description...
```

## Browser Compatibility

Supports modern browsers (Chrome, Firefox, Safari, Edge) with ES6+ features:
- `fetch()` API for HTTP requests
- `DOMParser` for HTML parsing
- `URL` constructor for validation
- `async/await` syntax
- `FileReader` API for file processing
- `localStorage` API for data persistence

## Color Scheme

- Primary: `#644a40` (brown)
- Background: `#f9f9f9` (light gray)
- Cards: `#fcfcfc` (white)
- Borders: `#d8d8d8` (gray)
- Good status: `#ffdfb5` background, `#582d1d` text
- Warning status: `#ffe6c4` background, `#582d1d` text
- Error status: `#e54d2e` background, `#ffffff` text
- Remove button: `#dc3545` (red)
- Detail button: `#666` (gray, enabled after analysis)

## Troubleshooting

### Common Issues
1. **SERP links not displaying**: Ensure Google format with › symbols or explicit "SERP links" header
2. **Files not persisting**: Check browser localStorage permissions
3. **Analysis fails**: Verify HTML file format and content
4. **Excel copy fails**: Use fallback manual copy dialog if clipboard API fails
5. **Duplicate detection**: Based on filename and file size matching

### Debug Information
- Check browser console for parsing logs
- "Parsing completed. Found X SERP links" indicates successful parsing
- File state saved to localStorage automatically

### Performance Notes
- Large files (>5MB) may take longer to process
- Batch analysis processes files sequentially
- localStorage has browser-dependent size limits (~5-10MB)