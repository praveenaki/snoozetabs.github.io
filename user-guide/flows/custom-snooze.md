# Custom Snooze Flow

How the custom date/time picker flow works.

```mermaid
flowchart TD
    A[Click 'Pick a date & time'] --> B[Custom picker expands]
    B --> C[Select date from calendar]
    C --> D[Select time]
    D --> E{Enable Repeat?}

    E -->|No| F[One-time snooze]
    E -->|Yes - PRO| G[Configure repeat]

    G --> H{Interval?}
    H -->|Daily| I[Set daily time]
    H -->|Weekly| J[Select days + time]
    H -->|Monthly| K[Select day of month]
    H -->|Yearly| L[Select date]

    I --> M[Repeat config set]
    J --> M
    K --> M
    L --> M

    F --> N[Click Snooze button]
    M --> N

    N --> O{Valid?}
    O -->|Yes| P[Tab closes]
    O -->|No - past time| Q[Show error, stay open]

    P --> R[Snooze created]
    R --> S{Recurring?}
    S -->|No| T[One-time snooze in Sleeping tab]
    S -->|Yes| U[Recurring snooze with repeat icon]
```

## Key Points

1. **Date/Time picker** - Select any future date and time
2. **Repeat option** - PRO feature for recurring snoozes
3. **Validation** - Can't schedule in the past
4. **Recurring indicator** - Shows repeat icon in Sleeping tab
