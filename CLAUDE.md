# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a standalone, single-file HTML application that provides a markdown viewer with folder and ZIP file support. The entire application is contained in `markdown_viewer_multi_folder.html` with no build process or dependencies to install.

## Architecture

**Single-File Application**: All HTML, CSS, and JavaScript are contained in one self-contained file that can be opened directly in a browser.

**Key Components**:
- **File Management**: Supports loading markdown files from local folders (via `webkitdirectory`) or ZIP files (via JSZip)
- **Tree Structure**: Files are organized into a collapsible folder tree with persistence of folder states in localStorage
- **Markdown Rendering**: Uses marked.js for parsing markdown and highlight.js for syntax highlighting
- **Material Design UI**: Custom CSS implementing Material Design principles with CSS custom properties for theming

**State Management**:
- `tree`: Global object holding the hierarchical file structure
- `selectedPath`: Currently selected file path
- `folderState`: Object stored in localStorage (`mdviewer_folder_state` key) to persist folder open/closed states

**Core Functions**:
- `buildTree(files)`: Constructs hierarchical tree structure from flat file list
- `mergeTrees(target, source)`: Merges new files into existing tree (allows loading multiple folders/zips)
- `renderNode(node)`: Recursively renders tree nodes with search filtering
- `openFile(node)`: Loads and renders markdown content, sets up code copy buttons and anchor links

## Development

Since this is a single HTML file with no build process:

1. **Testing**: Open `markdown_viewer_multi_folder.html` directly in a browser
2. **Debugging**: Use browser DevTools console for JavaScript debugging
3. **No Build Required**: Changes to the file are immediately reflected on browser reload

## External Dependencies (CDN)

The application loads these libraries from CDN:
- marked.js: Markdown parsing
- highlight.js: Code syntax highlighting
- JSZip: ZIP file extraction
- Google Fonts: Roboto font family

All dependencies are loaded at runtime; no package manager or build tools are used.
