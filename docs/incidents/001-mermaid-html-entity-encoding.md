# INC-001: Mermaid Bomb Icon - HTML Entity Encoding

**Date:** 2026-01-30
**Severity:** High (Feature completely broken)
**Status:** Resolved
**Tags:** #mermaid #docsify #html-encoding #parsing

---

## Symptom

The "Flow Diagram" Mermaid chart on the Tab Overwhelm page displayed a bomb icon with the error message "Syntax error in text" instead of rendering the flowchart.

![Bomb icon indicating Mermaid parsing failure](screenshot-placeholder.png)

---

## Investigation Timeline

### Initial Hypothesis
The diagram markdown might contain invalid Mermaid syntax.

### Investigation Steps

1. **Checked markdown source** - The Mermaid code looked valid:
   ```mermaid
   flowchart TD
       A[Too many tabs open] --> B[Click Snooze Tabs icon]
   ```

2. **Tested Mermaid directly** - Created a test div with the same content and called `mermaid.run()` - it rendered successfully.

3. **Compared content paths** -
   - Direct fetch of markdown file: Renders correctly
   - Docsify-processed content: Fails with syntax error

4. **Inspected HTML output** - Found the issue:
   ```html
   <!-- What Docsify produces -->
   <code class="lang-mermaid">flowchart TD
       A[Too many tabs open] --&gt; B[Click Snooze Tabs icon]
   </code>
   ```

   The `-->` arrows were HTML-encoded to `--&gt;`!

### Root Cause

**Docsify's markdown processor HTML-escapes content before plugins can access it.**

The processing pipeline:
```
Markdown → Docsify HTML-escapes → Plugin extracts content → Mermaid tries to parse --&gt; → FAILS
```

Mermaid expects `-->` but receives `--&gt;`, which is not valid Mermaid syntax.

---

## Resolution

### Fix Applied

Added HTML entity decoding before passing content to Mermaid:

```javascript
function decodeHtmlEntities(text) {
    const textarea = document.createElement('textarea');
    textarea.innerHTML = text;
    return textarea.value;
}

// In the plugin:
hook.afterEach(function(html) {
    return html.replace(
        /<pre[^>]*><code[^>]*class="[^"]*lang-mermaid[^"]*"[^>]*>([\s\S]*?)<\/code><\/pre>/gi,
        function(match, code) {
            const decoded = decodeHtmlEntities(code);  // <-- Fix here
            return '<div class="mermaid-wrapper"><div class="mermaid">' + decoded + '</div></div>';
        }
    );
});
```

### Why This Fix Works

The `textarea.innerHTML` trick leverages the browser's HTML parser to decode entities:
- `&gt;` → `>`
- `&lt;` → `<`
- `&amp;` → `&`
- `&quot;` → `"`

This is reliable because it uses the same decoder the browser uses for rendering HTML.

---

## Verification

```javascript
// Test in browser console
async () => {
  const response = await fetch('https://snoozetabs.com/user-guide/use-cases/tab-overwhelm.md');
  const text = await response.text();
  const match = text.match(/```mermaid\n([\s\S]*?)```/);

  const testDiv = document.createElement('div');
  testDiv.textContent = match[1];
  document.body.appendChild(testDiv);

  await mermaid.run({ querySelector: '.test' });
  // Result: Renders successfully with fresh content
}
```

---

## Key Learnings

1. **HTML encoding happens before plugins** - Docsify (and similar SPA frameworks) HTML-escape content for security. Plugins must decode if they pass content to external parsers.

2. **The textarea trick is reliable** - Using `textarea.innerHTML = encoded; return textarea.value;` is the canonical way to decode HTML entities in JavaScript.

3. **Test the data flow, not just endpoints** - The markdown was valid, Mermaid worked fine, but the integration layer transformed the data.

4. **Mermaid's error display is helpful** - The bomb icon + "Syntax error in text" clearly indicated a parsing failure, not a missing dependency.

---

## Prevention

For future Docsify plugins that pass content to external parsers:

```javascript
// ALWAYS decode HTML entities when extracting from Docsify-processed HTML
function decodeHtmlEntities(text) {
    const textarea = document.createElement('textarea');
    textarea.innerHTML = text;
    return textarea.value;
}
```

---

## Related

- [ADR-001: Mermaid Diagram Rendering and Zoom Controls](../decisions/001-mermaid-rendering-and-zoom.md)
- [INC-002: Mermaid Emoji Parsing](002-mermaid-emoji-parsing.md)
