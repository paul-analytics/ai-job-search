# Search Queries for Job Scraper

Personalized for Paul Owoicho-Oche John: Dubai, UAE. Target market is the UAE. Role titles were checked against live Dubai LinkedIn postings on 2026-11-13; see `documents/career/ats-keyword-map.md`. The updated CV targets **F&B operations, partner and account management, and revenue or business analysis**.

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. This fork ships two country-agnostic CLIs:

- **`linkedin-search`**: the main source for every category below. Always pass `--location "Dubai, United Arab Emirates"`. LinkedIn is where most Dubai hotel groups, luxury maisons and retail groups post.
- **`freehire-search`**: tech and data roles only. Use it for Priority 3 with `--country AE`. It is no use for hospitality or retail roles.
- **Indeed (MCP connector, when the session has it)**: Indeed UAE through Indeed's own API. Use for Priorities 1–3 with `country_code AE`, `location Dubai`. No recency flag, so filter to 14 days client-side. Often shows pay. See `SKILL.md` Step 1d.

The upstream Danish portals (Jobindex, Jobnet, Jobbank, Jobdanmark) were removed from this fork.

The major UAE boards (Bayt, GulfTalent, Naukrigulf, Indeed UAE, Dubizzle) all block automated access, with Cloudflare, Imperva or a login wall; this was tested on 2026-11-13. They have **no CLI here and must not be scraped around**. The exception is Indeed, reachable through the Indeed MCP connector (Step 1d) when a session has it. For each `/scrape`, print the ready-made manual search links from `uae-job-sites.md` (this directory) in the Step 5 summary so the user can open them in a browser.

**Language scope:** the candidate works in **English only**. Write every query in English. In Dubai, about one posting in four asks for Arabic and about one in seven asks for Russian (16 and 10 of 67 sampled postings). When a posting *requires* Arabic, Russian, French or another undeclared language (e.g. "Arabic Speaker", "Russian Speaker" in the title, or "fluent Arabic required"), exclude it via the Language Gate in `04-job-evaluation.md`. "Arabic is a plus" is not a requirement; keep those.

## Search Sites

Primary:
- **linkedin.com/jobs**: filter Dubai, United Arab Emirates; covered by the `linkedin-search` CLI
- **bayt.com**: largest MENA board; manual search only (see `uae-job-sites.md`)
- **naukrigulf.com**: high volume for hospitality, retail and customer service; manual only
- **gulftalent.com**: mid and senior professional roles; manual only
- **ae.indeed.com**: aggregator; manual only (login wall for bots)
- **dubizzle.com/jobs**: entry-level, hospitality and retail volume; manual only

Secondary (employer career pages via WebSearch `site:` queries):
- Hospitality: `careers.marriott.com`, `jobs.hilton.com`, `careers.accor.com`, `jumeirah.com`, `kerzner.com` (Atlantis, One&Only), `emaar.com`, `rotana.com`, `careers.ihg.com`, `careers.dorchestercollection.com`
- Luxury and premium retail: `chalhoubgroup.com`, `altayer.com`, `careers.majidalfuttaim.com`, `apparelgroupglobal.com`, `rivoligroup.com`, `landmarkgroup.com`
- F&B groups: `kitopi.com`, `gateshospitality.com`, `eatx.com`, `alabbarenterprises.com`

## Query Categories

Combine every query with `Dubai` (CLI: `--location "Dubai, United Arab Emirates"`). Categories are named by function; the titles inside are interchangeable variants.

### Priority 1: F&B operations and guest experience (strongest, current track)

Direct continuation of Mythos (Waiter 2021 -> Team Lead 2023): leading a 15+ person floor team, VIP guests, upselling, complaints, kitchen/bar coordination.

```
linkedin-search: "F&B supervisor" | "restaurant supervisor" | "assistant outlet manager" | "assistant restaurant manager" | "captain" | "F&B operations"
linkedin-search: "guest relations" | "guest experience" | "VIP host" | "head hostess" | "maitre d"
site:careers.hyatt.com Dubai ("F&B supervisor" OR "assistant manager - outlet")
site:careers.marriott.com "Dubai" ("restaurant supervisor" OR "guest experience")
```

### Priority 2: Partner and account management (CV target)

Restaurant-partner and key-account roles, mostly on food-delivery and quick-commerce platforms. The F&B floor experience plus Excel/SQL is the pitch. Postings ask for "manage a portfolio of restaurant partners", "business reviews", "data insights", "negotiation", "Excel" and "CRM".

```
linkedin-search: "account manager" restaurants | "key account manager" restaurants | "account management" food | "partner success" | "partner account manager"
linkedin-search: "account executive" F&B | "key account executive" hospitality | "client success" food delivery
site:careem.com careers "account manager"
site:careers.deliveroo.co.uk Dubai "account manager"
site:careers.talabat.com "account manager"
```

### Priority 3: Revenue, business and data analysis (CV target)

SQL (T-SQL), Python (pandas, scikit-learn), Power BI (DAX), backed by the hotel revenue dashboard and the BA data science simulation.

```
linkedin-search: "revenue coordinator" | "revenue analyst" hotel | "reservations" | "revenue executive"
linkedin-search: "junior data analyst" | "data analyst" | "business analyst" | "sales analyst" | "reporting analyst" | "power bi"
linkedin-search: "CRM analyst" | "customer insights" | "business intelligence analyst" | "commercial analyst"
freehire-search: -q "data analyst" --country AE | -q "power bi" --country AE | -q "business analyst" --country AE
```

### Priority 4: Luxury retail, CX and wider net

```
linkedin-search: "client advisor" | "sales associate" luxury | "customer experience executive" | "customer relations officer"
linkedin-search: "sales coordinator" hotel | "events coordinator" | "operations coordinator" | "operations executive"
```

## UAE boards via WebSearch (SKILL.md Step 1e)

These are search-engine queries, not page fetches; the boards themselves stay off-limits for automation. Run the ones matching the categories in play:

```
site:bayt.com restaurant supervisor Dubai
site:bayt.com "F&B supervisor" OR "floor supervisor" OR "team leader" Dubai
site:bayt.com "account manager" restaurants OR "food delivery" Dubai
site:bayt.com "data analyst" OR "revenue analyst" OR "business analyst" Dubai
site:gulftalent.com Dubai restaurant supervisor OR "F&B supervisor" OR "team leader"
site:gulftalent.com Dubai "account manager" OR "key account" food
site:gulftalent.com Dubai "data analyst" OR "revenue" OR "business analyst" junior
site:naukrigulf.com restaurant supervisor Dubai
site:naukrigulf.com "F&B supervisor" OR "captain" Dubai
site:jobs.workable.com Dubai restaurant supervisor OR "floor supervisor"
```

## Location Filter

The candidate lives in Dubai. Commute constraints are not confirmed yet (`/setup --section search` can refine this):
- **Ideal:** Dubai (all areas)
- **Acceptable:** Sharjah, Ajman (long commute; flag it)
- **Borderline:** Abu Dhabi, Ras Al Khaimah (would mean relocating; flag it)
- **Exclude:** outside the UAE, unless the user asks for GCC-wide searches

**Emiratisation filter:** exclude postings restricted to UAE nationals, e.g. "UAE National" in the title, "Emirati only", "UAE nationals only" or "Nafis". The candidate is not eligible.

## Language Filter

Working language: English (fluent). Apply `04-job-evaluation.md`'s Language Gate:
- Exclude: postings whose title or requirements need Arabic, Russian, French, Mandarin, Hindi, etc. ("Arabic Speaker", "Russian Speaking", "fluent Arabic required")
- Keep: "Arabic is an advantage" / "additional language is a plus", and say in the evaluation that it counts as a soft gap

## Salary Filter

Minimum AED 5,000/month. When a posting (often Indeed) states pay whose top end is below AED 5,000, mark it Low and say why. A range straddling 5,000 gets a ⚠ in the Title cell. No stated pay: no effect.

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus:
- "/scrape hospitality" or "/scrape f&b" -> Priority 1 + hotel-group career-page queries
- "/scrape accounts" -> Priority 2 (delivery platforms + F&B key accounts)
- "/scrape data" -> Priority 3 (LinkedIn + freehire)
- "/scrape luxury" -> Priority 4 retail/CX queries
- "/scrape broad" -> all four priorities
