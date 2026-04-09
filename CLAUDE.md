# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`sql-lint` is a standalone, single-file SQL linter and formatter web application. There is no build system, no package manager, and no test framework — the entire application lives in `sql-linter.html`.

## Running the Application

Open `sql-linter.html` directly in a web browser. No server, no install, no build step required.

## Architecture

The application is self-contained in `sql-linter.html` (~688 lines) with three main components:

### `sqlFormatter` (object)
- `format(query, config)` — beautifies SQL: uppercases keywords, inserts line breaks after major clauses, indents with 2 spaces by default
- `compress(query)` — minifies SQL by stripping comments and collapsing whitespace

### `SQLValidator` (class)
- Validates SQL syntax in real time
- Checks for: unclosed quotes, unbalanced parentheses, missing SQL keywords, SELECT without FROM
- Supports 30+ SQL keywords

### CodeMirror editor
- Configured with SQL syntax highlighting (material-ocean theme), auto-close brackets, bracket matching, line wrapping
- Integrated into the UI for live editing with real-time validation feedback

### UI
- Bootstrap 5.3 layout with a dark theme
- Status bar shows live line/char/word counts and validation state (green/red)
- Three action buttons: Beautify, Compress, Clear
- All dependencies loaded from CDN (Bootstrap, CodeMirror, Google Fonts)
