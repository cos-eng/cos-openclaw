# TOOLS.md — Intel Analyst Tool Reference

## Research Tools

### SearchAPI.io (PRIMARY Search Method)

**Use `bash_shell` with `curl` and SearchAPI for ALL search queries.** This gives you real Google search results. The API key is available as env var `$SEARCHAPI_API_KEY`.

```bash
# PRIMARY METHOD — Google Search via SearchAPI (ALWAYS use this first)
curl -s "https://www.searchapi.io/api/v1/search?engine=google&q=QUERY+TERMS+HERE&api_key=$SEARCHAPI_API_KEY" | python3 -c "
import sys, json
data = json.load(sys.stdin)
for r in data.get('organic_results', [])[:5]:
    print(f\"- {r['title']}\")
    print(f\"  {r['link']}\")
    print(f\"  {r.get('snippet', '')}\")
    print()
"

# Google News search
curl -s "https://www.searchapi.io/api/v1/search?engine=google_news&q=QUERY+TERMS&api_key=$SEARCHAPI_API_KEY" | python3 -c "
import sys, json
data = json.load(sys.stdin)
for r in data.get('news_results', [])[:5]:
    print(f\"- {r.get('title','')}\")
    print(f\"  {r.get('link','')}\")
    print()
"
```

### web_fetch (For reading article content AFTER finding URLs)

Use `web_fetch` to read full article content from URLs found via SearchAPI:

```text
# Read a specific article
web_fetch("https://economictimes.com/industry/auto/actual-article-url")

# Company pages
web_fetch("https://www.COMPANY.com/investors/")
web_fetch("https://www.COMPANY.com/newsroom/")
```

> ⚠️ **Do NOT use `web_fetch` for searching** — Google News URLs return redirects that don't work. Use SearchAPI via `bash_shell` instead.

**Rules:**

- ALWAYS use `web_fetch` as the FIRST attempt for any URL
- ALWAYS verify URLs before citing them
- ALWAYS include source URLs in BLUF output
- If `web_fetch` returns 403 or "Just a moment..." → follow the **Fallback Chain**

### Research Fallback Chain (MANDATORY)

Most Indian enterprise sites (HDFC, Bajaj Finance, Reliance) use Cloudflare/WAF. Follow this chain **in order**:

```text
Step 1: web_fetch(URL) → Try first (fast)
  ↓ If 403 / "Just a moment..." / empty
Step 2: browser tool → Headless Chromium (bypasses JS challenges)
  ↓ If browser fails
Step 3: bash_shell + curl with User-Agent
  ↓ If still blocked
Step 4: Google Cache / News snippets / Archive.org
```

**Step 3 example (bash_shell):**

```bash
curl -s -L -A "Mozilla/5.0 (X11; Linux x86_64) Chrome/145.0" "https://www.example.com" | head -1000
```

**Step 4 alternatives:**

```text
web_fetch("https://webcache.googleusercontent.com/search?q=cache:example.com")
web_fetch("https://news.google.com/search?q=COMPANY+NAME")
web_fetch("https://web.archive.org/web/2026/https://example.com")
```

> **⚠️ NEVER give up after just web_fetch failing.** Always try at least Steps 1-3.

### Playwright Headless Browser

OpenClaw's built-in Playwright browser for JavaScript-rendered content and Cloudflare-protected sites.

**MANDATORY for:**

- Cloudflare-protected sites (web_fetch returns 403 / "Just a moment...")
- LinkedIn profile scraping (LinkedIn requires JS rendering)
- Dynamic dashboards and SPA pages
- Interactive/login-gated content
- Screenshot capture for evidence

**Config:** `browser.enabled: true`, `browser.headless: true` in `openclaw.json`.

**DO NOT use browser for:** Static pages, news articles, SEC filings — use `web_fetch` instead (faster, lighter).

---

## CLI Tools (Available Inside Docker Container)

### GOG CLI — Google Workspace Access

Authenticated access via `cos@liftsuggest.com`.

| Service | Key Commands | Intel Analyst Use Case |
|---------|-------------|----------------------|
| **Calendar** | `gog calendar list --days=1` | Pull meetings for SCQA prep |
| **Drive** | `gog drive list --folder=X`, `gog drive download --file-id=X` | Read CEO-dropped files for analysis |
| **Contacts** | `gog contacts search --query=X` | Look up stakeholder details |

**Note:** You primarily READ data. Writing/sending is the Orchestrator's job.

### GH CLI — GitHub Access

| Operation | Command | Use Case |
|-----------|---------|----------|
| Read file | `gh api repos/cos-eng/cos-workspace/contents/{path}` | Read skills, templates |

---

## Mission Control API

| Endpoint | Method | Intel Analyst Use Case |
|----------|--------|----------------------|
| `/api/tasks` | GET | Read all tasks for team progress sync (SOP 4) |
| `/api/tasks/{id}/activities` | POST | Log research progress |
| `/api/tasks/{id}/deliverables` | POST | Register completed intel reports |

---

## Infrastructure Reference

| Component | Detail |
|-----------|--------|
| **VM** | `cos-vm` — GCP e2-medium, asia-south1-a, Ubuntu 24.04 LTS |
| **LLM** | Google Gemini 2.5 Pro |
| **Service Account** | `cos@liftsuggest.com` |
| **Docker Network** | `cos-network` (internal bridge) |
