# Snooze Tabs User Guide

> Master tab management: snooze tabs for later, save articles to read, build daily routines.

## Quick Start

1. **Click the Snooze Tabs icon** in your browser toolbar
2. **Pick when you want the tab back**:
   - Click a preset button (Tomorrow, This Evening, etc.)
   - Or click "Pick a date & time" for custom scheduling
3. **Your tab closes** and reappears when the time comes

That's it! Your tab will automatically open when scheduled.

---

## What Can You Do?

| I want to... | Use this feature | Time to learn |
| --- | --- | --- |
| Close a tab and get it back tomorrow | [Quick Snooze Presets](features/presets.md) | 30 seconds |
| Save an article to read "someday" | [Save for Later](features/save-for-later.md) | 1 minute |
| Open my standup page every morning | [Recurring Snoozes](features/recurring.md) | 2 minutes |
| Separate work tabs from personal | [Workspaces](features/workspaces.md) | 2 minutes |
| Access snoozes on another computer | [Google Drive Sync](features/sync.md) | 2 minutes |

---

## Features

### Core Features (Free)

- [Quick Snooze Presets](features/presets.md) - One-click snoozing with 7 preset times
- [Custom Date & Time](features/custom-picker.md) - Schedule tabs for any specific moment
- [Save for Later](features/save-for-later.md) - Bookmark tabs without a schedule
- [Keyboard Shortcuts](features/keyboard-shortcuts.md) - Snooze without opening the popup
- [Settings](features/settings.md) - Customize times, notifications, and more

### PRO Features

- [Recurring Snoozes](features/recurring.md) - Daily, weekly, monthly, yearly schedules
- [Workspaces](features/workspaces.md) - Organize snoozes into categories
- [Google Drive Sync](features/sync.md) - Cross-device backup and sync

---

## Use Cases

Real-world scenarios with step-by-step guides:

| Scenario | Description |
| --- | --- |
| [Tab Overwhelm](use-cases/tab-overwhelm.md) | "I have 50 tabs open and can't think" |
| [Research Mode](use-cases/research-mode.md) | "I keep finding articles but never read them" |
| [Daily Routines](use-cases/daily-routines.md) | "I need the same pages every morning" |
| [Project Organization](use-cases/project-organization.md) | "Work and personal tabs are mixed up" |

---

## The Popup at a Glance

The popup has 4 tabs:

| Tab | Purpose |
| --- | --- |
| **New Snooze** | Create snoozes and save tabs |
| **Sleeping** | View scheduled snoozes (badge shows count) |
| **Saved** | View saved-for-later items |
| **Settings** | Customize behavior |

### Snooze States

| State | Meaning | What happens |
| --- | --- | --- |
| **Sleeping** | Waiting for scheduled time | Auto-opens when time comes |
| **Missed** | Past grace period (15 min) | Manual wake required |
| **Saved** | No schedule | Open manually when ready |

---

## Snooze vs Save: When to Use Which

```mermaid
flowchart TD
    A[Tab to process] --> B{Does it have a natural 'when'?}

    B -->|Yes - tomorrow, weekend, etc.| C[SNOOZE IT]
    B -->|No - reference material| D[SAVE IT]

    C --> E[Tab returns automatically]
    D --> F[Access anytime from Saved tab]
```

**Snooze:** News, articles to read once, meeting links, time-sensitive content

**Save:** Documentation, API references, tutorials you'll revisit, Stack Overflow answers

---

## Tips & Tricks

### Power User Tips

1. **Use keyboard shortcuts** - `Alt+Shift+T` snoozes to tomorrow instantly
2. **Snooze all tabs** - Clear an entire window at once
3. **Custom defaults** - Change preset times in Settings
4. **Weekend start** - Set Friday as weekend for earlier "This Weekend"

### Common Questions

**Q: What if I close the browser before a snooze wakes?**
A: The tab opens next time you open your browser (within grace period).

**Q: Can I snooze chrome:// pages?**
A: No, browser internal pages can't be snoozed. Only web pages (http/https).

**Q: Where are my snoozes stored?**
A: Locally in Chrome storage. With PRO, sync to Google Drive.

---

## Getting Help

- **Website:** [snoozetabs.com](https://snoozetabs.com)
- **Email:** support@snoozetabs.com
