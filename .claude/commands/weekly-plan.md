---
description: Weekly review — what moved, what's stuck, plan next week
argument-hint: (no arguments needed)
allowed-tools: [Bash, mcp__obsidian__read_note, mcp__obsidian__write_note, mcp__obsidian__patch_note, mcp__claude_ai_Google_Calendar__list_events, mcp__claude_ai_Google_Calendar__create_event, mcp__claude_ai_Google_Calendar__suggest_time]
---

# Weekly Plan

Weekly review and planning session. Look back at what moved, look forward at what matters.

## Process

### 1. Gather state

- Read `02_Areas/Tasks.md` using `mcp__obsidian__read_note`
- List this week's calendar events (Monday to Sunday) using `mcp__claude_ai_Google_Calendar__list_events`
- List next week's calendar events for forward planning

### 2. Review: Done

Show everything in the Done section.

Ask:
- "Anything missing from Done that you actually completed this week?"
- Add any mentioned items.

Observe patterns: "You completed 3 Quick Tasks but no Deep Work items moved — is that a focus issue or were you blocked?"

### 3. Review: Active Deep Work

For each Active item:
- How long has it been active? (check the date if present)
- Did it move forward this week?

Flag items stuck for >1 week. Ask for each:
- "Still the right priority? Keep active, demote to Holding, or break down further?"

### 4. Review: Holding

Show Holding items. Ask:
- "Anything here ready to promote to Active?" (enforce the 5-item cap)
- "Anything to kill or delegate?"
- "Any new deadlines that change priority?"

### 5. Review: Quick Tasks

Flag any Quick Tasks older than 1 week. Ask:
- "These have been sitting here a while — do them, delegate them, or kill them?"

### 6. Capacity check

Reference the capacity-audit logic:
- How many parallel streams are active?
- Context switching tax estimate (3-4 streams = 20-30%, 5+ = 40%+)
- Flag if total active commitments exceed sustainable capacity

Be direct: "You have 12 things in flight. Your effective deep work hours are probably 10-15 per week after switching costs. That's 2-3 hours per item. Is that enough to make real progress?"

### 7. Set next week's intentions

Ask: "Which 3-5 things would make next week a success?"

Update Active Deep Work accordingly (enforcing the cap).

### 8. Archive Done

Create a weekly archive note at `02_Areas/Weekly_Reviews/Week_of_{date}.md` with:
- Completed items
- Key decisions made
- Items promoted/demoted
- Next week's intentions

Clear the Done section in Tasks.md.

### 9. Offer calendar blocking

Show next week's calendar. Ask:
- "Want me to block deep work time for your Active items?"
- Suggest specific slots based on calendar gaps
- Create events via `mcp__claude_ai_Google_Calendar__create_event`

## Tone

- Honest, not cheerful. If nothing moved, say so.
- The hard cap is non-negotiable. Don't let Claire add a 6th item without demoting one.
- Name the context switching tax directly — Claire knows she runs too many things in parallel. The system's job is to make that visible.
- End with clarity: "Here's your week. 5 deep work items. Go."
