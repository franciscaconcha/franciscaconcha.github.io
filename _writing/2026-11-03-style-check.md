---
title: "Style check: everything a post can contain"
date: 2026-11-03
summary: "A placeholder that exercises every element a writing post can use. Never published."
tags: [meta, style-check]
paper: https://example.com/paper
code: https://example.com/code
status: "Placeholder text for previewing the layout. Nothing here is a real result."
math: true
published: false
---

This first paragraph is the lede: it's shown a little larger than the rest. Use it to say what you
wanted to find out and why it matters, in two or three sentences.

Regular paragraphs follow. They can have **bold**, *italics*, [links](https://example.com), inline
`code`, and footnotes.[^thanks]

## Setup

A fenced code block with a language name gets syntax highlighting:

```python
def judge(model, example):
    prompt = JUDGE_TEMPLATE.format(source=example.source, extraction=example.output)
    reply = model.complete(prompt, temperature=0)
    return parse_verdict(reply)  # "pass" | "fail"

results = [judge(m, ex) for m in JUDGES for ex in golden]
```

Inline math uses single dollars: observed agreement $p_o$, chance agreement $p_e$, and a fraction
$\frac{1}{n}\sum_i x_i$. Display math uses double dollars on their own lines:

$$
\kappa = \frac{p_o - p_e}{1 - p_e}
$$

Inside single dollars, write products as $a \cdot b$ or $a \ast b$ rather than with `*`, and sets as
$\lbrace 1, 2 \rbrace$ rather than with `\{`, because Markdown would otherwise eat those characters.

## Results

| Judge   | Overall κ | Ambiguous κ |   n |
|---------|----------:|------------:|----:|
| Judge A |      0.81 |        0.42 | 300 |
| Judge B |      0.77 |        0.35 | 300 |
| Judge C |      0.69 |        0.21 | 300 |

An image with a title in quotes gets a caption:

![A stellar encounter truncating a protoplanetary disc](/images/disk_encounter.gif "Figure 1. An existing image from the site, standing in for a chart.")

> A blockquote, for quoting a paper or another author.

### A smaller heading

- Lists work as usual.
- Second item.

[^thanks]: Footnotes collect at the end of the post.
