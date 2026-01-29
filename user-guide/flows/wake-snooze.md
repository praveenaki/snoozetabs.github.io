# Wake Snooze Flow

How snoozes wake up and return tabs.

```mermaid
flowchart TD
    A[Scheduled time arrives] --> B{Browser open?}

    B -->|Yes| C{Within grace period?}
    B -->|No| D[Wait for browser to open]

    D --> E{Browser opened}
    E --> C

    C -->|Yes - within 15 min| F[Auto-wake]
    C -->|No - past grace period| G[Mark as Missed]

    F --> H[Tab opens in browser]
    H --> I{Multiple tabs?}
    I -->|Yes| J[All tabs open]
    I -->|No| K[Single tab opens]

    J --> L{Show notification?}
    K --> L

    L -->|Enabled| M[System notification shown]
    L -->|Disabled| N[Silent wake]

    M --> O{Recurring snooze?}
    N --> O

    O -->|No| P[Snooze complete, removed]
    O -->|Yes| Q[Reschedule for next occurrence]

    G --> R[Shows in Sleeping tab as Missed]
    R --> S[User can manually wake]
    S --> H
```

## Grace Period

| Time past scheduled | Action |
|---------------------|--------|
| 0-15 minutes | Auto-wake |
| 15 min - 7 days | Marked as Missed |
| 7+ days | Expired (auto-deleted) |

## Key Points

1. **Auto-wake** - Tabs open automatically within grace period
2. **Missed snoozes** - Require manual wake
3. **Notifications** - Optional system notifications
4. **Recurring** - Auto-reschedule after wake
