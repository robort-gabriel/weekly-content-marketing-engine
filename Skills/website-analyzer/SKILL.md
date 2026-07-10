---
name: website-analyzer
description: Crawl a website's most recent/prominent pages and identify content topics with SEO potential — gaps, thinly-covered angles, and trending questions relevant to the site's niche. This is stage 1 of the Weekly Content Marketing Engine pipeline. Use when the user provides a website URL and wants fresh, defensible topic ideas mined from the site's existing content plus external search signals. Hands its output to the seo-content-writer skill.
metadata:
  author: robort.zo.computer
---

# Website Analyzer

Crawls a website's existing content, then uses free search tools to find topics the site hasn't covered yet (or has covered thinly) that carry real search demand. Free-only — never requires a paid crawling/SEO API.

## Inputs

- `website_url` (required): the site to analyze, e.g. `https://coding180.com`.

## Workflow

### Step 1 — Crawl the site

- Try `read_webpage` on `<website_url>/sitemap.xml` and `<website_url>/sitemap_index.xml` first — sitemaps give the fastest, most complete page list.
- If no sitemap is found, use `read_webpage`/`open_webpage` + `view_webpage` on the homepage and its blog/articles listing page, following pagination or "recent posts" links.
- From whichever source works, collect the 10-20 most recent or most prominent pages: title, URL, and a one-line topic summary for each.

### Step 2 — Find topics with SEO potential

- Run 3-4 differently-worded `web_search` / `web_research` queries (use `topic="news"` when recency matters) around the site's established niche (inferred from the crawled titles/topics), looking for:
  - Recurring "People Also Ask"-style questions
  - Recent news/announcements creating new search demand in the niche
  - Forum/Reddit/Quora threads signaling real, current questions
- Optionally run `x_search` for live discourse if the niche is fast-moving (product launches, AI tooling, etc.).
- Compare each candidate against the crawled page list from Step 1: keep only topics the site has **not** covered, or has covered only in passing (a single old paragraph, not a dedicated piece).
- Score each candidate's SEO potential Low/Medium/High using visible SERP-quality signals only (long-tail phrasing, forums/UGC ranking on page 1, no dominant brand = lower competition; page 1 dominated by major publishers = higher competition). Never state an exact search-volume or difficulty number that wasn't actually retrieved from a real, connected data source — these scores are heuristic estimates, and must be labeled as such.

### Step 3 — Rank and select

- Rank candidates by (a) fit with the site's established audience/niche and (b) apparent low competition / clear content gap.
- Select the single top-ranked topic as "this cycle's pick" — this is what `seo-content-writer` will draft into a blog post next.

### Step 4 — Save output

Slugify the site's domain and write `Content/Website-Content-Engine/<site-slug>/<YYYY-MM-DD>/site-analysis.md`:

```markdown
# Website Analysis — <Website URL>

Generated: <YYYY-MM-DD>

## Crawled Pages

| Title | URL | Topic |
|---|---|---|
| <page title> | <url> | <one-line topic> |

## Candidate Topics (Content Gaps)

| Topic | SEO Potential | Reason |
|---|---|---|
| <topic> | Low/Medium/High | <one-line gap + demand rationale> |

## Selected Topic for This Cycle

**<topic>** — <one-line justification for why this beat the other candidates>
```

No extra spaces inside table separator rows — downstream skills parse these tables.

### Step 5 — Handoff

Report the output file path, how many crawled pages and candidate topics were found, and the selected topic. Tell the user (or the orchestrating automation) to run the `seo-content-writer` skill next, pointing it at this `site-analysis.md` file.
</content>
