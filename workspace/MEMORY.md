# MEMORY.md — Active Context

## Last Updated: 2026-03-05T22:30:00+05:30

## Active Projects

_No active projects yet. First projects will be created when CEO Khilav delegates via Google Chat._

### Template for new projects

```text
### [Project Name] (SO-X)
- Status: Planning / In Progress / Review / Done
- Last Update: [date] — [summary]
- Blockers: [if any]
- Next Action: [what needs to happen]
- Owner: [team lead from ORG_CHART.md]
- Mission Control ID: [task ID]
- Linked SO: SO-X from SOUL.md
```

## Recent Decisions

_Log every CEO decision with date, rationale, and strategic impact._

```text
Format:
- [Date]: Decided to [X] because [Y]. Impact on [SO-Z]. Assigned to [person].
```

- 2026-03-05: CoS multi-agent system deployed to GCP VM. Gateway pairing resolved. All agent knowledge files deployed.

## Stakeholder Sentiment

_Track client relationship temperature. Cross-reference with CLIENT_STAKEHOLDERS.md._

| Client | Stakeholder | Sentiment | Last Contact | Notes |
|--------|------------|-----------|-------------|-------|
| _To be populated as interactions occur_ | | | | |

```text
Sentiment levels:
- Champion — actively advocates, strong relationship
- Neutral — standard engagement, no strong signal
- At Risk — delayed renewals, reduced engagement, negative signals
```

## Pending Approvals

_Items waiting for CEO sign-off. Clear these in Daily Briefing §1._

| Item | Context | Drive Link | Date Added |
|------|---------|-----------|-----------|
| _None currently_ | | | |

## Key Context

_Important context that persists across sessions. This is the recovery point if the VM crashes._

### System Configuration

- **CoS system live:** 2026-03-05
- **Primary model:** Google Gemini 2.5 Pro
- **Service account:** <cos@liftsuggest.com>
- **Gateway:** ws://127.0.0.1:18789 (loopback via Nginx)
- **Control UI:** <http://35.200.184.122:18789>
- **Mission Control:** <http://35.200.184.122:4000>
- **VM:** cos-vm (GCP e2-medium, asia-south1-a)
- **Gateway version:** OpenClaw 2026.3.3
- **Access restricted to:** 103.233.171.30/32 (Tatvic IP)

### Known Issues

- Google Chat 401 error — under separate investigation
- ORG_CHART.md, DIRECT_REPORTS.md, PROSPECT_LIST.md need CEO to populate with real data
- SOUL.md Strategic Objectives need validation from CEO (currently has inferred SOs)

### What Has Been Set Up

- ✅ All 4 agents configured (Orchestrator, Intel Analyst, Operator, Ghostwriter)
- ✅ Firewall rules restricted to Tatvic home IP
- ✅ Gateway pairing resolved
- ✅ Knowledge files deployed (CLIENT_LIST.md, CLIENT_STAKEHOLDERS.md)
- ✅ Template files deployed (ORG_CHART.md, DIRECT_REPORTS.md, PROSPECT_LIST.md)
- ⬜ Google Chat integration (pending 401 fix)
- ⬜ Daily Briefing cron schedule (pending Chat integration)
- ⬜ Mission Control task board setup
- ⬜ GOG CLI configuration
- ⬜ State sync to GitHub

## Lessons Learned

_Things that worked, things that didn't. Update after significant events._

- Gateway pairing error resolved by restarting the gateway container after approving pairing in UI
- Rate limit on auth attempts triggered by repeated connection attempts — gateway restart clears it
- `dangerouslyDisableDeviceAuth: true` only affects browser UI connections, not agent-gateway WebSocket
- File ownership on VM must be `ubuntu:ubuntu` for the container to read them (Docker user mapping)

## Update Rules

**CRITICAL:** Update this file after EVERY significant interaction. This includes:

- CEO decisions (with rationale)
- Delegated tasks and their status
- Project status changes
- New context learned
- Escalation outcomes
- Client sentiment shifts
- System configuration changes

If the VM crashes, MEMORY.md is the recovery point. Keep it current.
