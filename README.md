# peasy-formats-embed

[![npm](https://img.shields.io/npm/v/peasy-formats-embed)](https://www.npmjs.com/package/peasy-formats-embed)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Zero Dependencies](https://img.shields.io/badge/dependencies-0-brightgreen)](https://www.npmjs.com/package/peasy-formats-embed)
[![Size](https://img.shields.io/badge/gzipped-<8KB-green)](https://bundlephobia.com/package/peasy-formats-embed)

Embed **PeasyFormats** widgets on any website or blog. File format encyclopedia — specs, comparisons, and conversion guides. Each widget is completely isolated via **Shadow DOM**, requires **zero dependencies**, and supports **3 built-in themes** (light, dark, sepia). The self-executing script finds all `data-peasy-formats` elements on the page and renders interactive widgets automatically, including support for dynamically added elements in single-page applications via MutationObserver.

PeasyFormats is part of the [Peasy Tools](https://peasytools.com) ecosystem, providing 11 widget types for embedding file format information, tool cards, conversion guides, glossary terms, search boxes, and interactive tools directly into your pages.

> **Try the interactive widget builder at [widget.peasyformats.com](https://widget.peasyformats.com)** -- build, preview, and copy embed code for any widget type.

<p align="center">
  <img src="demo.gif" alt="peasy-formats-embed demo -- embed peasyformats widgets with Shadow DOM isolation and theme support" width="800">
</p>

## Table of Contents

- [Quick Start](#quick-start)
- [Widget Types](#widget-types)
- [Widget Options](#widget-options)
- [Themes](#themes)
- [CDN Options](#cdn-options)
- [Examples](#examples)
  - [Format Info Card](#format-info-card)
  - [Tool Card](#tool-card)
  - [Search Box](#search-box)
  - [Format Badge (Inline)](#format-badge-inline)
  - [Interactive Tool](#interactive-tool)
  - [Glossary Tooltip](#glossary-tooltip)
  - [Compact Widget (Sidebar)](#compact-widget-sidebar)
  - [Dark Theme](#dark-theme)
- [Technical Details](#technical-details)
- [Learn More](#learn-more)
- [Peasy Tools Family](#peasy-tools-family)
- [License](#license)

## Quick Start

```html
<!-- 1. Place a widget element where you want it -->
<div data-peasy-formats="format"
  data-slug="json"
  data-theme="light">
</div>

<!-- 2. Load the embed script once, anywhere on the page -->
<script src="https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.min.js"></script>
```

That's it. The script will find all `data-peasy-formats` elements, fetch data from the PeasyFormats API, and render each widget with full Shadow DOM style isolation.

## Widget Types

PeasyFormats supports 11 widget types -- 11 common types available on all Peasy sites.

| Type | Description | Usage |
|------|-------------|-------|
| `format` | File format info card with specs, MIME type, and use cases | `<div data-peasy-formats="format" data-slug="..."></div>` |
| `tool` | Tool card with description and direct launch link | `<div data-peasy-formats="tool" data-slug="..."></div>` |
| `convert` | Conversion card showing input/output format pair | `<div data-peasy-formats="convert" data-slug="..."></div>` |
| `compare` | Side-by-side comparison of two formats or tools | `<div data-peasy-formats="compare" data-slug="..."></div>` |
| `glossary` | Glossary term tooltip with definition on hover | `<div data-peasy-formats="glossary" data-slug="..."></div>` |
| `gallery` | Grid gallery of available tools for a category | `<div data-peasy-formats="gallery" data-slug="..."></div>` |
| `guide` | Guide/tutorial card with summary and read-more link | `<div data-peasy-formats="guide" data-slug="..."></div>` |
| `usecase` | Use-case card showing when and why to use a tool | `<div data-peasy-formats="usecase" data-slug="..."></div>` |
| `badge` | Inline badge showing format type or tool category | `<div data-peasy-formats="badge" data-slug="..."></div>` |
| `search` | Search box with autocomplete for tools and formats | `<div data-peasy-formats="search" data-slug="..."></div>` |
| `interactive` | Embedded interactive tool via iframe | `<div data-peasy-formats="interactive" data-slug="..."></div>` |

## Widget Options

All options are set via `data-*` attributes on the widget element.

| Attribute | Values | Default | Description |
|-----------|--------|---------|-------------|
| `data-peasy-formats` | format, tool, convert, compare, glossary, gallery, guide, usecase, badge, search, interactive | *required* | Widget type to render |
| `data-slug` | any valid slug | -- | Format or tool slug (format, tool, glossary, guide, usecase widgets) |
| `data-from` | format slug | -- | Source format for conversion widget |
| `data-to` | format slug | -- | Target format for conversion widget |
| `data-a` | slug | -- | First item for comparison widget |
| `data-b` | slug | -- | Second item for comparison widget |
| `data-category` | category slug | -- | Filter gallery by category |
| `data-url` | full URL | -- | Tool URL for interactive (iframe) widget |
| `data-height` | e.g. "500px" | "400px" | Iframe height for interactive widget |
| `data-label` | any string | slug | Display label for badge widget |
| `data-placeholder` | any string | "Search tools..." | Search input placeholder text |
| `data-theme` | light, dark, sepia, auto | light | Visual theme for the widget |
| `data-size` | compact, default, large | default | Widget size variant |
| `data-lang` | en, ko, ja, es, etc. | en | Language for widget labels |
| `data-track` | true, false | false | Send anonymous usage analytics |

## Themes

Three built-in themes are available, plus an auto mode that follows the user's OS preference.

```html
<!-- Light theme (default) -- clean white background -->
<div data-peasy-formats="format" data-slug="json" data-theme="light"></div>

<!-- Dark theme -- dark background, light text -->
<div data-peasy-formats="format" data-slug="json" data-theme="dark"></div>

<!-- Sepia theme -- warm, paper-like appearance -->
<div data-peasy-formats="format" data-slug="json" data-theme="sepia"></div>

<!-- Auto theme -- follows prefers-color-scheme -->
<div data-peasy-formats="format" data-slug="json" data-theme="auto"></div>
```

Each theme sets CSS custom properties inside the Shadow DOM. The accent color (`#6366F1`) is consistent across all themes, providing brand recognition for PeasyFormats.

## CDN Options

### jsDelivr (recommended -- global CDN, auto-updates with npm)

```html
<script src="https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.min.js"></script>
```

### npm (for bundlers like webpack, Vite, Rollup)

```bash
npm install peasy-formats-embed
```

```javascript
// Just import -- the script self-executes and activates all widgets
import 'peasy-formats-embed';
```

### ESM import (for modern module-based setups)

```html
<script type="module">
  import 'https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.esm.js';
</script>
```

## Examples

### Format Info Card

Display detailed information about a file format including MIME type, extensions, and use cases.

```html
<!-- PeasyFormats format info card with light theme -->
<div data-peasy-formats="format" data-slug="json" data-theme="light"></div>
<script src="https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.min.js"></script>
```

### Tool Card

Show a tool card with its description, category, and a direct link to launch the tool.

```html
<!-- PeasyFormats tool card -->
<div data-peasy-formats="tool" data-slug="json" data-theme="light"></div>
<script src="https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.min.js"></script>
```

### Search Box

Add a search widget with autocomplete for finding tools and formats.

```html
<!-- Search across PeasyFormats tools and formats -->
<div data-peasy-formats="search"
  data-placeholder="Search PeasyFormats tools..."
  data-theme="light">
</div>
<script src="https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.min.js"></script>
```

### Format Badge (Inline)

Display a compact inline badge showing a format type or tool category.

```html
<p>This file is in <div data-peasy-formats="badge" data-slug="json"></div> format.</p>
<script src="https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.min.js"></script>
```

### Interactive Tool

Embed a full interactive tool via iframe with complete isolation.

```html
<!-- Embed an interactive PeasyFormats tool -->
<div data-peasy-formats="interactive"
  data-url="https://peasyformats.com/embed/json/"
  data-height="500px"
  data-theme="light">
</div>
<script src="https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.min.js"></script>
```

### Glossary Tooltip

Show a glossary term with its definition, rendered as a tooltip-style card.

```html
<div data-peasy-formats="glossary" data-slug="lossless" data-theme="light"></div>
<script src="https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.min.js"></script>
```

### Compact Widget (Sidebar)

Use the compact size for sidebar placements.

```html
<div data-peasy-formats="format"
  data-slug="json"
  data-theme="light"
  data-size="compact">
</div>
<script src="https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.min.js"></script>
```

### Dark Theme

```html
<div data-peasy-formats="format"
  data-slug="json"
  data-theme="dark"
  data-size="large">
</div>
<script src="https://cdn.jsdelivr.net/npm/peasy-formats-embed@1/dist/embed.min.js"></script>
```

## Technical Details

- **Shadow DOM**: Complete CSS isolation -- widget styles never leak into your page, and your page styles never affect the widget
- **Zero dependencies**: No jQuery, React, Alpine, or any external library required
- **System fonts**: Uses the system font stack -- no Google Fonts request, instant text rendering
- **Self-executing**: Include the script tag and add data attributes -- no initialization code needed
- **MutationObserver**: Automatically detects and renders widgets added dynamically (SPA-compatible)
- **Lazy loading**: Widgets outside the viewport use IntersectionObserver for deferred initialization
- **CORS**: PeasyFormats API has CORS enabled for all origins
- **Bundle size**: < 8KB gzipped (IIFE) -- minimal impact on page load
- **Accessibility**: Semantic HTML, proper ARIA attributes, keyboard navigation support
- **Powered by**: Each widget includes a subtle "PeasyFormats" backlink in the footer

## Learn More

Visit [peasyformats.com](https://peasyformats.com) for the full PeasyFormats experience.

- **All Tools**: [peasyformats.com](https://peasyformats.com)
- **Formats**: [peasyformats.com/formats/](https://peasyformats.com/formats/)
- **Glossary**: [peasyformats.com/glossary/](https://peasyformats.com/glossary/)
- **Guides**: [peasyformats.com/guides/](https://peasyformats.com/guides/)
- **API Documentation**: [peasyformats.com/developers/](https://peasyformats.com/developers/)
- **OpenAPI Spec**: [peasyformats.com/api/openapi.json](https://peasyformats.com/api/openapi.json)
- **Widget Builder**: [widget.peasyformats.com](https://widget.peasyformats.com)
- **npm Package**: [npmjs.com/package/peasy-formats-embed](https://www.npmjs.com/package/peasy-formats-embed)

## Peasy Tools Family

Part of [Peasy Tools](https://peasytools.com) -- simple, fast, free developer tools.

| Site | Domain | npm | Focus |
|------|--------|-----|-------|
| PeasyPDF | [peasypdf.com](https://peasypdf.com) | [npm](https://www.npmjs.com/package/peasy-pdf-embed) | PDF tools, conversion, compression, merging, and splitting |
| PeasyImage | [peasyimage.com](https://peasyimage.com) | [npm](https://www.npmjs.com/package/peasy-image-embed) | Image conversion, compression, resizing, and format tools |
| PeasyVideo | [peasyvideo.com](https://peasyvideo.com) | [npm](https://www.npmjs.com/package/peasy-video-embed) | Video conversion, compression, trimming, and format tools |
| PeasyAudio | [peasyaudio.com](https://peasyaudio.com) | [npm](https://www.npmjs.com/package/peasy-audio-embed) | Audio conversion, compression, trimming, and format tools |
| PeasyCSS | [peasycss.com](https://peasycss.com) | [npm](https://www.npmjs.com/package/peasy-css-embed) | CSS tools, minification, formatting, color conversion, and previews |
| PeasyText | [peasytext.com](https://peasytext.com) | [npm](https://www.npmjs.com/package/peasy-text-embed) | Text tools, word counting, encoding, hashing, and formatting |
| PeasyTools | [peasytools.com](https://peasytools.com) | [npm](https://www.npmjs.com/package/peasy-tools-embed) | The Peasy Tools hub |
| **PeasyFormats** | [peasyformats.com](https://peasyformats.com) | [npm](https://www.npmjs.com/package/peasy-formats-embed) | File format encyclopedia |
| PeasyDev | [peasydev.com](https://peasydev.com) | [npm](https://www.npmjs.com/package/peasy-dev-embed) | Developer tools |
| PeasyDesign | [peasydesign.com](https://peasydesign.com) | [npm](https://www.npmjs.com/package/peasy-design-embed) | Design tools |
| PeasyQR | [peasyqr.com](https://peasyqr.com) | [npm](https://www.npmjs.com/package/peasy-qr-embed) | QR code generation, scanning, and customization tools |
| PeasySEO | [peasyseo.com](https://peasyseo.com) | [npm](https://www.npmjs.com/package/peasy-seo-embed) | SEO analysis tools |
| PeasySafe | [peasysafe.com](https://peasysafe.com) | [npm](https://www.npmjs.com/package/peasy-safe-embed) | Security tools |
| PeasySocial | [peasysocial.com](https://peasysocial.com) | [npm](https://www.npmjs.com/package/peasy-social-embed) | Social media tools |
| PeasyMath | [peasymath.com](https://peasymath.com) | [npm](https://www.npmjs.com/package/peasy-math-embed) | Math tools |
| PeasyGen | [peasygen.com](https://peasygen.com) | [npm](https://www.npmjs.com/package/peasy-gen-embed) | Generator tools |

## License

MIT -- see [LICENSE](./LICENSE).

Built by [Peasy Tools](https://peasytools.com).
