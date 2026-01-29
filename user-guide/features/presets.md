# Quick Snooze Presets

Snooze tabs instantly with one click using pre-configured time presets.

## Available Presets

| Preset | When it wakes | Best for |
|--------|---------------|----------|
| **Later Today** | Current time + 15 min (configurable) | Quick break, meeting ends soon |
| **This Evening** | Today at 6:00 PM (configurable) | After work reading |
| **Tomorrow** | Tomorrow at 8:00 AM (configurable) | Next day tasks |
| **Tomorrow Evening** | Tomorrow at 6:00 PM | End of next day |
| **This Weekend** | Saturday at 10:00 AM (configurable) | Weekend reading |
| **Next Week** | Monday at 8:00 AM (configurable) | Next week tasks |
| **Next Month** | 1st of next month | Long-term items |

## How Presets Work

Each preset calculates a wake time based on:
1. **Current time** - When you click the button
2. **Your settings** - Customizable start/end times
3. **Smart scheduling** - Won't schedule in the past

### Example: "This Evening"
- If it's 2:00 PM → Wakes at 6:00 PM today
- If it's 7:00 PM → Wakes at 6:00 PM tomorrow (skips past time)

### Example: "This Weekend"
- If it's Wednesday → Wakes Saturday 10:00 AM
- If it's Saturday afternoon → Wakes next Saturday

## Keyboard Shortcuts

Skip the popup entirely with these shortcuts:

| Shortcut | Action |
|----------|--------|
| `Alt+Shift+S` | Later Today |
| `Alt+Shift+E` | This Evening |
| `Alt+Shift+T` | Tomorrow |
| `Alt+Shift+W` | This Weekend |

*On Mac, use `Ctrl+Shift` instead of `Alt+Shift`*

## Customizing Presets

Go to **Settings** to adjust default times:

| Setting | Default | Affects |
|---------|---------|---------|
| Start of day | 8:00 AM | Tomorrow, Next Week |
| End of day | 6:00 PM | This Evening, Tomorrow Evening |
| Later Today | 15 minutes | Later Today |
| Weekend morning | 10:00 AM | This Weekend |
| Week starts on | Monday | Next Week |
| Weekend starts on | Saturday | This Weekend |

## Tips

1. **Use keyboard shortcuts** for tabs you process frequently
2. **Customize times** to match your actual schedule
3. **"Later Today"** is great for meeting tabs you'll need after a break
4. **"This Weekend"** works well for articles and long reads

## Related

- [Custom Date & Time](custom-picker.md) - For specific scheduling
- [Settings](settings.md) - Customize preset times
- [Keyboard Shortcuts](keyboard-shortcuts.md) - Full shortcut reference
