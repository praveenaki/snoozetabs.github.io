# Save for Later Flow

How the Save for Later feature works.

```mermaid
flowchart TD
    A[User has a tab open] --> B[Click Snooze Tabs icon]
    B --> C[Popup opens showing current tab]
    C --> D[Click 'Save for Later']

    D --> E[Tab closes immediately]
    E --> F[Item added to Saved tab]
    F --> G[No wake time set]

    G --> H[Item persists indefinitely]

    H --> I{User action}
    I -->|Open| J[Click Open button in Saved tab]
    I -->|Delete| K[Click Delete button]
    I -->|Nothing| L[Item stays in Saved]

    J --> M[Tab opens in browser]
    M --> N{Keep saved?}
    N -->|Yes| O[Item remains in Saved tab]
    N -->|Manual delete| P[User deletes from Saved]

    K --> Q[Item removed permanently]
```

## Saved vs Snoozed

```mermaid
flowchart LR
    subgraph Saved
        A[No wake time]
        B[Manual open only]
        C[Stays forever]
    end

    subgraph Snoozed
        D[Scheduled wake time]
        E[Auto-opens]
        F[Removed after wake]
    end
```

## Key Points

1. **No schedule** - Saved items don't have a wake time
2. **Manual only** - User decides when to open
3. **Persistent** - Items stay until manually deleted
4. **Perfect for** - Reference docs, tutorials, bookmarks
