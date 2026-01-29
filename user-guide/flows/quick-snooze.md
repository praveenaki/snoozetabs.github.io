# Quick Snooze Flow

How the preset button snooze flow works.

```mermaid
flowchart TD
    A[User has a tab open] --> B[Click Snooze Tabs icon]
    B --> C[Popup opens showing current tab]
    C --> D{Choose action}

    D -->|Quick snooze| E[Click preset button]
    E --> F{Which preset?}
    F -->|Later Today| G[+15 min]
    F -->|This Evening| H[Today 6 PM]
    F -->|Tomorrow| I[Tomorrow 8 AM]
    F -->|This Weekend| J[Saturday 10 AM]
    F -->|Next Week| K[Monday 8 AM]
    F -->|Next Month| L[1st of next month]

    G --> M[Tab closes]
    H --> M
    I --> M
    J --> M
    K --> M
    L --> M

    M --> N[Snooze created in Sleeping tab]
    N --> O[Popup stays open for next tab]

    D -->|Save| P[Click Save for Later]
    P --> Q[Tab closes]
    Q --> R[Item added to Saved tab]
    R --> O

    D -->|Custom time| S[Click 'Pick a date & time']
    S --> T[See custom-snooze flow]
```

## Key Points

1. **Preset buttons** - One click creates snooze with calculated time
2. **Tab closes** - Immediately after clicking
3. **Popup stays open** - Process multiple tabs quickly
4. **Badge updates** - Sleeping tab shows count
