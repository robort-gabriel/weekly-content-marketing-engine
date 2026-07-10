---
name: seo-content-writer
description: Write a publication-ready, SEO-optimized blog post for a chosen topic, matching the tone and structure of an existing website. This is stage 2 of the Weekly Content Marketing Engine pipeline. Use when a topic and website context have already been identified — e.g. via the website-analyzer skill's site-analysis.md — and a full blog post draft is needed. Hands its output to the social-repurposer skill.
metadata:
  author: robort.zo.computer
---

# SEO Content Writer

Turns a chosen, already-validated topic into a full SEO blog post draft, matched to the source website's voice. Free-only — research relies on `web_search`/`web_research`, never a paid content or SEO API.

## Inputs

- `site_analysis_file` (required unless both of the below are given): path to a `site-analysis.md` produced by `website-analyzer` (e.g. `Content/Website-Content-Engine/<site-slug>/<date>/site-analysis.md`).
- `topic` + `website_url` (alternative to `site_analysis_file`): use when the user hands you a topic directly without running `website-analyzer` first.

## Workflow

### Step 1 — Gather context

- Read `site_analysis_file` for the **Selected Topic**, the site's apparent niche/audience, and 1-2 of the crawled page titles/topics to get a feel for existing coverage.
- Skim 1-2 of the site's actual crawled pages (via `read_webpage`) if you need a clearer sense of its tone (formal vs. conversational, technical depth, typical post length).

### Step 2 — Research supporting facts

- Run 2-3 `web_search`/`web_research` queries on the topic to gather current, accurate supporting facts, examples, or data points.
- Track source URLs for anything you cite. Never fabricate statistics, quotes, or claims — if you can't verify a number, describe it qualitatively instead.

### Step 3 — Draft the blog post

Write a single post with:
- **Title** — SEO-friendly, includes the primary keyword naturally, matches the site's existing title style.
- **Meta description** — ~155 characters, includes the primary keyword.
- **Body** — 900-1500 words, H2/H3 structure, a real intro (hook + what the reader will get) and a real conclusion (recap + next step), natural (not stuffed) keyword usage.
- **Personalization** — write in the site's own established voice/perspective, not generic AI-blog tone. Reference the site's apparent audience and angle directly rather than writing something generic that could belong to any site.
- **Formatting** — do not use em dashes (—) anywhere in the draft; use commas or periods instead. This applies to every piece of text this skill produces, since it is written to be published.

### Step 4 — Save output

Write `blog-post.md` in the same folder as `site_analysis_file` (or, if working from a bare topic, in `Content/Website-Content-Engine/<site-slug>/<YYYY-MM-DD>/` using the site's own slug and today's date):

```markdown
# <Blog Post Title>

Meta description: <~155 char meta description>
Primary keyword: <keyword>
Generated: <YYYY-MM-DD>
Source topic: <site-analysis.md path, or "direct topic input">

<full post body, H2/H3 structured>
```

### Step 5 — Handoff

Report the output file path, word count, and primary keyword. Tell the user (or the orchestrating automation) to run the `social-repurposer` skill next, pointing it at this `blog-post.md` file.

## Notes

This skill produces a draft file only — it never publishes or posts anywhere. Publishing to the live website, LinkedIn, X, or any other channel always requires a separate, explicit approval step outside this pipeline.
</content>
