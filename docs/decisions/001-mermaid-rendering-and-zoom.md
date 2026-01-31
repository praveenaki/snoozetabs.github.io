# ADR-001: Mermaid Diagram Rendering and Zoom Controls

**Status:** Accepted
**Date:** 2026-01-30
**Decision Makers:** Praveen, Claude
**Tags:** #mermaid #docsify #ux #diagrams

---

## Context

The Snooze Tabs user guide uses Docsify to render markdown documentation, including Mermaid flowcharts for visualizing user flows and decision trees. Two critical issues were identified:

1. **Rendering Failures**: The "Flow Diagram" on the Tab Overwhelm page showed a bomb icon (Mermaid's error indicator) instead of the flowchart
2. **Readability**: The "Decision Tree" diagram rendered but was too small to read, with no way to zoom or enlarge it

### Technical Background

- **Docsify**: Static site generator that renders markdown on the client side
- **Mermaid**: JavaScript library for rendering diagrams from text definitions
- **Integration**: Custom Docsify plugin converts `mermaid` code blocks to Mermaid diagrams

### Observed Symptoms

| Diagram | Symptom | User Impact |
|---------|---------|-------------|
| Flow Diagram | Bomb icon with "Syntax error in text" | Users cannot see the workflow |
| Decision Tree | Renders but tiny, unreadable text | Users must squint or cannot use the guide |

---

## Decision

### Decision 1: Fix HTML Entity Encoding Issue

**Problem**: Docsify HTML-escapes markdown content before plugins process it. Mermaid arrows `-->` become `--&gt;`, which Mermaid cannot parse.

**Solution**: Add `decodeHtmlEntities()` function to decode HTML entities before passing content to Mermaid.

```javascript
function decodeHtmlEntities(text) {
    const textarea = document.createElement('textarea');
    textarea.innerHTML = text;
    return textarea.value;
}
```

**Rationale**:
- Uses browser's native HTML parsing (reliable, handles all edge cases)
- Non-invasive fix that doesn't require changes to Docsify or Mermaid
- Applied at the integration layer where the problem occurs

**Alternatives Considered**:
| Alternative | Why Rejected |
|-------------|--------------|
| Use Docsify's raw markdown | Would break other markdown processing |
| Pre-render diagrams as SVG | Loses editability, increases maintenance burden |
| Use different diagram library | Mermaid is well-supported and feature-rich |

### Decision 2: Simplify Mermaid Diagram Syntax

**Problem**: Emojis and `<br/>` tags in node labels caused parsing failures or visual artifacts.

**Solution**: Remove emojis and replace `<br/>` line breaks with simplified labels.

Before:
```mermaid
A[😫 Too many tabs open] --> B[...]
C[⏰ Tomorrow<br/>e.g., Hacker News]
```

After:
```mermaid
A[Too many tabs open!] --> B[...]
C["TOMORROW preset"]
```

**Rationale**:
- Emojis have inconsistent support across Mermaid versions and renderers
- `<br/>` tags interact poorly with HTML entity encoding
- Simplified labels are more accessible and translate better

**Trade-offs**:
- Loss of visual personality from emojis
- Gain in reliability and cross-platform consistency

### Decision 3: Add Click-to-Zoom Modal for Diagrams

**Problem**: Complex diagrams are hard to read at their default size.

**Solution**: Wrap diagrams in clickable containers that open a fullscreen modal with zoom controls.

**Implementation**:
```
┌─────────────────────────────────────┐
│  .mermaid-wrapper                   │
│  ┌───────────────────────────────┐  │
│  │  .mermaid (clickable)         │  │
│  │  [diagram SVG]                │  │
│  └───────────────────────────────┘  │
│  "🔍 Click to zoom" (hover hint)    │
└─────────────────────────────────────┘

Modal:
┌─────────────────────────────────────┐
│ [×]                                 │
│                                     │
│   ┌─────────────────────────────┐   │
│   │  Zoomed diagram             │   │
│   │  (scalable 0.5x - 3x)       │   │
│   └─────────────────────────────┘   │
│                                     │
│   [- Zoom Out] [Reset] [+ Zoom In]  │
└─────────────────────────────────────┘
```

**Features**:
- Click diagram to open modal
- Zoom in/out/reset buttons (0.5x to 3x range)
- Close via × button, Escape key, or clicking outside
- Hover hint shows "🔍 Click to zoom"
- Dark theme matching site aesthetics

**Rationale**:
- Non-intrusive: diagrams work normally until user needs more detail
- No external dependencies (pure CSS/JS)
- Consistent with common lightbox UX patterns

**Alternatives Considered**:
| Alternative | Why Rejected |
|-------------|--------------|
| Pan-zoom library (panzoom.js) | Added dependency, complex gestures |
| CSS hover zoom | Accidental activation, poor mobile UX |
| Larger default diagrams | Breaks page flow, doesn't scale |
| External diagram viewer link | Breaks reading flow |

---

## Implementation Details

### Files Changed

| File | Changes |
|------|---------|
| `user-guide/index.html` | Added CSS for modal, JS for zoom functionality, updated Mermaid plugin |
| `user-guide/use-cases/tab-overwhelm.md` | Simplified diagram syntax |

### CSS Classes Added

| Class | Purpose |
|-------|---------|
| `.mermaid-wrapper` | Container with relative positioning for zoom hint |
| `.mermaid-modal` | Fullscreen overlay for zoomed view |
| `.mermaid-modal-content` | Scrollable container for zoomed diagram |
| `.mermaid-modal-controls` | Button container for zoom controls |
| `.mermaid-modal-close` | Close button styling |

### JavaScript Functions Added

| Function | Purpose |
|----------|---------|
| `decodeHtmlEntities(text)` | Decode HTML entities in Mermaid code |
| `openMermaidModal(element)` | Open zoom modal with diagram content |
| `closeMermaidModal()` | Close modal and restore page scroll |
| `zoomMermaid(delta)` | Adjust zoom level (delta=0 resets) |

---

## Consequences

### Positive

- Diagrams render reliably across all pages
- Users can zoom to read complex diagrams
- Simplified diagram syntax is more maintainable
- No new dependencies added
- Consistent dark theme styling

### Negative

- Slight increase in page weight (~2KB CSS/JS)
- Emojis removed from diagrams (less visual flair)
- Modal doesn't support touch gestures (pinch-to-zoom)

### Risks

| Risk | Mitigation |
|------|------------|
| Mermaid version incompatibility | Pinned to Mermaid v10 |
| Modal accessibility | Added Escape key handler, focus management could be improved |
| CDN caching delays | Changes will propagate as cache expires |

---

## Validation

### Manual Testing Performed

1. ✅ Fresh markdown fetch renders correctly
2. ✅ First diagram (Flow Diagram) renders without errors
3. ✅ Second diagram (Decision Tree) renders correctly
4. ✅ Click-to-zoom modal opens
5. ✅ Zoom in/out/reset buttons work
6. ✅ Escape key closes modal
7. ✅ Click outside closes modal

### Known Issue

CDN caching may serve stale markdown content for a period after deployment. Hard refresh (Cmd+Shift+R) or incognito mode shows correct content immediately.

---

## Related Documents

- [INC-001: Mermaid Bomb Icon - HTML Entity Encoding](../incidents/001-mermaid-html-entity-encoding.md)
- [INC-002: Mermaid Syntax Error - Emojis in Node Labels](../incidents/002-mermaid-emoji-parsing.md)
- [INC-003: Decision Tree br Tags Displayed Literally](../incidents/003-mermaid-br-tag-escaping.md)

---

## References

- [Mermaid Documentation](https://mermaid.js.org/)
- [Docsify Plugin Development](https://docsify.js.org/#/write-a-plugin)
- [HTML Entity Decoding Techniques](https://stackoverflow.com/questions/1912501/unescape-html-entities-in-javascript)
