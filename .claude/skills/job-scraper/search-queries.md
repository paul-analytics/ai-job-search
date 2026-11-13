# Search Queries for Job Scraper

Personalized for Paul Owoicho-Oche John: Dubai, UAE. Target market is the UAE. Role titles were checked against live Dubai LinkedIn postings on 2026-11-13; see `documents/career/ats-keyword-map.md`.

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. This fork ships two country-agnostic CLIs:

- **`linkedin-search`**: the main source for every category below. Always pass `--location "Dubai, United Arab Emirates"`. LinkedIn is where most Dubai hotel groups, luxury maisons and retail groups post.
- **`freehire-search`**: tech and data roles only. Use it for Priority 3 with `--country AE`. It is no use for hospitality or retail roles.

The upstream Danish portals (Jobindex, Jobnet, Jobbank, Jobdanmark) were removed from this fork.

The major UAE boards (Bayt, GulfTalent, Naukrigulf, Indeed UAE, Dubizzle) all block automated access, with Cloudflare, Imperva or a login wall; this was tested on 2026-11-13. They have **no CLI here and must not be scraped around**. For each `/scrape`, print the ready-made manual search links from `uae-job-sites.md` (this directory) in the Step 5 summary so the user can open them in a browser.

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

### Priority 1: Guest experience and F&B leadership (strongest, current track)

Direct continuation of the Senior Waiter role at Mythos (City Walk): VIP guests, upselling, leading a 15+ person floor team, POS.

```
linkedin-search: "restaurant supervisor" | "F&B supervisor" | "captain" | "head waiter" | "assistant restaurant manager"
linkedin-search: "guest relations" | "guest experience" | "guest relations executive" | "VIP host" | "head hostess" | "maitre d"
site:careers.marriott.com "Dubai" ("restaurant supervisor" OR "guest experience")
site:jumeirah.com careers Dubai "guest relations"
```

### Priority 2: Luxury retail sales and clienteling

Consultative selling, clienteling, VIP relationship management and visual merchandising. TIVA Bespoke plus the luxury F&B record.

```
linkedin-search: "client advisor" | "sales associate" luxury | "sales advisor" boutique | "client relations" luxury | "clienteling"
linkedin-search: "customer experience executive" | "customer experience specialist" | "customer relations officer" | "customer excellence"
site:chalhoubgroup.com careers "sales" Dubai
site:altayer.com careers "client advisor"
```

### Priority 3: Data-driven bridge roles (MBA + Google Data Analytics + SQL/Power BI)

Hospitality, retail or customer roles where the data side is a real part of the job. These are the bridge from guest-facing work into analytics.

```
linkedin-search: "revenue coordinator" | "revenue analyst" hotel | "reservations" | "reservations agent" | "revenue executive"
linkedin-search: "junior data analyst" | "data analyst" | "sales analyst" | "reporting analyst" | "power bi"
linkedin-search: "CRM executive" | "CRM analyst" | "customer insights" | "business intelligence analyst"
freehire-search: -q "data analyst" --country AE | -q "power bi" --country AE | -q "sql analyst" --country AE
```

### Priority 4: Broader customer-facing and operations roles (wider net)

```
linkedin-search: "sales coordinator" hotel | "F&B sales coordinator" | "events coordinator" | "banquet coordinator"
linkedin-search: "operations coordinator" | "operations executive" | "customer service executive" | "customer service representative"
linkedin-search: "front office agent" | "guest service agent" | "front desk"
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

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus:
- "/scrape hospitality" -> Priority 1 + hotel-group career-page queries
- "/scrape luxury" -> Priority 2 + maison/retail-group career-page queries
- "/scrape data" -> Priority 3 (LinkedIn + freehire)
- "/scrape broad" -> all four priorities
