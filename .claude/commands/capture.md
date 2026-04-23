---
description: Capture a task to your todo list — zero friction, one line
argument-hint: the task to capture (prefix with "deep:" for multi-day work)
allowed-tools: [mcp__obsidian__read_note, mcp__obsidian__patch_note]
---

# Capture

Quick capture — add a task to Tasks.md with zero friction.

**Input:** $ARGUMENTS

## Process

1. Read `02_Areas/Tasks.md` using `mcp__obsidian__read_note`

2. Determine where it goes:
   - If `$ARGUMENTS` starts with "deep:" → strip the prefix, add to **Holding** (not Active — you earn Active during `/daily-sync` or `/weekly-plan`)
   - Otherwise → add to **Quick Tasks**

3. Append a new checkbox line to the appropriate section:
   ```
   - [ ] {today's date} — $ARGUMENTS
   ```

4. Write the updated note back using `mcp__obsidian__patch_note`

5. Confirm to the user in ONE line:
   - "Captured → Quick Tasks: [task]"
   - or "Captured → Holding: [task]"

## Rules

- **No follow-up questions.** Capture and confirm. That's it.
- **Do not reorganise** the rest of Tasks.md. Only append.
- **Do not ask** whether it should be Quick Tasks or Holding unless genuinely ambiguous. Default to Quick Tasks.
- If Active Deep Work already has 5 items, do NOT add to Active. Mention this only if the user explicitly asks to add something to Active.
