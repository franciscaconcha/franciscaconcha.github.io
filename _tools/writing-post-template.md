---
# Copy this file to _writing/YYYY-MM-DD-short-slug.md and fill it in.
#
# The file name sets the URL: _writing/2026-11-10-llm-judges.md is published at
# https://francisca.cr/writing/llm-judges/ (the date is dropped from the URL).
# Make the slug a short, lowercase version of the title, and don't change it once
# the post is live, because that changes its URL.
#
# Every field below is plain data. The layout decides how to show it, so keep the
# post itself plain Markdown: no {{ }} or {% %} tags, includes or shortcodes.

# Required. The title, shown on the post and in the list at /writing/.
title: "Do LLM judges agree with a golden dataset?"

# Required. Sets the order on /writing/ (newest first) and the date shown on the post.
date: 2026-11-10

# One or two sentences. Shown under the title on /writing/, in the feed, and as the
# description search engines and link previews use.
summary: >-
  How often LLM-as-judge grades match expert labels, and whether the
  disagreements are random.

# Optional. Short, lowercase, hyphenated.
tags: [evals, llm-as-judge, replication]

# Optional. Links to the paper and the code, shown as "paper" and "code" buttons.
paper: https://arxiv.org/abs/0000.00000
code: https://github.com/franciscaconcha/repo

# Optional "epistemic status": how confident you are and what you haven't checked.
# Shown in a callout above the post.
status: >-
  A weekend replication on one small dataset. I haven't tested other
  domains yet.

# true loads KaTeX on this post, for $…$ and $$…$$ math.
math: false

# Only for a post first published somewhere else: its original URL and the site's name.
# Shows "Originally published on <site>" and tells search engines the original is canonical.
# original_url: https://example.com/original-post
# original_site: Example blog

# Keep false while drafting: the post isn't built on the live site at all.
# Delete this line (or set it to true) to publish.
published: false
---

The first paragraph is the lede and is shown a little larger. Say what you wanted to
find out and why it matters.

## Section headings use two hashes

They're shown as small uppercase labels. Use ### for a smaller heading inside a section.

Code: put the language after the opening fence for syntax highlighting.

```python
print("hello")
```

Math (needs `math: true` above): inline as $p_o$, and display on its own lines:

$$
\kappa = \frac{p_o - p_e}{1 - p_e}
$$

Inside single dollars, Markdown can eat a few characters. Write products as
`\cdot` or `\ast` instead of `*`, and braces as `\lbrace … \rbrace` instead of `\{ … \}`.
Double dollars (`$$…$$`) are always safe, even in the middle of a sentence.

Tables: a colon on the right of the separator right-aligns a column (good for numbers).

| Judge   | κ    |
|---------|-----:|
| Judge A | 0.81 |

Images: put them in images/writing/<slug>/ (the same slug as the file name) and link
them with a path starting at the site root. Text in quotes becomes the caption.

![Bar chart of agreement by judge](/images/writing/llm-judges/agreement.png "Figure 1. Cohen's κ by judge.")

Footnotes work like this.[^1]

[^1]: And appear at the end of the post.
