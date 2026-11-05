# A/B Test Plan: Home Page Headline

**Site:** First Season Iowa, https://grweston.github.io/first-season-iowa/
**Author:** Gage Weston, MKTG:4400 Deliverable 3
**This plan was committed before any trials were run.** The commit timestamp on this file is the proof.

## 1. Page and element

**Page:** Home page (`index.html`).
**Element:** The main headline (H1) only. Everything else on the page is identical in both versions.

| Version | Headline | Where it lives |
|---|---|---|
| A (control) | Iowa Deer Hunting for Beginners: How to Start | `index.html` |
| B (variant) | Never Hunted Before? Plan Your First Iowa Deer Hunt in Five Steps | `index-b.html` |

Version B has a `noindex` tag and a canonical tag pointing to version A, and it is not listed in `sitemap.xml`, so it cannot compete with version A in search.

### Why the headline

The site's goal is for a beginner to use the guide to plan a first deer hunt, and the headline is the first thing a visitor reads and the main signal of whether the page is for them. The current headline was written in Deliverable 2 to match search keywords ("Iowa deer hunting", "for beginners"), not to persuade the reader. That makes it the element most likely to be underperforming, and the one where a change could plausibly affect the decision to use the guide. Testing it leaves the rest of the page, including its content and SEO work, untouched, so any difference can only come from the headline.

## 2. Hypothesis

A larger share of AI visitors will say **yes, they would use this guide** when shown version B than when shown version A.

**Reasoning:** Version A's headline is built around search keywords. Version B speaks directly to the reader's situation (someone who has never hunted) and promises a concrete result (a planned first hunt), so a visitor who matches the target audience should see B as more clearly meant for them.

**This could turn out wrong:** the page content is identical in both versions, so the AI visitor may judge mostly on the content and ignore the headline. It may also say yes to both versions almost every time, leaving no room for a difference.

## 3. Visitors, prompt, and assignment

**Model:** Claude Sonnet 4.6 (`claude-sonnet-4-6`), called through the Claude API with default settings and a 1,000-token output limit. The same model and settings are used for every trial, and the model name is recorded on every row.

**One trial = one fresh conversation:** each trial is a single, separate API request with no earlier messages and no memory, so each answer depends only on the prompt and the page it was shown.

**Page shown:** the full visible text of the assigned version (notice, header, headline, body, and footer), pasted into the prompt the same way for both versions.

**Exact prompt** (identical in every trial except for the page text at the end):

> You are a 27-year-old who lives in Iowa City, Iowa. You have never been hunting, but a coworker invited you on a deer hunt this December, and you want to learn how to get started. Read this web page and decide whether you would use this guide to plan your first deer hunt. Answer yes or no, then give one sentence of reasoning.
>
> [full text of version A or version B]

**Assignment:** decided by chance before any trial runs. A list of 50 A's and 50 B's was shuffled with a random number generator (Python `random.shuffle`, seed 20261109). The full list is committed with this plan as `ab-test-assignments.csv`, and trials are run in that row order. Shuffling, rather than running all A's then all B's, means anything that changes during data collection affects both versions alike.

## 4. Primary outcome and scoring rule

**Outcome:** whether the visitor would use the guide. **Yes = 1, everything else = 0.**

**Scoring rule, fixed before any answers are seen:** only an answer that starts with "yes" scores 1. "No," "maybe," or any other answer scores 0. Every raw answer stays in the data file, and no trial is ever rerun or dropped.

## 5. Sample size and timing

**100 trials: 50 for version A and 50 for version B**, all collected before any analysis, with no stopping early.

With 50 per version, only a fairly large gap, roughly 28 percentage points or more (80% power, 5% significance, session 17 formula), is likely to show up as significant. A smaller real effect may come out not significant.

**Dates:** version B published by **Nov 12, 2026**; trials run **Nov 16 to 17, 2026**; all 100 complete by **Nov 17**.

## 6. Comparison and decision rule

**Comparison:** yes share in B minus yes share in A, tested with a **two-proportion z test**, two-sided, using each version's own share for the standard error (session 18 method). The report will show each version's count of visitors and yeses, the yes shares, the difference in points, the z statistic, the two-sided p value, and the 95% confidence interval.

**Support for the hypothesis:** B's yes share is higher than A's **and** p < .05.
**No support:** any other result. A flat result will be reported as flat.

## 7. Records kept

`ab-test-results.csv`, one row per trial: trial number, version, date, model, answer (yes/no/other), outcome (1/0), and the full output. Anything that goes wrong is logged with the date in `ab-test-log.md`.
