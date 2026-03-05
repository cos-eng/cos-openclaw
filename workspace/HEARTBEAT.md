# HEARTBEAT.md — CoS Operational Rhythm

## Heartbeat Schedule

- **Frequency:** Every 30 minutes (08:01–23:00 IST)
- **Quiet Hours:** 23:00–07:00 IST (HEARTBEAT_OK unless urgent)

## On Every Heartbeat

Check in this order (rotate through, 2–4 checks per heartbeat):

1. **Unread messages** — Any new Google Chat messages from CEO?
2. **Calendar** — Upcoming meetings in next 2 hours? Prep needed?
3. **Drive inbox** — New files dropped in `/CoS-Shared/inbox/`?
4. **Mission Control** — Task status changes? Blockers reported?
5. **Memory update** — Anything to log in MEMORY.md?

## Proactive Triggers (Act Immediately)

- CEO message received → Process and respond/delegate
- Calendar event in < 2 hours → Trigger Intel Analyst for SCQA prep
- File dropped in Drive inbox → Trigger Operator for processing
- Task blocked > 48 hours → Escalate to CEO
- Client sentiment change detected → Alert CEO

## Cron Schedule (Off-Hours, Run by Orchestrator)

| Time (IST) | Cron | Agent | Output |
|------------|------|-------|--------|
| 2:00 AM | Client News Scan | Intel Analyst | Client intelligence for briefing §4 |
| 3:00 AM | LinkedIn Tracking | Intel Analyst | External intel for briefing §5 |
| 4:00 AM | Team Progress Sync | Intel Analyst | Team updates for briefing §3 |
| 5:00 AM | Calendar Prep | Intel Analyst | SCQA meeting prep for briefing §2 |
| 6:30 AM | Briefing Assembly | Orchestrator | Compile all outputs into Daily Briefing |
| 7:00 AM | Briefing Delivery | Orchestrator | Send to CEO via Google Chat + save to Drive |
| Every 6h | State Sync | Orchestrator | Commit MEMORY.md + dynamic files to GitHub |

## When to Reach Out

- Important/urgent email arrived
- Calendar event coming up (< 2 hours)
- Task completed that CEO is waiting on
- Blocker or escalation needed
- Client intelligence worth immediate attention

## When to Stay Quiet (HEARTBEAT_OK)

- Quiet hours (23:00–07:00) unless genuinely urgent
- CEO is in a meeting (check calendar)
- Nothing new since last check
- Last check was < 30 minutes ago

## Memory Maintenance

Every few heartbeats, review recent memory/ files and update MEMORY.md with distilled insights. Remove outdated info. MEMORY.md is curated wisdom, not raw logs.

**CRITICAL:** Update MEMORY.md after EVERY significant interaction — not just at session end. This includes CEO decisions, delegated tasks, project status changes, new context, and escalation outcomes. If the VM crashes, MEMORY.md is the recovery point.
