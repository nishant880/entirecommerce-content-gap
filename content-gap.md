# Content Gap + AEO Opportunity: Master Prompt

> Paste this entire file into Claude Code from a folder containing a `.env` (your API keys). If a `CLAUDE.md` business brief is already populated, Claude loads it and proceeds. Otherwise Claude interviews you conversationally for the business specifics and writes the `CLAUDE.md` for you. Either way, Claude runs the analysis end-to-end, produces a single consolidated report in markdown and Word formats, and saves supporting data alongside.
>
> Built by Nishant Kapoor at EntireCommerce AI. Version 1, April 2026.

---

You are executing the Content Gap + AEO Opportunity playbook for the brand in the current working directory. Follow these steps in order. Do not skip steps. Do not invent data. Honour the voice conventions in Step 6.

---

## Step 1. Load or populate the business brief

Look for `CLAUDE.md` in the current working directory.

**If `CLAUDE.md` exists and is fully filled in** (no `{placeholder}` text remaining, required fields populated), read it and proceed to Step 2.

**If `CLAUDE.md` does not exist, contains placeholder text, or is missing required fields, run the business-brief interview before proceeding.** Do not skip. Do not guess.

### The business-brief interview

Ask the user these questions conversationally, one batch at a time. Write the answers into `CLAUDE.md` progressively (create the file if missing) and confirm before moving on.

**Batch 1: Brand overview.** Brand name. Primary URL. Domain age. Ecommerce platform. Geographic focus. Stage.

**Batch 2: Product and audience.** What you sell in one sentence. Price range or AOV. Catalog size. Core buyer in one sentence. Where they hang out online.

**Batch 3: Current content footprint.** Blog or long-form presence. Monthly organic traffic band. Active topic clusters (if any). Publishing cadence. Team producing content.

**Batch 4: Positioning.** Why you win. Three to five competitor URLs. Pricing tier vs category median.

**Batch 5: AEO priorities.** Which LLM the ICP uses most. Current AEO presence suspicion. Three to five category questions you hear from customers.

**Batch 6: Tool stack and constraints.** Website / CMS. GSC property. SEO tools. Publishing velocity ceiling. Subject-matter expertise access. 12-month organic traffic goal. Primary outcome the content must drive.

### Minimum required to proceed to Step 2

If after the interview you do not have these seven fields, ask again:

1. Brand name
2. Primary URL
3. What the brand sells (one sentence)
4. Core buyer (one sentence)
5. Three to five competitor URLs
6. Monthly organic traffic band
7. Which LLM the ICP uses most

Optional fields can be marked "unknown" or "to be confirmed". Do not invent.

---

## Step 2. Inventory tool access

Read `.env` in the current working directory. Print the credential inventory:

```
External tools (public data)
- DataForSEO: configured / not configured
- Serper: configured / not configured
- Keywords Everywhere: configured / not configured
- Ahrefs: configured / not configured
- Google PageSpeed Insights (GOOGLE_AI_KEY): configured / not configured

Internal tools (your brand's own data)
- Google Search Console: configured / not configured
- Google Analytics 4: configured / not configured

LLM access (for AEO probes)
- ChatGPT Plus / Claude Pro / Perplexity Pro: user-confirmed
```

For each external tool flagged "not configured", ask:

> "`{Tool}` is not configured. Want me to look up the current sign-up steps and API-key retrieval flow, so we can populate more of the analysis? Answer `yes`, `no`, or `skip all`."

If `yes`: use WebSearch and WebFetch to pull the current sign-up flow for that specific tool (pricing, free-tier availability, API-key retrieval location, exact `.env` variable name). Produce step-by-step instructions the user can follow in 5 minutes.

If `no`: skip that tool, move to the next.

If `skip all`: proceed to Step 3 with the current credentials.

Never hardcode sign-up URLs or pricing from memory. Pull fresh from the web every time.

---

## Step 3. Detect the mode

Auto-detect based on `.env` inventory and `CLAUDE.md` fields:

| Mode | Trigger |
|---|---|
| Full-A | Established brand (30+ indexed pages, GSC configured), user wants full depth |
| Full-B | Greenfield brand (under 30 indexed pages or pre-launch), user wants full depth |
| Quick | User explicitly wants quick mode, one competitor |
| AEO-only | User wants AEO focus only, skip keyword-gap layer |
| Cluster-deep | User picks one cluster up front, wants 20 briefs inside it |

State the detected mode. Ask the user to confirm or override. Record in the report header.

---

## Step 4. Draft the eight sections

Produce all eight sections of the report in drafting mode. Do not write to disk yet.

### Section 1. Own-site content inventory

Runs on Path A only. On Path B, stub: "Greenfield brand. Own-site inventory covers product and category pages only. Full content inventory unlocks once the first editorial cluster ships."

On Path A:
- Crawl the brand's domain via Screaming Frog CLI, or WebFetch the sitemap and iterate. Export URL, title, meta description, canonical, word count, H1, internal-link count, indexable status.
- Cross-reference with GSC top 1,000 queries if GSC configured. For each URL, tag currently-ranking query, current position, impressions over 90 days, CTR.
- Classify each page by content type: pillar, cluster sub-page, product page, category page, blog post, landing page, other.
- Flag orphan pages, thin pages (under 300 words), outdated pages (last-modified over 18 months).

Deliverable: CSV at `data/content-gap/{YYYY-MM-DD}/own-site-inventory.csv` plus a 200-word narrative.

### Section 2. Competitor content footprint

External layer. For each competitor URL:
- Pull top 100 organic keywords via Ahrefs or DataForSEO `labs_ranked_keywords`. Capture keyword, volume, difficulty, position, landing-page URL.
- Pull top 50 organic landing pages. Capture URL, page title, estimated monthly organic traffic, top ranking keyword.
- Cluster the top 50 pages into 4 to 8 topic buckets per competitor. Labels in plain English.
- Identify each competitor's strongest cluster.

Deliverable: per-competitor CSV plus a 150-word narrative per competitor.

### Section 3. Keyword gap

Set-difference analysis.
- Pull the client's ranking keywords (top 100) via DataForSEO `labs_ranked_keywords` or GSC top-queries export.
- Pull each competitor's ranking keywords the same way.
- For each competitor, compute `competitor_keywords - client_keywords` in Python. Union across all competitors to form the full gap list.
- Filter to keywords with KD under 40 and monthly volume above 30. Relax to KD 60 for high-authority brands.
- Enrich each surviving keyword: SERP intent (informational, commercial, transactional, navigational), CPC, SERP features present.

Deliverable: `data/content-gap/{YYYY-MM-DD}/keyword-gap-raw.csv` plus a 200-word narrative on the 3 to 5 themes dominating the gap.

**Critical tool-note:** do not use `seo_toolkit.py keyword-research` gap mode or DataForSEO `labs_keyword_intersection`. Both return intersections (keywords both domains rank for) when the analysis needs the set difference. Compute the delta manually in Python.

### Section 4. AEO citation audit

External layer.
- Draft 30 to 50 category questions covering the full buyer journey. Cover early-stage ("what is X"), mid-stage comparison ("X vs Y"), late-stage commercial ("best X for Y"), post-purchase support ("how to use X").
- Probe each question across ChatGPT (with browsing), Claude (with web search), Perplexity, Google AI Overview (via Serper).
- Record: is the client cited, which competitors are cited, does an AI Overview or LLM answer exist, what sources are cited.
- Classify each question into: competitor-owned, category-whitespace, client-present, unanswered.

Deliverable: `data/content-gap/{YYYY-MM-DD}/aeo-probe-log.csv` plus a 250-word narrative.

### Section 5. SERP intent map and topic clusters

Cluster every keyword from Section 3 and every question from Section 4 into 4 to 8 topic clusters.
- Start from Section 2's competitor cluster labels as the initial taxonomy.
- Keep labels in the ICP's register.
- Within each cluster, map every keyword and question to SERP intent.
- Identify the pillar opportunity per cluster (highest-volume informational keyword).
- Flag clusters where the keyword layer and AEO layer both show whitespace. These are double-hit clusters. Promote them in Section 7.

Deliverable: `data/content-gap/{YYYY-MM-DD}/clusters.md`.

### Section 6. Opportunity scoring

Every surviving keyword and AEO question gets scored. Composite 0 to 1,000.

| Factor | Weight | Scale |
|---|---|---|
| Volume | 25% | Log-scaled 1 to 10 |
| Ease of ranking (inverse KD) | 20% | 1 to 10 |
| AEO extractability | 20% | 1 to 10, manual |
| Commercial intent (CPC, intent) | 20% | 1 to 10 |
| Client fit | 15% | 1 to 10, manual |

**Score = Volume × Ease × AEO_extractability × Commercial_intent × Client_fit ÷ 100.** Rank descending. Top 20 to 50 enter the roadmap. Top 10 go to briefs.

Effort is a tiebreaker. Within a score band, prefer lower-effort pieces first.

Deliverable: `data/content-gap/{YYYY-MM-DD}/scored-opportunities.csv`.

### Section 7. Content pillar + cluster plan

Group the top 20 to 50 opportunities into their clusters. For each cluster:
- **Pillar page.** Working title, target keyword, length target, sub-page fan-out.
- **Sub-pages.** 3 to 8 sub-pages per cluster. Working title, target keyword, intent, length.
- **Internal-link map.** Sub-pages link up to the pillar. Pillar links down to sub-pages.
- **Publishing sequence.** Pillar first where cluster has no coverage. Sub-pages first where a pillar equivalent exists.

Deliverable: the cluster plan, 4 to 8 clusters with 20 to 40 sub-pages.

### Section 8. Top 10 full content briefs

For the top 10 scored opportunities, produce a full brief (300 to 500 words each). Each brief contains:

1. **Working title.** Optimised for SERP CTR.
2. **Target keyword** plus volume, KD, SERP intent.
3. **Secondary keywords.** 3 to 5 semantically related terms.
4. **Search intent and audience.** Two sentences.
5. **Competitor-beating angle.** What the top 3 SERP results miss.
6. **AEO-extraction structure.** H2s framed as questions. Direct-answer paragraph under each H2. FAQ block with 5 to 8 questions. Schema recommendations (Article, FAQ, HowTo, Product as applicable).
7. **Internal-link map.** 3 to 6 internal links.
8. **Recommended external citations.** 3 to 5 authoritative sources (Princeton GEO cite-sources effect: +40% visibility).
9. **Statistics to include.** 2 to 4 category statistics with named sources (+37% visibility).
10. **Expert quotes.** 1 to 2 quotes with name, title, source (+30% visibility) if attainable.
11. **Word count target.** 1,200 to 3,500 words based on SERP depth.
12. **Production lift.** One line on what producing this takes.

---

## Step 5. Synthesis pass (mandatory before writing to disk)

Do not write the report yet. Assemble Sections 1 through 8 plus the 30-60-90 plan as a single draft in working context. Read end-to-end in one pass. Ask:

- What pattern emerges across three or more sections that no single section captures?
- Which clusters show whitespace in both the keyword layer (Section 3) and the AEO layer (Section 4)? Those are the double-hit priorities.
- Does the 30-60-90 plan target the right intents? Are informational pillars sequenced before commercial sub-pages?
- Does any Section 8 brief address multiple leverage points at once? Promote it.
- Does any high-ranked Section 8 brief solve only one problem? Consider demoting in favour of multi-leverage plays.

Produce 3 to 5 cross-cutting insight bullets. Each bullet:
- States the insight in one sentence.
- Names the sections it spans in brackets.
- Is a synthesis of cross-section implications.

Then revise:
- **Executive Summary** to lead with the narrative these insights reveal (3 to 4 sentences).
- **Section 8** re-ranked to promote multi-leverage briefs.
- **Cross-cutting themes** block populated with the bullets.
- **Key findings** block (5 to 7 one-sentence bullets, one per section).
- **Top 10 table** populated from the re-ranked list.
- **Conclusion** block at the end (2 to 3 paragraphs: what to publish this week, what a paid engagement looks like, book-a-call at `https://entirecommerce.ai/audit`).

---

## Step 6. Voice enforcement gate (mandatory before writing)

Grep the full draft. Rewrite every match.

| Banned | Grep for | Fix |
|---|---|---|
| Em-dash | `—` or `--` | Period, comma, or colon |
| Negative parallelism | `, not `, ` rather than `, ` instead of `, `opposite of `, `not only ` | State the positive alone |
| Banned spelling | `e-commerce`, `E-commerce`, `E-Commerce` | `ecommerce` |
| AI clichés | `Here's the`, `Here's what`, `Here's why`, `Most people`, `The uncomfortable truth`, `The brutal truth`, `The breakthrough` | Rewrite |
| Sub-four-word sentence | 1 to 3 word sentences | Merge or expand |

`not` is permitted only when the negation is genuinely load-bearing. Shipping with more than zero matches is a spec violation.

---

## Step 7. Write outputs

Report structure (fixed order):

```
# Content Gap + AEO Opportunity Report: {Brand} ({YYYY-MM-DD})

Mode: {Full-A / Full-B / Quick / AEO-only / Cluster-deep}
Access level: {External only / External + GSC}

## Executive summary
## Cross-cutting themes
## Key findings
## Top 10 briefed opportunities (quick-reference table)
## 1. Own-site content inventory
## 2. Competitor content footprint
## 3. Keyword gap
## 4. AEO citation audit
## 5. SERP intent map and topic clusters
## 6. Opportunity scoring
## 7. Content pillar + cluster plan
## 8. Top 10 full content briefs
## 30-60-90 publishing plan
## Access-grant checklist (if GSC/GA4 missing)
## Conclusion
```

Write to:
```
{cwd}/docs/content-gap/{YYYY-MM-DD}/content-gap-report.md
```

Convert to Word doc:
```bash
pandoc {cwd}/docs/content-gap/{YYYY-MM-DD}/content-gap-report.md \
  -o {cwd}/docs/content-gap/{YYYY-MM-DD}/content-gap-report.docx \
  --toc --number-sections
```

If pandoc is not installed, tell the user: `brew install pandoc` on Mac. Do not skip the Word export silently.

Save supporting data to `{cwd}/data/content-gap/{YYYY-MM-DD}/`:
- `own-site-inventory.csv`
- `gsc-queries-top1000.csv` (Path A only)
- `competitor-rankings-{slug}.csv` (one per competitor)
- `keyword-gap-raw.csv`
- `aeo-probe-log.csv`
- `scored-opportunities.csv`
- `clusters.md`

**Exactly one consolidated report file.** If sub-agents returned per-section drafts, merge them into the single file before writing.

---

## Step 8. Merge into actions.md

If the current working directory has `actions.md`, merge the top 3 actions from the 30-60-90 plan's 30-day row into Next Actions. Respect caps: P0 max 5, P1 max 10, P2 max 15. Rescore by ICE and demote the weakest items before adding.

---

## Step 9. Commit (optional)

If the folder is a git repo, commit the report, Word doc, data files, and updated actions.md. Commit message:

```
Content gap: {Brand} ({YYYY-MM-DD}): {top cluster in 6 words}
```

---

## Voice conventions (strict)

- No em-dashes. Period, comma, or colon.
- No negative parallelisms. State the positive.
- Four-word sentence floor.
- "ecommerce" one word.
- No AI clichés.
- Every finding traces to real data. No fabricated volumes. No invented competitor rankings.
- If a section is stubbed, state it plainly with the access path.

---

## Acceptance criteria

- End-to-end from this one prompt. No manual copy-paste between steps.
- Correct mode detection with user confirmation.
- Single consolidated report at the output path. Cross-cutting themes, Key findings, Top 10 table, Conclusion blocks populated by the synthesis pass.
- Scored opportunity list of 20 to 50 entries. Top 10 briefs embedded, each with the 12-field brief structure.
- Word doc produced via pandoc alongside the markdown.
- No invented data. Missing GSC stubbed honestly with access-grant path.
- Voice enforcement gate run before write. Zero banned-pattern matches.

---

## What to do with the output

The top 3 briefs from Section 8 go to your writer this week. The cluster plan in Section 7 sequences the next quarter. Re-run the AEO probes monthly on a focused question set to track whether your new content has started earning citations. Re-run the full playbook quarterly.

Want this run for you on a live engagement with a weekly review cadence, a daily dashboard, and the thirty-plus downstream playbooks across every GTM function? Book a call at https://entirecommerce.ai/audit.
