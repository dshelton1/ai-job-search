# Search Queries for Job Scraper

<!-- SETUP: Customize these queries based on your skills, target roles, and location -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

## Search Sites

Primary (your market's job boards - scaffold one with `/add-portal`):
- **usajobs.gov** - federal government jobs (no CLI installed yet; use WebSearch/`site:` fallback below, or run `/add-portal` to scaffold a CLI)
- **linkedin.com/jobs** - LinkedIn job listings (filter: United States / Washington, D.C.); also covered by `linkedin-search` CLI
- **indeed.com** - general job board (no CLI installed; WebSearch/`site:` fallback)
- **glassdoor.com** - general job board with company reviews (no CLI installed; WebSearch/`site:` fallback)
- **ziprecruiter.com** - general job board (no CLI installed; WebSearch/`site:` fallback)

Note: only `linkedin-search` and `freehire-search` CLIs are currently installed under `.agents/skills/`. USAJobs, Indeed, Glassdoor, and ZipRecruiter have no dedicated CLI yet - `/scrape` will fall back to WebSearch with the `site:` queries below for these. Run `/add-portal` if you want a dedicated CLI scaffolded for any of them.

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies (open search - no specific target company list)

## Query Categories

Queries are grouped by priority. Each query should be combined with your location terms (e.g. your city, region, or metro area) where the site supports it.

### Priority 1: Policy Analyst / Research Associate

These match your strongest and most desired career direction.

```
site:usajobs.gov "Policy Analyst" Washington DC
site:indeed.com "Policy Analyst" OR "Research Associate" Washington DC
site:linkedin.com/jobs "Policy Analyst" Washington DC United States
site:linkedin.com/jobs "Research Associate" "policy analysis" United States
```

### Priority 2: Consulting / Government Affairs / Foreign Policy Domain

These match your domain expertise.

```
site:indeed.com "policy analysis" OR "strategic research" Washington DC OR Virginia
site:glassdoor.com "Government Affairs Associate" Washington DC
site:linkedin.com/jobs "Consulting Analyst" "stakeholder" Washington DC United States
site:linkedin.com/jobs "foreign policy" OR "national security" analyst Washington DC
```

### Priority 3: Program/Project Coordination & Legislative Roles

Adjacent roles you could pivot into.

```
site:indeed.com "Program Coordinator" "stakeholder engagement" Washington DC
site:linkedin.com/jobs "Legislative Correspondent" OR "Staff Assistant" Washington DC
site:ziprecruiter.com "Project Coordinator" nonprofit Washington DC
```

### Priority 4: Broader Research / Administrative Roles

Wider net for general roles matching transferable skills.

```
site:indeed.com "research analyst" Washington DC OR Richmond OR Norfolk
site:linkedin.com/jobs "research analyst" "policy analysis" United States
site:glassdoor.com "program coordinator" OR "project coordinator" Washington DC
```

## Location Filter

When evaluating results, verify the job location is within reasonable commute distance from home, or is open to relocation. Define acceptable areas:
- Washington, D.C. and the DMV (D.C., Maryland, Virginia suburbs) - ideal
- Richmond, VA - acceptable
- Newport News / Norfolk, VA - acceptable
- Other major U.S. metros - borderline (discuss with Daniel; open to relocating only if salary/benefits are strong enough to justify it)
- Roles requiring more than 40% travel - too far / excluded (deal-breaker)

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
