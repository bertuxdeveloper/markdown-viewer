# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a standalone, single-file HTML application that provides a feature-rich markdown viewer with folder and ZIP file support. The entire application is contained in `markdown_viewer_multi_folder.html` with no build process or dependencies to install.

## Architecture

**Single-File Application**: All HTML, CSS, and JavaScript are contained in one self-contained file that can be opened directly in a browser.

**Key Components**:
- **File Management**: Supports loading markdown files from local folders (via `webkitdirectory`) or ZIP files (via JSZip) with drag & drop support
- **Tree Structure**: Files are organized into a collapsible folder tree with persistence of folder states in localStorage
- **Advanced Markdown Rendering**:
  - Uses marked.js for parsing markdown and highlight.js for syntax highlighting
  - Mermaid.js for diagram rendering
  - KaTeX for mathematical equation rendering
  - Auto-generated Table of Contents
- **Material Design UI**: Custom CSS implementing Material Design principles with CSS custom properties for theming
- **Search**: Dual-mode search (filename and full-text content search) with highlighting
- **Export**: Multiple export formats (HTML with theme preservation, PDF, and Markdown with annotations)
- **User Preferences**: Comprehensive settings panel with font size, line height, preview width, 6 theme presets, code highlighting themes
- **Favorites & Recent Files**: Quick access to frequently used files

**State Management**:
- `tree`: Global object holding the hierarchical file structure
- `selectedPath`: Currently selected file path
- `folderState`: Folder open/closed states persisted in localStorage (`mdviewer_folder_state`)
- `searchMode`: Current search mode (filename or content)
- `recentFiles`: Array of recently opened files (max 10)
- `favorites`: Array of bookmarked file paths
- All user preferences stored in localStorage with dedicated keys

**Core Functions**:
- `buildTree(files)`: Constructs hierarchical tree structure from flat file list
- `mergeTrees(target, source)`: Merges new files into existing tree (allows loading multiple folders/zips)
- `renderNode(node)`: Recursively renders tree nodes with search filtering
- `openFile(node)`: Loads and renders markdown content, handles Mermaid diagrams, KaTeX math
- `performSearch(query)`: Full-text search across file contents with caching
- `exportAsHTML()`: Exports current document as standalone HTML with theme preservation
- `exportAsPDF()`: Exports current document as PDF using jsPDF and html2canvas
- `exportAsMarkdown()`: Exports original markdown with YAML frontmatter annotations
- `generateTOC()`: Auto-generates table of contents from headings
- `applyThemePreset(name)`: Applies one of 6 predefined theme presets

## Development

Since this is a single HTML file with no build process:

1. **Testing**: Open `markdown_viewer_multi_folder.html` directly in a browser
2. **Debugging**: Use browser DevTools console for JavaScript debugging
3. **No Build Required**: Changes to the file are immediately reflected on browser reload

## External Dependencies (CDN)

The application loads these libraries from CDN:
- **marked.js**: Markdown parsing
- **highlight.js**: Code syntax highlighting with multiple theme support
- **JSZip**: ZIP file extraction
- **Mermaid.js**: Diagram rendering (flowcharts, sequence diagrams, etc.)
- **KaTeX**: Mathematical equation rendering
- **jsPDF**: PDF generation for export functionality
- **html2canvas**: HTML to canvas rendering for PDF export
- **Google Fonts**: Roboto font family

All dependencies are loaded at runtime; no package manager or build tools are used.

## Features

### Navigation & Search
- **Keyboard Shortcuts**: `/` for search, `↑/↓` for navigation, `Enter` to open, `Esc` to clear, `T` for TOC, `?` for help, `Ctrl/Cmd+,` for settings
- **Resizable Sidebar**: Drag the handle to adjust sidebar width (persisted)
- **Breadcrumb Navigation**: Clickable path segments for quick directory navigation
- **Recent Files**: Automatically tracks last 10 opened files
- **Favorites/Bookmarks**: Star files for quick access

### Display & Theming
- **Dark Mode**: Toggle between light and dark themes
- **Theme Presets**: 6 built-in themes (Light, Dark, GitHub, Dracula, Nord, Monokai)
- **Font Customization**: Adjustable font size (12-24px) and line height
- **Preview Width**: Choose between 700px, 900px, 1200px, or full width
- **Code Highlighting**: 5 code highlighting themes available
- **Mobile Responsive**: Full mobile support with hamburger menu

### Export Options
- **HTML Export**: Standalone HTML file with embedded theme colors and styles
- **PDF Export**: High-quality PDF with proper page breaks
- **Markdown Export**: Original source with YAML frontmatter metadata

### Advanced Markdown
- **Diagrams**: Full Mermaid.js support for flowcharts, sequence diagrams, etc.
- **Math Equations**: LaTeX math rendering via KaTeX
- **Table of Contents**: Auto-generated from headings with floating panel
- **Search Highlighting**: Visual highlighting of search terms in content
