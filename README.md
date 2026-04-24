# AI Chief of Staff

A personal task management system built on [Claude Code](https://claude.ai/claude-code) slash commands and [Obsidian](https://obsidian.md). Designed for people who run too many things in parallel and need a system with teeth — not just capture, but forced prioritisation.

## The Problem

Most task systems are capture tools pretending to be productivity tools. You dump everything in, feel organised for 20 minutes, then drown in a flat list of 47 items with no signal about what actually matters.

This system is different:

- **Hard cap of 5 active deep work items.** No exceptions. To add a 6th, you demote one first.
- **Voice capture from anywhere** — "Hey Siri, add 'call the accountant' to my Capture list" lands in Apple Reminders, gets pulled into your task list during morning sync.
- **Calendar-aware planning** — sees your actual day, suggests focus blocks, flags when you're kidding yourself about available time.
- **Weekly capacity audit** — names the context switching tax directly. Running 12 things? Your effective deep work hours are 10-15 per week. That's 1.5 hours per item. Is that enough?

## What You Get

Three Claude Code slash commands:

| Command | What it does |
|---------|-------------|
| `/capture [thing]` | Zero friction capture. Lands in Quick Tasks (default) or Holding (prefix with `deep:`). No questions asked. |
| `/daily-sync` | Morning focus session. Reads your tasks + calendar + Apple Reminders. Drains the capture buffer. Suggests today's focus. Offers to block deep work time. |
| `/weekly-plan` | Weekly review. What moved, what's stuck. Enforces the cap. Archives done items. Sets next week's intentions. |

Plus a task list template for Obsidian:

```
## Active Deep Work (max 5)    ← the hard cap
## Quick Tasks                  ← small stuff, do between meetings
## Holding                      ← big items waiting their turn
## Recurring                    ← weekly/monthly items that auto-surface
## Done (this week)             ← cleared on weekly review
```

## Prerequisites

- [Claude Code](https://claude.ai/claude-code) (Anthropic's CLI)
- [Obsidian](https://obsidian.md) with the [Obsidian MCP](https://github.com/MarkusPfworflmüller/obsidian-mcp) server configured
- Google Calendar MCP (optional, for calendar integration)
- macOS (for Apple Reminders / Siri voice capture)

## Installation

### 1. Copy the commands

```bash
# From your Obsidian vault root (or any Claude Code project):
mkdir -p .claude/commands
cp .claude/commands/capture.md     YOUR_PROJECT/.claude/commands/
cp .claude/commands/daily-sync.md  YOUR_PROJECT/.claude/commands/
cp .claude/commands/weekly-plan.md YOUR_PROJECT/.claude/commands/
```

### 2. Create your task list

Copy `templates/Tasks.md` to wherever you keep area notes in your Obsidian vault (e.g. `02_Areas/Tasks.md`).

Update the file paths in each command if your location differs from `02_Areas/Tasks.md`.

### 3. Set up Apple Reminders (optional)

Create a Reminders list called **"Capture"** on your Mac or iPhone. The `/daily-sync` command reads from this list and imports items into your task list.

To capture from anywhere:
- **Siri:** "Hey Siri, add 'book dentist' to my Capture list"
- **iPhone/Watch:** Open Reminders → Capture list → add item
- **Mac:** Reminders app → Capture list → add item

### 4. Configure MCP servers

The commands use these MCP integrations:

- **Obsidian MCP** — reads and writes your task list (`mcp__obsidian__read_note`, `mcp__obsidian__patch_note`, `mcp__obsidian__write_note`)
- **Google Calendar MCP** — reads events and creates focus blocks (`mcp__claude_ai_Google_Calendar__list_events`, `mcp__claude_ai_Google_Calendar__create_event`)

Configure these in your Claude Code MCP settings. The commands still work without Calendar MCP — you just lose the calendar-aware features.

## How It Works

### The Daily Loop

```
Morning:    /daily-sync     → drain Reminders, see your day, pick focus
During day: /capture [x]    → zero friction capture (or Siri → Reminders)
```

### The Weekly Loop

```
Friday/Sunday: /weekly-plan → review, archive, set next week's intentions
```

### Recurring Tasks

Add items to the `## Recurring` section with a frequency prefix:

```markdown
- [ ] weekly: Review job application pipeline
- [ ] monthly: Review finances and runway
- [ ] fortnightly: Catch up with mentor
```

`/daily-sync` checks each morning and auto-adds due items to Quick Tasks. `/weekly-plan` reviews whether recurring items are still relevant.

### Task Dependencies

Add `→ blocked-by: [thing]` to any task that can't start yet:

```markdown
- [ ] List house in June → blocked-by: decorator work
- [ ] Submit application → blocked-by: CV review
```

`/daily-sync` skips blocked items when suggesting focus. When a blocker is completed, it flags newly unblocked items. `/weekly-plan` shows a dependency view and flags items blocked for >2 weeks.

### The Rules

1. **Active Deep Work is capped at 5.** This is not a suggestion. The system enforces it.
2. **New items land in Quick Tasks or Holding.** You earn your way into Active during `/daily-sync` or `/weekly-plan`.
3. **Done gets cleared weekly.** Archived to a weekly review note.
4. **Context switching tax is named directly.** 3-4 parallel streams = 20-30% overhead. 5+ = 40%+. The system will tell you.
5. **Blocked tasks are skipped.** Don't suggest work that can't move. Surface it when the blocker resolves.
6. **Recurring items auto-surface.** No manual re-entry for weekly/monthly tasks.

## Customisation

- **Change the cap:** Edit the number in `Tasks.md` rules and in each command file. But consider whether you actually need more, or whether you're avoiding the hard choice.
- **Different vault structure:** Update the file paths in each `.md` command file.
- **No Obsidian:** Adapt the commands to use file system reads/writes instead of MCP. The logic is the same.
- **No Apple Reminders:** The daily-sync falls back to asking you directly. The Reminders drain step is skipped if the list is empty or doesn't exist.

## Philosophy

This system is inspired by Cal Newport's Slow Productivity and the "AI Chief of Staff" concept. The key insight: **the bottleneck isn't capture, it's prioritisation.** Most people don't need a better inbox — they need a system that forces them to choose what matters and makes the cost of overcommitment visible.

The hard cap is the feature, not the limitation.

## License

MIT — use it, fork it, adapt it.
