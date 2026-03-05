# TOOLS.md — CoS Environment Notes

## CLI Tools (Inside Docker Container)

### GOG CLI (Google CLI for OpenClaw)

Provides authenticated access to Google Workspace via `cos@liftsuggest.com`.

| Service | Commands | Use Case |
|---------|----------|----------|
| Gmail | `gog gmail list`, `gog gmail read`, `gog gmail send` | Inbox summary, send internal updates |
| Calendar | `gog calendar list`, `gog calendar create` | Daily meetings, scheduling |
| Drive | `gog drive list`, `gog drive upload`, `gog drive download` | Deliverables, file drops, drafts |
| Chat | `gog chat send`, `gog chat spaces` | Daily Briefing, notifications, CEO directives |

**Auth:** OAuth tokens in encrypted keyring (`GOG_KEYRING_PASSWORD`).
**Account:** `cos@liftsuggest.com` — NOT CEO's personal account.
**Delegated Access:** CEO's calendar (read/write), CEO's Drive (read/write), CEO's Gmail (read-only).

### GH CLI (GitHub CLI)

Provides access to GitHub repos via `GH_TOKEN`.

| Operation | Command | Use Case |
|-----------|---------|----------|
| Read content | `gh api repos/{owner}/{repo}/contents/{path}` | Read skills, templates |
| Create issues | `gh issue create` | Track bugs, feature requests |
| List PRs | `gh pr list` | Monitor open PRs |
| Clone/pull | `gh repo clone` | Sync workspace |

**Repos:**

- `cos-eng/cos-openclaw` — Gateway config, agents, workspace (this repo)
- `cos-eng/cos-workspace` — Skills, docs, templates, synced state

### OpenClaw Native Browser

Built-in headless browser for web scraping and dynamic content.

- Used by Intel Analyst for LinkedIn tracking, news scraping
- Accessed via OpenClaw's browser service (not Playwright)
- Config in `openclaw.json`: `browser.enabled: true`

## Infrastructure

| Component | Detail |
|-----------|--------|
| VM | `cos-vm` — GCP e2-medium, asia-south1-a |
| Gateway | Port 18789 (token-protected) |
| Mission Control | Port 4000 (Tatvic IP restricted) |
| Docker Network | `cos-network` (internal bridge) |
| LLM | Google Gemini 2.5 Pro (primary) |
| Service Account | <cos@liftsuggest.com> |

## Google Drive Structure

```text
/CoS-Shared/
├── inbox/      ← CEO drops files here for processing
├── data/       ← Operator outputs (charts, pivots, analysis)
├── drafts/     ← Ghostwriter staged content for CEO review
├── briefings/  ← Daily Briefing archives
├── charters/   ← Project charter documents
└── reports/    ← Intel Analyst research outputs
```

## Mission Control API

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/tasks` | POST | Create task from CEO directive |
| `/api/tasks/{id}` | PATCH | Update task status |
| `/api/tasks/{id}/activities` | POST | Log progress |
| `/api/tasks/{id}/deliverables` | POST | Register completed work |
| `/api/tasks/{id}/subagent` | POST | Register spawned sub-agent |
| `/api/tasks` | GET | Read all tasks (for team sync) |
| `/api/files/upload` | POST | Upload files |
