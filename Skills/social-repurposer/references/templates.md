# Output File Templates

All files below are written to the same folder as the input `blog-post.md` (i.e. `Content/Website-Content-Engine/<site-slug>/<YYYY-MM-DD>/`). Follow the formatting exactly (no extra spaces inside table/list rows) so downstream tooling can parse these reliably. No em dashes anywhere — these are published-facing drafts.

## linkedin-post.md

```markdown
# LinkedIn Post — <Blog Post Title>

Generated: <YYYY-MM-DD>
Source: <path to blog-post.md>

<hook line>

<body paragraphs, short, line-broken>

<CTA line with [BLOG_URL] placeholder>

#hashtag1 #hashtag2 #hashtag3
```

## x-thread.md

```markdown
# X Thread — <Blog Post Title>

Generated: <YYYY-MM-DD>
Source: <path to blog-post.md>

1/ <hook tweet, stands alone>

2/ <key point tweet>

3/ <key point tweet>

...

N/ <CTA tweet with [BLOG_URL] placeholder>
```

## carousel-outline.md

```markdown
# Carousel Outline — <Blog Post Title>

Generated: <YYYY-MM-DD>
Source: <path to blog-post.md>

## Slide 1 (Cover)
<title / hook line>

## Slide 2
**<heading>**
<1-2 lines of supporting content>

## Slide 3
**<heading>**
<1-2 lines of supporting content>

...

## Slide N (Closing CTA)
<call to action, e.g. "Read the full breakdown, link in bio">
```
</content>
