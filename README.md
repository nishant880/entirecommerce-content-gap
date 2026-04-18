<div align="center">

---

### [Want us to run this for you? Book a call](https://entirecommerce.ai/audit)

---

</div>

# Content Gap + AEO Opportunity Playbook

## A content gap analysis that surfaces the exact 20 to 50 keywords your competitors rank for that you don't, the 30 to 50 questions ChatGPT and Perplexity cite competitors on while ignoring you, and the intent-mapped topic clusters your content programme should pursue next. Delivered as a Word doc plus the markdown source with 10 full content briefs ready to hand to a writer. Built by Nishant Kapoor at EntireCommerce AI.

---

<div align="center">

### Fastest way to use this playbook

**Paste this document's URL into Claude Code and say:**

> *"Read this and take me through it step by step."*

**Claude will interview you for the business context, walk you through any missing API setup, and run the full content-gap analysis end-to-end. You don't need to read the rest of this document.**

</div>

---

## Who This Playbook Is For

Three people use this playbook.

**The founder-led DTC brand owner running a content programme by intuition.** You have a blog. You publish two or three posts a month. You picked the topics yourself based on what felt useful. Traffic is flat. You suspect your competitors are mining a keyword list you cannot see, and you suspect ChatGPT cites them when buyers ask about your category. You want the data that tells you what to write next, ranked, with briefs ready to hand to a writer this week.

**The content-marketing lead at a funded DTC brand with a production team.** Your team of two writers ships four to six pieces a month. The editor-calendar conversation cycles through the same five-to-ten topics. You want a single document that sequences the next quarter's production in priority order, with full briefs that the writers can pick up and run. Your job becomes review and shipping. Ideation moves to the playbook.

**The fractional CMO managing a portfolio of DTC brands.** Every client asks "what should we write about?" and "how do we show up in AI answers?" You need a repeatable diagnostic that answers both questions in one artefact, across every client. This playbook is the same process every time: eight sections, scored opportunities, 10 briefs, publishing plan.

If you have been picking topics from a Google Keyword Planner screenshot and hoping, this playbook collapses the discovery, scoring, and briefing into one consolidated output in a single Claude Code session.

---

## What The Content Gap Playbook Actually Is

**The short version.** Eight sections in one consolidated report. Claude runs the synthesis end-to-end: inventories your existing content, pulls your competitors' top-ranking keywords, computes the set-difference to surface your keyword gap, probes ChatGPT, Claude, Perplexity, and Google AI Overview on 30 to 50 category questions to surface your AEO citation gap, maps both layers into topic clusters with SERP intent, scores every opportunity on a composite Volume × Ease × AEO-extractability × Commercial-intent × Client-fit rubric, groups them into a pillar-and-cluster plan, and writes 10 full content briefs for the top 10 scored pieces. Plus a synthesis pass that surfaces 3 to 5 cross-cutting themes across the keyword, AEO, and intent layers, the strategic narrative your content programme reveals when every finding is in view at once.

**Best for.** Premium DTC brands. AOV $500+ or 2x category median. Founder-led. US or English-speaking market focus. Either 6+ months of organic activity with at least 30 indexed pages, or greenfield brands willing to publish one to two pieces a week for two quarters.

**How it's different.** Three things most content-gap tools skip.

First, **SEO and AEO synthesised in one view**. Every other content-gap tool runs the keyword layer alone. Ahrefs ships a content-gap button. DataForSEO has keyword-intersection mode. Neither surfaces the LLM citation whitespace separately, then overlays both. Double-hit clusters, where the keyword layer and the AEO layer both show competitor dominance, get promoted to the top of the roadmap. That ranking signal only surfaces when both layers run in the same pass.

Second, **the synthesis pass**. Section-by-section output is a directory of findings. The synthesis pass is the story. A SERP-intent cluster in Section 5 might imply a pillar architecture in Section 7 that compounds into AEO authority on a cluster-of-questions in Section 4. None of those connections surface from a section-at-a-time read. Claude does the cross-read explicitly, then revises the Executive Summary to lead with the narrative.

Third, **the output is production-ready**. Most content-gap deliverables stop at a keyword list. This playbook ships the keyword list, the cluster architecture, the pillar-and-cluster map, and 10 full content briefs: target keyword, secondary keywords, search intent, competitor-beating angle, H2 structure tuned for AEO extraction, FAQ block, schema recommendations, internal-link map, external-citation recommendations, statistics to include, word-count target. Your writer picks up the doc and starts drafting.

**Skip this playbook if** you have fewer than three named competitors, a category with zero search volume (too niche to rank), or a brand with zero intent to publish more than one piece a month. The playbook's output assumes a sustained publishing cadence.

---

## Setup (15 Minutes)

### Prerequisites

- **Claude Code** installed. Verify with `claude --version`.
- **pandoc** installed for Word-doc export. On macOS: `brew install pandoc`. Verify with `pandoc --version`.
- **A project folder** on your machine. One per brand.

### Cost overview

The playbook itself is free. You pay for API credits consumed by the tools the analysis uses.

| Tool | Subscription model | Typical per-run cost | Role |
|---|---|---|---|
| DataForSEO | Pay-as-you-go, no monthly fee | **$2 to $12** | Recommended. Competitor keyword footprint, SERP enrichment. Heaviest spender. |
| Serper | Free tier gives 2,500 credits | Under $1 | Recommended. SERP + AI Overview probes. |
| Keywords Everywhere | ~$10 one-time for 100K credits | Under $0.50 | Recommended. Volume lookups. |
| Ahrefs | $129+ per month | Optional | If you already have a seat, the native content-gap tool is the fastest single-tool shortcut. Skip otherwise. |
| ChatGPT Plus / Claude Pro / Perplexity Pro | $20/month each | Varies | Recommended at least one. Required for AEO citation probes. |
| Google Search Console | Free (your own account) | $0 | Internal tool. Share via service account for Path A depth. |
| Google Analytics 4 | Free | $0 | Internal tool. Optional enrichment. |

**Typical total cost per full run: $3 to $20** across the paid external tools, assuming you already hold LLM subscriptions.

Numbers are approximate as of April 2026. Pricing changes. The master prompt offers live sign-up lookups for any missing tool.

### Step 1: Create the project folder

```bash
mkdir my-brand-content-gap && cd my-brand-content-gap
```

Drop the three files from this bundle (CLAUDE.md, content-gap.md, README.md) into the folder.

### Step 2: Set up your .env

Create `.env` in the project folder. Add the API keys you have. If you are missing any, run the master prompt and Claude offers to walk you through sign-up for each missing tool before starting the analysis.

Minimum recommended `.env`:

```
DATAFORSEO_LOGIN=your_login
DATAFORSEO_PASSWORD=your_password
DATAFORSEO_AUTH_BASE64=your_base64_auth
SERPER_API_KEY=your_key
KEYWORDS_EVERYWHERE_API_KEY=your_key
GOOGLE_AI_KEY=your_google_cloud_api_key
AHREFS_API_KEY=your_key_if_you_have_one
```

**Gotcha:** Never commit `.env` to a public repo. Add it to `.gitignore` before the first commit.

### Step 3: Populate CLAUDE.md (or let Claude interview you)

Two options:

**Option A (recommended).** Leave `CLAUDE.md` as-is. Run the master prompt. Claude interviews you conversationally and writes the file for you. Takes about 10 minutes.

**Option B (DIY).** Open `CLAUDE.md` and replace every `{placeholder}` with your specifics before running the analysis.

**Gotcha:** The 3 to 5 competitor URLs are load-bearing. Without them, Claude has to auto-discover competitors from the SERPs. Auto-discovery usually works but hand-picked competitors always produce sharper gap analysis.

### Step 4: Open Claude Code in the folder

```bash
claude
```

Claude Code loads `CLAUDE.md` on session start. Confirm you see "Loaded CLAUDE.md" in the session log.

---

## The Three Files in This Bundle

### File 1: CLAUDE.md (business-briefing template)

**Path:** `{your-project-folder}/CLAUDE.md`
**What it does:** Claude Code loads this on every session start. Your brand's specifics live here: product, audience, positioning, current content footprint, competitor URLs, AEO priorities.
**How to use it:** Replace every `{placeholder}` with your specifics. Keep it tight, founder voice over marketing copy.

### File 2: content-gap.md (the master prompt Claude runs)

**Path:** `{your-project-folder}/content-gap.md`
**What it does:** The prompt Claude executes end-to-end to produce the content-gap analysis. Covers all eight sections plus the synthesis pass plus the voice gate plus the pandoc export.
**How to use it:** Paste its contents into Claude Code and hit enter. Do not edit the structure unless you know what you are doing.

### File 3: README.md

**Path:** `{your-project-folder}/README.md`
**What it does:** You are reading it. Setup, run, troubleshooting reference.

---

## Your First Run

Five steps. Thirty to sixty minutes.

1. **Open Claude Code in your project folder.** `cd my-brand-content-gap && claude`
2. **Paste the full contents of `content-gap.md` into the terminal.** Hit enter.
3. **Claude prints a credential inventory.** External tools first, GSC and GA4 second. Missing tools flagged with an offer to walk you through sign-up.
4. **Claude auto-detects the mode** (Full-A, Full-B, Quick, AEO-only, or Cluster-deep) based on your data maturity and scope request. Confirm or override.
5. **Claude runs the analysis.** Inventories your existing content, pulls competitor rankings, computes the keyword gap, probes the four LLMs on your category questions, maps clusters, scores every opportunity, writes 10 briefs, runs the synthesis pass, runs the voice gate, writes the report.

Output lands at:

```
{your-project-folder}/docs/content-gap/YYYY-MM-DD/content-gap-report.md
{your-project-folder}/docs/content-gap/YYYY-MM-DD/content-gap-report.docx
```

Plus supporting CSVs and the AEO probe log in `{your-project-folder}/data/content-gap/YYYY-MM-DD/`.

---

## What You'll Get

Ten high-value deliverables in one consolidated report.

1. **Executive summary with cross-cutting themes.** A 3-4 sentence narrative plus 3-5 strategic insights spanning multiple sections. Produced by a dedicated synthesis pass. The story of your content opportunity surface as a single narrative.
2. **Own-site content inventory.** Every indexed page on your site tagged by type, word count, ranking query, GSC position, impressions, CTR. Flags orphan pages, thin pages, outdated pages.
3. **Competitor content footprint.** Top 100 ranking keywords and top 50 landing pages for each of 3 to 5 competitors. Clustered into topic buckets. Identifies each competitor's strongest cluster.
4. **Keyword gap analysis.** The set-difference of competitor keywords minus client keywords, filtered to KD under 40 and volume above 30. Enriched with SERP intent, CPC, and SERP-feature presence.
5. **AEO citation audit.** 30 to 50 category questions probed across ChatGPT, Claude, Perplexity, and Google AI Overview. Every question classified into competitor-owned, category-whitespace, client-present, or unanswered. The whitespace and competitor-owned buckets are the AEO roadmap.
6. **SERP intent map and topic clusters.** Every keyword and AEO question mapped to intent (informational, commercial, transactional, navigational) and grouped into 4 to 8 plain-English topic clusters. Double-hit clusters (keyword whitespace plus AEO whitespace) flagged.
7. **Opportunity scoring.** Every surviving opportunity scored on Volume × Ease × AEO-extractability × Commercial-intent × Client-fit. Ranked descending. Top 20 to 50 enter the roadmap.
8. **Content pillar and cluster plan.** The top 20 to 50 opportunities grouped into their clusters. Each cluster gets a pillar page, sub-pages, internal-link map, and publishing sequence.
9. **Top 10 full content briefs.** Production-ready briefs for the top 10 scored opportunities. Each brief covers target keyword, secondary keywords, search intent, competitor-beating angle, AEO-extraction structure, FAQ block, schema recommendations, internal-link map, external-citation recommendations, statistics to include, word-count target, production lift.
10. **30-60-90 publishing plan and conclusion.** A calendar mapping the top 10 briefs plus the next 10 to 20 opportunities across three horizons. Followed by a conclusion with what to publish this week and an optional paid-engagement path.

**Format.** One consolidated Word doc plus the markdown source in your GitHub repo. Typically 5,000 to 9,000 words. Reading time around 30 minutes cover to cover, 90 seconds to skim via the Key Findings block at the top.

---

## Modes

The playbook auto-detects which mode applies and adapts section depth.

| Mode | When it applies | What changes |
|---|---|---|
| Full-A | Established brand with 30+ indexed pages, GSC configured | Own-site inventory populates fully. Keyword gap uses both GSC and competitor data. Deepest analysis. |
| Full-B | Greenfield brand with minimal indexed content | Gap analysis runs bottom-up from competitor footprint. Section 1 stubs with a note on greenfield framing. |
| Quick | Any data maturity, one competitor, 10 opportunities, 5 briefs | Runs in 20 to 30 minutes. Best for first-look scoping. |
| AEO-only | Any data maturity | Skips Section 3 (keyword gap). Full depth on Section 4 (AEO) with 50+ questions probed. Top 15 questions briefed. |
| Cluster-deep | Any data maturity | One cluster chosen up front. 20 briefs inside that cluster across informational, commercial, transactional intents. |

---

## Honest Caveats

**The AEO probe layer is sample-based.** Thirty to fifty questions is a meaningful sample of a category but it is not exhaustive. Re-run the AEO section monthly on a tighter focus list once the first content ships, to track whether the brand has started showing up.

**LLM answers drift week to week.** A question ChatGPT cites a competitor on today may not surface that competitor next month. The AEO snapshot captures the state at the time of the run. Treat individual probe results as directional evidence. The cluster-level pattern (competitor-owned vs category-whitespace) is the durable signal.

**Keyword difficulty scores are approximations.** Different tools (Ahrefs, DataForSEO, Semrush) disagree by up to 15 points on the same keyword. The relative ranking within the report is robust. The absolute KD thresholds (KD under 40) are calibrated to DataForSEO. Relax or tighten depending on your brand authority and the tool you trust.

**Voice rules are strictly enforced.** Claude runs a mechanical grep-pass for em-dashes, negative parallelisms, banned spellings, and AI clichés before writing the report. If a banned pattern slips through, flag it and re-run the gate.

**GSC access is the single biggest Path A lever.** Without GSC, Section 1 (own-site inventory) degrades to a public Screaming Frog crawl with no query or CTR layer. Plan on spending 5 to 10 minutes wiring up GSC access before the first run.

**API costs are real but small.** A typical full run costs $3 to $20 across the paid external tools, assuming you already hold LLM subscriptions. Full breakdown in the Cost overview table.

**The playbook is tuned for premium DTC.** Edge cases: B2B SaaS, service businesses, local-intent brands. The methodology still applies but the cluster templates and brief patterns will need adaptation.

---

## Quick-Start Checklist

- [ ] Claude Code installed (`claude --version` works)
- [ ] pandoc installed (`pandoc --version` works)
- [ ] Project folder created for the brand
- [ ] CLAUDE.md and content-gap.md from this bundle copied into the folder
- [ ] DataForSEO account created and credentials added to `.env`
- [ ] Serper API key added to `.env`
- [ ] Keywords Everywhere API key added to `.env`
- [ ] ChatGPT Plus, Claude Pro, or Perplexity Pro subscription active (needed for AEO probes)
- [ ] GSC access granted to the EntireCommerce service account (for Path A depth)
- [ ] CLAUDE.md populated, every placeholder replaced
- [ ] First run executed and Word doc produced at `docs/content-gap/{date}/`
- [ ] Report reviewed, top 3 briefs handed to the writer this week
- [ ] Re-run quarterly to refresh the roadmap as the market shifts
- [ ] Book a call if you'd rather we run this for you on a live engagement: [entirecommerce.ai/audit](https://entirecommerce.ai/audit)

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| "pandoc not found" at Word-doc export | pandoc not installed | `brew install pandoc` (macOS) |
| Section 3 returns an empty gap table | Wrong DataForSEO call (keyword-intersection returns shared keywords when the analysis needs the set difference) | Known bug trap. Playbook computes set-difference in Python. A clean run handles this automatically. |
| AEO probes return empty for Google AI Overview | Serper credits exhausted, or query has no AI Overview | Check Serper dashboard. If credits OK, accept that many queries simply do not trigger an AI Overview. Move on. |
| Claude skips sections 2 or 3 | Competitor URLs missing from CLAUDE.md | Populate the "Three competitors the buyer also considers" field in CLAUDE.md and re-run. |
| Voice gate flags em-dashes or "X, not Y" patterns | Style drift in sub-agent output | Paste the banned-patterns list back into Claude and ask for a scan-and-fix pass. |
| Report splits into per-section files | Sub-agent split issue | Re-run. Spec explicitly bans per-section files as primary deliverable. |
| Keyword gap table has only 3 or 4 entries | KD and volume thresholds too tight for the brand's authority | Relax thresholds in Section 3 (KD under 60, volume above 10) and re-run Step 4. |

---

## Credit

Built by Nishant Kapoor at EntireCommerce AI.

- **LinkedIn**: [linkedin.com/in/nishantkapoor1](https://www.linkedin.com/in/nishantkapoor1)
- **Email**: nishant@entirecommerce.co
- **Book a call**: [entirecommerce.ai/audit](https://entirecommerce.ai/audit)
- **Full playbook library**: [entirecommerce.ai/playbooks](https://entirecommerce.ai/playbooks)

Use this playbook freely. Share it with other DTC founders. If you ship a case study running it on your brand, tag us. We will link to it from the site.
