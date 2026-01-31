# Snooze Tabs Documentation

Technical documentation for the Snooze Tabs website and user guide.

---

## Architecture Decision Records (ADRs)

ADRs document significant technical decisions made during development.

| ADR | Title | Status | Date |
|-----|-------|--------|------|
| [ADR-001](decisions/001-mermaid-rendering-and-zoom.md) | Mermaid Diagram Rendering and Zoom Controls | Accepted | 2026-01-30 |

---

## Incident Reports

Incident reports document issues encountered and their resolutions.

| Incident | Title | Severity | Status |
|----------|-------|----------|--------|
| [INC-001](incidents/001-mermaid-html-entity-encoding.md) | Mermaid Bomb Icon - HTML Entity Encoding | High | Resolved |
| [INC-002](incidents/002-mermaid-emoji-parsing.md) | Mermaid Syntax Error - Emojis in Node Labels | High | Resolved |
| [INC-003](incidents/003-mermaid-br-tag-escaping.md) | Decision Tree `<br/>` Tags Displayed Literally | Medium | Resolved |

---

## Quick Reference

### Mermaid in Docsify - Do's and Don'ts

```markdown
# DO ✓
flowchart TD
    A[Plain text labels] --> B["Quoted labels work too"]
    B --> C[Use punctuation for emphasis!]

# DON'T ✗
flowchart TD
    A[😫 Emojis may fail] --> B[Line 1<br/>Line 2 breaks]
```

### Key Technical Decisions

1. **HTML Entity Decoding**: Always decode HTML entities when passing Docsify content to external parsers
2. **Simplified Diagrams**: Prefer plain text over emojis for reliability
3. **Zoom Modal**: Click-to-zoom pattern for complex diagrams

---

## Document History

| Date | Change |
|------|--------|
| 2026-01-30 | Initial documentation created for Mermaid fixes |
