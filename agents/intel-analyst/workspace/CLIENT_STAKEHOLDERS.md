# CLIENT_STAKEHOLDERS.md — Key Contacts

## Last Updated: 2026-03-05

| Client | Name | Designation | Stakeholder Role | Company Website URL | LinkedIn URL | Tatvic Account Manager | Sentiment | Last Contact |
|--------|------|-------------|-----------------|---------------------|-------------|----------------------|-----------|-------------|
| TVS Motor | Adarsh Kumar | Chief Digital & AI Officer - Retail Mobility - D&AI | Final Decision Maker | <https://www.tvsmotor.com/> | <https://www.linkedin.com/in/adarsh-kumar-tbx/> | Rikita Shukla | — | — |
| RoyalEnfield | Jatin Chhikara | Global Head - Marketing | Final Decision Maker | <https://www.royalenfield.com/> | <https://www.linkedin.com/in/jatin-chhikara-65036165/> | Neha Singh | — | — |

## Column Definitions

| Column | Purpose | Used By |
|--------|---------|---------|
| `Client` | Company name (matches CLIENT_LIST.md entries) | Intel Analyst — cross-referencing |
| `Name` | Stakeholder's full name | Encoder — registered as known person |
| `Designation` | Their role/title at the company | Intel Analyst — context in briefings |
| `Stakeholder Role` | Decision authority: `Final Decision Maker` / `Influencer to decisions` | Orchestrator — prioritization |
| `Company Website URL` | Client's homepage | Intel Analyst — web scraping |
| `LinkedIn URL` | Stakeholder's LinkedIn profile | Intel Analyst — LinkedIn tracking cron |
| `Tatvic Account Manager` | Internal account owner | Orchestrator — routing internal queries |
| `Sentiment` | Relationship temperature: Champion / Neutral / At Risk | Orchestrator — strategic decisions |
| `Last Contact` | Date of most recent interaction | Orchestrator — follow-up scheduling |

## Update Rules

- Update `Sentiment` after every client interaction
- Update `Last Contact` after every meeting or significant communication
- Add new stakeholders when discovered during meetings or research
- Source: [Client Stakeholder Database](https://docs.google.com/document/d/1icxuGakG6rp2uTSSe0HiXIDMyx5DMRFZniWNzvEiIrE/edit?tab=t.0)
