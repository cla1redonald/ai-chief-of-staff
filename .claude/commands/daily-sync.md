---
description: Morning focus session — read tasks + calendar, plan your day
argument-hint: (no arguments needed)
allowed-tools: [Bash, mcp__obsidian__read_note, mcp__obsidian__patch_note, mcp__obsidian__write_note, mcp__claude_ai_Google_Calendar__list_events, mcp__claude_ai_Google_Calendar__create_event, mcp__claude_ai_Google_Calendar__list_calendars, mcp__claude_ai_Google_Calendar__suggest_time]
---

# Daily Sync

Morning focus session. Read your tasks and calendar, decide what matters today.

## Process

### 1. Read the current state

- Read `02_Areas/Tasks.md` using `mcp__obsidian__read_note`
- List today's calendar events using `mcp__claude_ai_Google_Calendar__list_events` (today's date, all calendars)
- If this is the first run, also call `mcp__claude_ai_Google_Calendar__list_calendars` to identify which calendars are active

### 2. Show the dashboard

Present a concise summary:

**Calendar today:**
- List events with times (meetings, calls, commitments)
- Flag gaps where deep work could happen

**Active Deep Work ({count}/5):**
- List all items with a quick status check
- If >5: "You're over the cap. What gets demoted?"
- If ≤3: "Good focus. You have headroom."

**Quick Tasks:**
- List items, flag any that are time-sensitive (today/this week)

### 3. Drain the Apple Reminders capture buffer

Run this via `Bash` to pull uncompleted items from the "Capture" Reminders list:

```bash
osascript -e '
tell application "Reminders"
  set output to ""
  set captureList to list "Capture"
  repeat with r in (every reminder of captureList whose completed is false)
    set output to output & name of r & linefeed
  end repeat
  return output
end tell'
```

**If items exist:**
- Show them: "These came in from your phone/Siri:"
- For each item, add to Quick Tasks in Tasks.md (default) or Holding if clearly multi-day work
- After importing, mark each as complete in Reminders:

```bash
osascript -e '
tell application "Reminders"
  set captureList to list "Capture"
  repeat with r in (every reminder of captureList whose completed is false)
    set completed of r to true
  end repeat
end tell'
```

- Confirm: "Imported 3 items from Reminders → Quick Tasks"

**If no items:** move on silently.

Then ask: **"Anything else in your head to capture before we plan?"**

If the user shares items:
- Add each to Quick Tasks or Holding in Tasks.md
- Confirm each one briefly

If nothing: move on.

### 4. Suggest today's focus

Based on calendar gaps and task priorities, suggest:
- **Deep Work block:** Which 1-2 Active items to progress today, and when (based on calendar gaps)
- **Quick wins:** Which Quick Tasks to knock off between meetings
- **Skip today:** What can wait until tomorrow

Keep suggestions to 3-5 items max. Don't overwhelm.

### 5. Offer calendar blocking

Ask: **"Want me to block deep work time on your calendar?"**

If yes:
- Use `mcp__claude_ai_Google_Calendar__create_event` to create a focus block
- Title: "Deep Work: [task name]"
- Description: Brief context from Tasks.md
- Duration: suggest 90-120 min blocks

### 6. Offer breakdown help

Ask: **"Any of these feel too vague or too big? Want me to help break one down?"**

If yes: help decompose the task into concrete next steps, update Tasks.md with the breakdown.

If no: wrap up with a one-line summary of today's plan.

## Tone

- Concise, not chatty
- Suggest, don't lecture
- Respect the hard cap — it's the point of the system
- If Claire has too many things active, name it directly: "You're running 7 deep work items. The cap is 5. What moves to Holding?"
