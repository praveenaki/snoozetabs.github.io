# ADR 003: Hero Header Animation Style

## Status
**Accepted** - Implemented Option 4 (Static Action, Rotating Object)

*Note: Initially tried Option 1 (Dual Rotating Words) but it felt too busy. Switched to Option 4 for cleaner UX.*

## Context
The Snooze Tabs product has two core actions (Snooze, Save) and three object types (Tabs, Windows, Todos). The hero header needs to communicate this breadth of functionality in an engaging, modern way.

The original static header was:
```
Snooze tabs, windows and todos for later
```

We wanted to upgrade to an animated header that cycles through the capabilities dynamically.

## Decision Drivers
- **Engagement**: Modern websites use motion to capture attention
- **Feature Communication**: Show the full range of actions and objects
- **Brand Alignment**: Match the modern, polished feel of the product
- **Performance**: Keep it lightweight for GitHub Pages (no heavy libraries)
- **Accessibility**: Animation should be smooth, not jarring

## Options Considered

### Option 1: Dual Rotating Words
```
[Snooze/Save] [Tabs/Windows/Todos] for later
```

**Implementation**: Two independent rotating word containers with different cycle speeds.
- Actions rotate every 3.5s
- Objects rotate every 2.5s

**Pros**:
- Most dynamic and engaging
- Shows all 6 combinations naturally
- Independent timing creates visual interest
- Communicates product breadth effectively

**Cons**:
- Slightly more complex CSS/JS
- Can create unexpected word combinations
- Two simultaneous animations may be distracting to some users

**When to use**: When you want maximum engagement and have multiple independent dimensions to show.

---

### Option 2: Curated Phrase Rotation
```
Cycle through specific phrases:
- "Snooze Tabs for later"
- "Save Windows for later"
- "Snooze Todos for later"
- etc.
```

**Implementation**: Single rotating container with full phrases.

**Pros**:
- Full control over which combinations appear
- Can prioritize key use cases
- Simpler mental model for users
- Predictable messaging

**Cons**:
- Less dynamic feeling
- Longer text means larger container needed
- May feel more "slideshow" than "modern animation"

**When to use**: When specific messaging control is critical, or when certain combinations don't make sense.

---

### Option 3: Stacked Animated Lines
```
Snooze it.
Save it.
For later.
```

**Implementation**: Vertical stack with sequential line animations.

**Pros**:
- Bold, impactful visual design
- Works well for short, punchy copy
- Creates rhythm with sequential reveals
- Very modern aesthetic

**Cons**:
- Takes more vertical space
- Harder to show all object types
- May not work well on mobile
- Loses the sentence structure

**When to use**: For brand-focused landing pages where impact matters more than feature communication.

---

### Option 4: Static Action, Rotating Object (CHOSEN)
```
Snooze or Save [Tabs/Windows/Todos] for later
```

**Implementation**: Single rotating container for objects only.

**Pros**:
- Simplest implementation
- "Snooze or Save" always visible
- Objects are the main variable
- Clearest communication of core value prop

**Cons**:
- Less dynamic
- "Snooze or Save" is longer text
- May feel less modern than other options

**When to use**: When the action verbs must always be visible, or for simpler implementations.

---

## Technical Implementation Notes

### CSS Animation Approach
Uses `@keyframes` with `translateY` and `opacity`:
- `slideOutUp`: Word slides up and fades out
- `slideInUp`: New word slides up from below and fades in
- Duration: 400ms per transition
- Timing: ease-in for out, ease-out for in

### Spacing Considerations
Inline-block elements create whitespace challenges:
- Use `margin-right: 0.25em` on containers for consistent word spacing
- Avoid negative margins that can eat spaces between words
- `overflow: hidden` on containers for clean slide animations

### Mobile Responsiveness
All options should degrade gracefully:
- Words should wrap naturally on narrow screens
- Consider reducing animation on `prefers-reduced-motion`

## Consequences

### Positive
- Header now communicates full product capability
- Modern, engaging user experience
- Lightweight implementation (vanilla JS, ~50 lines)

### Negative
- Slightly more complex than static text
- Users may not see all combinations in a brief visit

## Future Considerations
- A/B test different options to measure engagement
- Add `prefers-reduced-motion` support for accessibility
- Consider pausing animation when not in viewport
- Could extend to other parts of the page (features section, etc.)

## References
- Implementation: `index.html` (inline CSS and JS)
- CSS animation spec: [MDN @keyframes](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes)
