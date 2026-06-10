# Prompt Engineering Log — AI Content Automation

> Tracks the evolution of the main generation prompt: what broke, what changed, and the final working version.

---

## Initial Prompt (v1)

```
Generate content for the topic provided by the user.

Create:
- Blog Title
- Blog Outline
- Blog Article
- Social Media Captions
- Hashtags
```

---

## Issues Identified

| # | Issue | Impact |
|---|---|---|
| 1 | Inconsistent output structure | Sections appeared in random order |
| 2 | Markdown symbols in output (`**`, `##`, `--`) | Broke Telegram rendering |
| 3 | Variable content quality | Outputs ranged from shallow to verbose |
| 4 | Unnecessary preamble and explanations | Bloated messages, harder to parse |
| 5 | No platform-specific social content | Generic captions across LinkedIn, Instagram, X |

---

## Improvements Made

### Structure
- Added labelled output sections with fixed order
- Defined exactly what each section must contain
- Specified word count for the blog article (800–1200 words)

### Output format
- Enforced plain text — no `#`, `##`, `**`, `--`, tables, or code blocks
- Stripped explanatory preamble from responses
- Improved readability for Telegram delivery

### Content quality
- Added SEO requirements for titles
- Introduced platform-specific social posts (LinkedIn, Instagram, X)
- Set business-quality writing standard
- Increased hashtag count to 20 for better discoverability

---

## Final Prompt (v2)

```
You are a professional content writer, SEO specialist, and social media manager.

Topic: {{$json.topic}}

Generate the following content:

1. Five SEO-friendly blog titles.
2. A detailed blog outline including:
   - Introduction
   - Main sections with subsections
   - Conclusion
3. A professional blog article between 800 and 1200 words.
4. Three LinkedIn posts.
5. Three Instagram captions.
6. Three Twitter/X posts.
7. Twenty relevant hashtags.

Output requirements:
- Use plain text only.
- Do not use Markdown formatting.
- Do not use #, ##, **, --, tables, or code blocks.
- Keep formatting clean and professional.
- Avoid unnecessary explanations or preamble.
- Use business-quality language.
- Ensure all content is relevant to the topic.

Output format — use these exact section labels in this order:

BLOG TITLES
BLOG OUTLINE
BLOG ARTICLE
LINKEDIN POSTS
INSTAGRAM CAPTIONS
TWITTER/X POSTS
HASHTAGS
```

---

## Output Specification

| Section | Format | Quantity |
|---|---|---|
| Blog titles | Plain text, one per line | 5 |
| Blog outline | Intro → sections → subsections → conclusion | 1 |
| Blog article | 800–1200 words, business tone | 1 |
| LinkedIn posts | Professional, paragraph style | 3 |
| Instagram captions | Engaging, conversational | 3 |
| Twitter/X posts | Under 280 chars each | 3 |
| Hashtags | Plain text, space-separated | 20 |

---

## Benefits

- Consistent section order every run
- Zero Markdown bleed into Telegram
- Platform-appropriate social content (LinkedIn ≠ Instagram ≠ X)
- Faster review — no preamble to strip
- SEO-ready titles out of the box
- Business-quality tone enforced at prompt level
