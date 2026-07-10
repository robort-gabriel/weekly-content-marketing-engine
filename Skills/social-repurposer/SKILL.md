---
name: social-repurposer
description: Repurpose a finished blog post into a LinkedIn post, an X/Twitter thread, and a carousel slide outline. This is stage 3 (final) of the Weekly Content Marketing Engine pipeline. Use when a blog-post.md (e.g. produced by the seo-content-writer skill) exists and needs to be adapted into short-form social formats. Produces drafts only — never publishes or posts on its own.
metadata:
  author: robort.zo.computer
---

# Social Repurposer

Turns one finished blog post into three short-form social drafts: a LinkedIn post, an X thread, and a carousel slide outline.

## Inputs

- `blog_post_file` (required): path to a `blog-post.md` produced by `seo-content-writer` (e.g. `Content/Website-Content-Engine/<site-slug>/<date>/blog-post.md`).

## Workflow

### Step 1 — Extract the core

Read `blog_post_file`. Pull out:
- One strong hook line (can reuse or sharpen the post's own opening line).
- 3-5 key points/takeaways from the body.
- The primary keyword/topic, for hashtag and thread framing.

### Step 2 — Write the LinkedIn post

150-250 words. Hook as the first line. Short paragraphs with line breaks (not one dense block). Personal/professional tone matching the blog post's voice. End with a CTA line pointing to the full post (use a `[BLOG_URL]` placeholder if the live URL isn't known yet), then 3-5 relevant hashtags on their own line at the end. No em dashes — commas or periods only, since this is written to be published.

### Step 3 — Write the X thread

5-8 tweets. First tweet is the hook and must stand alone (no thread-numbering needed at all, or use lightweight `1/`, `2/` markers — pick one style and stay consistent). Each tweet under 280 characters. Middle tweets each carry one key point. Last tweet is the CTA with a `[BLOG_URL]` placeholder. No em dashes.

### Step 4 — Write the carousel outline

A slide-by-slide outline (not a finished visual carousel): cover slide with the hook, 4-8 content slides (one heading + 1-2 lines each, one key point per slide), and a closing CTA slide. No em dashes.

If the user wants this outline turned into an actual visual carousel (HTML/image slides), that requires the separate, globally-installed `carousel-generator` skill — outside this project's scope — so hand it off by name rather than attempting to build visuals here.

### Step 5 — Save outputs

Write these files in the same folder as `blog_post_file` — see `references/templates.md` for exact formats:
- `linkedin-post.md`
- `x-thread.md`
- `carousel-outline.md`

### Step 6 — Report back

Summarize in chat: which 3 files were written and their folder path. Remind the user that these are drafts — nothing gets posted to LinkedIn, X, or anywhere else until they explicitly review and approve each piece for publishing.

## Notes

This skill never calls a social platform API and never publishes on its own. It only ever writes local draft files.
</content>
