# APEC.fr Scraper - French Executive Jobs

Extract structured data from [apec.fr](https://apec.fr) — apec.fr - French executive job listings with salary ranges, company, location, skills, contract type, recruiter contact, and apply URLs. Incremental tracking for new and changed roles across runs.

**[APEC.fr Scraper - French Executive Jobs on Apify →](https://apify.com/blackfalcondata/apec-scraper?fpr=1h3gvi)**

---

## Key features

**Search with filters** — Search by keyword and location. Filter by country, and more.

**Multiple input modes** — search by keyword / contract type or scrape specific offer urls. Switch modes without re-scraping.

**Direct URL mode** — Paste a list of listing URLs and fetch each one directly. Skips search — ideal for monitoring known IDs.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from apec.fr on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from apec.fr.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on apec.fr to inform pricing decisions, hiring plans, or candidate negotiations.

**Lead generation**
Extract employer contact details alongside listings to build outreach lists for recruiters, staffing agencies, or B2B sales teams.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "developpeur",
  "maxResults": 25,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `mode` | enum | `"search"` | How to discover jobs. 'search' runs a keyword + contractType query. 'jobUrls' scrapes specific offer URLs directly (bypasses search). |
| `query` | string | — | Job search keywords. Leave empty to browse by contract type only. |
| `contractTypes` | array | `[]` | Filter by contract type. At least one of query, contractTypes, or jobUrls must be set. |
| `country` | enum | `"FR"` | Which market to search. |
| `location` | string | — | City, state, or region. |
| `jobUrls` | array | `[]` | Specific apec.fr offer URLs. Format: https://www.apec.fr/candidat/recherche-emploi/detail-offre.html/offre/<ID>. Set mode=jobUrls to use. |
| `maxResults` | integer | `25` | Maximum total results (0 = unlimited). |
| `includeDetails` | boolean | `true` | Fetch full job details. |
| `descriptionMaxLength` | integer | `0` | Truncate description to N chars. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `incrementalMode` | boolean | `false` | Compare against previous run state. |
| `stateKey` | string | — | Stable identifier for tracked universe. |
| `emitUnchanged` | boolean | `false` | Also emit jobs that have not changed since the last run (incrementalMode only). |
| `emitExpired` | boolean | `false` | Also emit jobs that have disappeared since the last run (incrementalMode only). |
| `skipReposts` | boolean | `false` | When incremental, skip jobs whose content matches an expired job from a prior run (cross-run repost detection). |

---

## Output fields

Every listing returns the same 75-field schema. Missing values are `null` — never omitted.

- `jobId`
- `jobKey`
- `numeroOffre`
- `title`
- `url`
- `applyUrl`
- `portalUrl`
- `description`
- `descriptionText`
- `descriptionHtml`
- `descriptionMarkdown`
- `summary`
- `candidateProfileHtml`
- `recruitmentProcess`
- `salaryText`
- `salaryRange`
- `salaryMin`
- `salaryMax`
- `salaryCurrency`
- `salaryType`
- `employmentType`
- `contractTypeId`
- `contractDurationText`
- `isPartTime`
- `partTimeDurationLabel`
- `location`
- `city`
- `postalCode`
- `streetAddress`
- `department`
- `region`
- `country`
- `latitude`
- `longitude`
- `company`
- `companyBrand`
- `companyCommercialName`
- `companyId`
- `companyLogo`
- `companyIndustry`
- `companyIndustryParent`
- `companyDescription`
- `companyVideoUrl`
- `isConfidential`
- `jobFunction`
- `jobRole`
- `experienceLevel`
- `educationLevel`
- `positionType`
- `travelZone`
- `remoteWorkLevel`
- `skills`
- `applyMethod`
- `requiresCoverLetter`
- `lowApplicationVolume`
- `numberOfPositions`
- `clientReference`
- `contactFirstName`
- `contactLastName`
- `contactEmail`
- `contactPhone`
- `postedAt`
- `firstPublishedAt`
- `lastModifiedAt`
- `startDate`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `scrapedAt`
- `source`
- `contentHash`
- `isRepost`
- `repostOfId`
- `repostDetectedAt`
- `changeType`

---

## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "478c33b75f9c9a4cc4f4ea2e68446bf161465a0b67dd8248277c3442a7fd9bdf",
  "jobKey": "178546113W",
  "numeroOffre": "178546113W",
  "title": "DEVELOPPEUR .NET F/H",
  "url": "https://www.apec.fr/candidat/recherche-emploi/detail-offre.html/offre/178546113W",
  "applyUrl": null,
  "portalUrl": "https://www.apec.fr/candidat/recherche-emploi/detail-offre.html/offre/178546113W",
  "description": "Pour le compte de notre client, une ESN Française à taille humaine (100 collaborateurs), située sur la Métropole Lilloise, proposant une expertise technologique pointue et des miss…",
  "descriptionText": "Pour le compte de notre client, une ESN Française à taille humaine (100 collaborateurs), située sur la Métropole Lilloise, proposant une expertise technologique pointue et des miss…",
  "descriptionHtml": null,
  "descriptionMarkdown": null,
  "summary": "Pour le compte de notre client, une ESN Française à taille humaine (100 collaborateurs), située sur la Métropole Lilloise, proposant une expertise technologique pointue et des miss…"
}
```

*Truncated — full records contain 75 fields. See Output fields for the complete schema.*

**[Try APEC.fr Scraper - French Executive Jobs now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/apec-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.005 |
| Result | $0.001 |

See the [actor on Apify](https://apify.com/blackfalcondata/apec-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape apec.fr?**
Use this actor on Apify to extract structured data from apec.fr. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get apec.fr data as JSON, CSV, or Excel?**
The actor writes each listing to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape apec.fr?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check apec.fr's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for listings extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage. Expired listings can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [APEC.fr Scraper - French Executive Jobs](https://apify.com/blackfalcondata/apec-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 04*
