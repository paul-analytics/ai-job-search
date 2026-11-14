# UAE Job Sites: Coverage and Manual Search Links

Checked 2026-11-13 from this repo's cloud environment. This lists every UAE hiring channel that matters for the candidate's target roles. It says which ones `/scrape` covers automatically and which must be searched by hand in a browser.

## Automated (CLI in `.agents/skills/`)

| Site | Skill | Covers | Status |
|---|---|---|---|
| LinkedIn Jobs | `linkedin-search` | All target roles, Dubai | ✅ Works. Live test returned Dubai postings. Personal use only, low volume |
| Indeed UAE | Indeed MCP connector (`mcp__Indeed__*`) | All target roles, `country_code AE`, `location Dubai` | ✅ Works through Indeed's API (tested 2026-11-14; returns pay on many ads). No recency filter: filter to 14 days client-side. Only in sessions where the connector is attached |
| freehire.me | `freehire-search` | Tech/data roles only (`--country AE`) | ✅ Works. Live test returned Dubai/Sharjah data analyst roles |

## Manual only (bot-protected: do NOT build scrapers that get around this)

| Site | Best for | Why manual | Notes |
|---|---|---|---|
| **Bayt.com** | Largest MENA board; office, hospitality and retail roles at established employers | Cloudflare challenge (HTTP 403) | Make a profile and turn on job alerts. Many recruiters search Bayt CVs directly |
| **GulfTalent** | Professional and mid-level roles (analyst, CRM, CX, revenue) | Imperva/Incapsula (HTTP 403) | Upload the CV. GulfTalent recruiters search its CV database |
| **Naukrigulf** | High volume for hospitality, retail, customer service | Imperva/Incapsula, connection refused | Popular with South and Southeast Asian and African applicants; lots of hotel postings |
| **Indeed UAE** (ae.indeed.com) | Aggregator; includes many employer career pages | Login wall for scrapers (HTTP 401); **use the Indeed connector instead** when attached | Use the 14-day filter (`fromage=14`) |
| **Dubizzle Jobs** | Entry-level, F&B, retail, customer service | Imperva/Incapsula | Many listings are low-paid or part-time; check salary before applying |
| **Dubai Careers** (dubaicareers.ae) | Dubai Government entities | Not tested | Most roles favour UAE nationals; check eligibility |
| **Nafis** | Emirati-only private-sector roles | n/a | **Not eligible.** Skip |

### Employer career sites (highest response rate for hospitality and luxury)

Apply directly. These groups post there first and often never use the boards:
- **Hotels:** Marriott (careers.marriott.com), Hilton (jobs.hilton.com), Accor (careers.accor.com), Jumeirah, Kerzner (Atlantis The Royal, One&Only), Emaar Hospitality (Address, Vida), Rotana, IHG, Dorchester Collection (The Lana), Four Seasons, Mandarin Oriental
- **Luxury and premium retail:** Chalhoub Group, Al Tayer Group, Majid Al Futtaim, Rivoli Group, Apparel Group, Landmark Group, Damas, Ahmed Seddiqi & Sons
- **Delivery / quick-commerce platforms (account management):** Careem, Deliveroo, noon Food, Talabat
- **F&B groups:** Kitopi, Gates Hospitality, EATX, Alabbar Enterprises, Bulldozer Group, Atelier House Hospitality
- **Recruiters:** Hays, Michael Page, Robert Half (data roles); Hospitality-focused agencies (e.g. Caterer Global listings)

## Ready-made manual searches (Dubai, last ~14 days where the site supports it)

URL patterns were checked against live indexed pages on 2026-11-13: GulfTalent `/uae/jobs/dubai/title/<slug>`, Naukrigulf `/<slug>-jobs-in-dubai`, Indeed `?q=&l=Dubai`. The Bayt pattern could not be confirmed past the Cloudflare page. If a Bayt link 404s, use the site's search box.

| Role | LinkedIn | GulfTalent | Naukrigulf | Bayt | Indeed UAE |
|---|---|---|---|---|---|
| Account Manager | [open](https://www.linkedin.com/jobs/search/?keywords=Account+Manager&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/account-manager) | [open](https://www.naukrigulf.com/account-manager-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/account-manager-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Account+Manager&l=Dubai&fromage=14) |
| F&B Supervisor | [open](https://www.linkedin.com/jobs/search/?keywords=F%26B+Supervisor&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/fandb-supervisor) | [open](https://www.naukrigulf.com/fandb-supervisor-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/fandb-supervisor-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=F%26B+Supervisor&l=Dubai&fromage=14) |
| Business Analyst | [open](https://www.linkedin.com/jobs/search/?keywords=Business+Analyst&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/business-analyst) | [open](https://www.naukrigulf.com/business-analyst-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/business-analyst-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Business+Analyst&l=Dubai&fromage=14) |
| Restaurant Supervisor | [open](https://www.linkedin.com/jobs/search/?keywords=Restaurant+Supervisor&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/restaurant-supervisor) | [open](https://www.naukrigulf.com/restaurant-supervisor-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/restaurant-supervisor-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Restaurant+Supervisor&l=Dubai&fromage=14) |
| Guest Relations Executive | [open](https://www.linkedin.com/jobs/search/?keywords=Guest+Relations+Executive&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/guest-relations-executive) | [open](https://www.naukrigulf.com/guest-relations-executive-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/guest-relations-executive-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Guest+Relations+Executive&l=Dubai&fromage=14) |
| Guest Experience | [open](https://www.linkedin.com/jobs/search/?keywords=Guest+Experience&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/guest-experience) | [open](https://www.naukrigulf.com/guest-experience-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/guest-experience-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Guest+Experience&l=Dubai&fromage=14) |
| Client Advisor | [open](https://www.linkedin.com/jobs/search/?keywords=Client+Advisor&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/client-advisor) | [open](https://www.naukrigulf.com/client-advisor-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/client-advisor-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Client+Advisor&l=Dubai&fromage=14) |
| Sales Associate | [open](https://www.linkedin.com/jobs/search/?keywords=Sales+Associate&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/sales-associate) | [open](https://www.naukrigulf.com/sales-associate-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/sales-associate-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Sales+Associate&l=Dubai&fromage=14) |
| Customer Experience Executive | [open](https://www.linkedin.com/jobs/search/?keywords=Customer+Experience+Executive&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/customer-experience-executive) | [open](https://www.naukrigulf.com/customer-experience-executive-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/customer-experience-executive-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Customer+Experience+Executive&l=Dubai&fromage=14) |
| Reservations Agent | [open](https://www.linkedin.com/jobs/search/?keywords=Reservations+Agent&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/reservations-agent) | [open](https://www.naukrigulf.com/reservations-agent-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/reservations-agent-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Reservations+Agent&l=Dubai&fromage=14) |
| Revenue Coordinator | [open](https://www.linkedin.com/jobs/search/?keywords=Revenue+Coordinator&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/revenue-coordinator) | [open](https://www.naukrigulf.com/revenue-coordinator-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/revenue-coordinator-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Revenue+Coordinator&l=Dubai&fromage=14) |
| Junior Data Analyst | [open](https://www.linkedin.com/jobs/search/?keywords=Junior+Data+Analyst&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/junior-data-analyst) | [open](https://www.naukrigulf.com/junior-data-analyst-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/junior-data-analyst-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Junior+Data+Analyst&l=Dubai&fromage=14) |
| Sales Coordinator | [open](https://www.linkedin.com/jobs/search/?keywords=Sales+Coordinator&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/sales-coordinator) | [open](https://www.naukrigulf.com/sales-coordinator-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/sales-coordinator-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Sales+Coordinator&l=Dubai&fromage=14) |
| CRM Executive | [open](https://www.linkedin.com/jobs/search/?keywords=CRM+Executive&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/crm-executive) | [open](https://www.naukrigulf.com/crm-executive-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/crm-executive-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=CRM+Executive&l=Dubai&fromage=14) |
| Operations Coordinator | [open](https://www.linkedin.com/jobs/search/?keywords=Operations+Coordinator&location=Dubai%2C%20United%20Arab%20Emirates&f_TPR=r1209600) | [open](https://www.gulftalent.com/uae/jobs/dubai/title/operations-coordinator) | [open](https://www.naukrigulf.com/operations-coordinator-jobs-in-dubai) | [open](https://www.bayt.com/en/uae/jobs/operations-coordinator-jobs-in-dubai/) | [open](https://ae.indeed.com/jobs?q=Operations+Coordinator&l=Dubai&fromage=14) |

## How `/scrape` uses this file

At the end of every `/scrape` run, list the manual-search links above that match the categories that were run. The CLIs can't reach these boards, so they are where the user's own browser search fills the gap. When the user pastes a posting URL from any of these sites into `/apply`, it counts as a known board (see `apply.md` Source Host Verification).
