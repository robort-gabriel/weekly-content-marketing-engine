# Weekly Content Marketing Engine — Automation Prompt

## Objective

Keep `{{WEBSITE_URL}}`'s content pipeline full automatically: crawl its latest pages, find a topic with real SEO potential it hasn't covered, write a full blog post about it, and repurpose that post into a LinkedIn post, X thread, and carousel outline — by running the three project-local skills in sequence: `website-analyzer` -> `seo-content-writer` -> `social-repurposer`.

## Inputs

- `website_url` (required): `{{WEBSITE_URL}}` — the site to analyze and generate content for, e.g. `https://coding180.com`.
- `focus_topic` (optional): `{{FOCUS_TOPIC}}` — if given, skip topic selection in `website-analyzer` and write directly about this topic instead of the auto-ranked pick.

## Steps

1. Run the `website-analyzer` skill (`Skills/website-analyzer/SKILL.md`) for `website_url`. It crawls the site's recent/prominent pages and identifies content gaps with SEO potential using only `web_search`, `web_research`, `x_search`, `read_webpage`, and browser tools — never a paid crawling or SEO API. Output: `Content/Website-Content-Engine/<slug>/<date>/site-analysis.md`. If `focus_topic` was given, still crawl the site for voice/context, but set the Selected Topic to `focus_topic` instead of auto-ranking.
2. Run the `seo-content-writer` skill (`Skills/seo-content-writer/SKILL.md`) on that `site-analysis.md`. Output: `blog-post.md` in the same folder.
3. Run the `social-repurposer` skill (`Skills/social-repurposer/SKILL.md`) on that `blog-post.md`. Output: `linkedin-post.md`, `x-thread.md`, and `carousel-outline.md` in the same folder.
4. Do not fabricate keyword competition, search volume, or statistics at any stage — only report data actually retrieved from a real search. Every written draft must be personalized to the site's own voice and must not use em dashes.
5. Do not publish or post anything to the live website, LinkedIn, X, or anywhere else. This automation only ever writes draft files for later human review.

## Outputs

Saved under `Content/Website-Content-Engine/<site-slug>/<YYYY-MM-DD>/`:

- `site-analysis.md`
- `blog-post.md`
- `linkedin-post.md`
- `x-thread.md`
- `carousel-outline.md`

Plus a short chat/report summary: the selected topic, the blog post title and word count, and the output folder path. Keep the summary to 3-5 bullet points since it may be delivered via SMS/email/Slack when run unattended.

## Error handling

- If `website_url` is missing or unreachable, stop and report that rather than guessing or fabricating a site analysis.
- If no sitemap is found and the homepage can't be crawled, report the blocker rather than inventing crawled pages.
- If research turns up no clear content gap, report that honestly rather than inventing a topic — do not skip straight to a fabricated blog post.
- If any stage's required input file is missing (e.g. `seo-content-writer` can't find `site-analysis.md`), stop and report which stage failed rather than guessing its contents.
</content>
