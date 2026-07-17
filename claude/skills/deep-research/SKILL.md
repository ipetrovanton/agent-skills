---
name: deep-research
description: >
  Conduct deep, multi-phase research on any subject using SearXNG and web_fetch.
  Produces comprehensive 50-100 page markdown reports with full source citations.
  Use whenever the user asks to research something deeply, requests a deep dive, full
  report, comprehensive analysis, or any research task requiring substantial depth.
  Triggers on phrases like "research X", "deep research on X", "do a deep dive on X",
  "write a report on X", "I want to know everything about X".
---

# Deep Research Skill

Produces 50-100 page comprehensive research reports via systematic multi-phase searching, content extraction, and synthesis.

## Phase 0: Intake

Before starting research, ask Tom these questions in a single message. Do not start researching until you have answers.

**Questions to ask:**
1. What is the exact topic or question? (Be as specific as possible — e.g. "Bitcoin mining economics in 2026" not just "Bitcoin")
2. What is this research for? (personal learning, investment due diligence, business strategy, content creation, etc.)
3. Which specific angles or subtopics must be covered? Any you want excluded?
4. What's your existing knowledge level? (beginner / familiar / expert)
5. Time scope: historical background needed, or recent developments only, or both?
6. Any sources, organizations, or viewpoints to prioritize or avoid?
7. Where should the report be saved? (default: `research/[topic-slug]-[date].md`)

Wait for answers before proceeding.

## Phase 1: Research Architecture

Based on intake answers, plan the research before searching:

1. **Define the topic tree**: Break the subject into 6-12 major subtopics/sections
2. **Draft report outline**: Write section headings for the full report before you start searching
3. **Write 30-50 search queries**: Cover every angle — definitions, history, current state, key players, controversies, data/statistics, expert opinions, criticism, future outlook, comparisons, case studies

Query strategy — run searches across these dimensions:
- Fundamentals: `"[topic] explained" "[topic] overview" "[topic] guide"`
- Current state: `"[topic] [current year]" "[topic] news [current year]"`
- Data/stats: `"[topic] statistics" "[topic] data" "[topic] research study"`
- Players/orgs: `"[topic] companies" "[topic] leaders" "[topic] experts"`
- Controversy: `"[topic] criticism" "[topic] problems" "[topic] debate"`
- Comparisons: `"[topic] vs [alternative]" "[topic] alternatives"`
- Deep dives: specific subtopic queries for each section in your outline
- Academic/expert: `"[topic] study" "[topic] academic" "[topic] analysis"`

## Phase 2: Search Execution

Run searches systematically using SearXNG:

```bash
node scripts/searxng.mjs "your query here" --count=10 --engines=google,bing
```

**Rules:**
- Run at least 25 searches, ideally 40+
- Vary queries widely; avoid repetitive near-duplicate queries
- For each search, collect: page title, URL, snippet
- Curate a reading list of 40-80 URLs — prioritize: primary sources, expert analysis, data, long-form journalism, academic papers, official org pages
- Exclude: thin aggregator pages, listicles with no depth, paywalled pages with no preview content

Track every URL you plan to fetch in a running source list with format:
```
[Title] — URL — [category: data/expert/news/official/analysis]
```

## Phase 3: Content Extraction

Read actual page content for all prioritized URLs using `web_fetch`:

```
web_fetch(url, extractMode="markdown", maxChars=15000)
```

**Process:**
- Fetch 40-80 pages
- Extract key facts, quotes, data points, arguments
- Note the source URL for every piece of information you extract
- If a page is thin or irrelevant, skip it and replace with another URL
- For statistics/data: note the exact figure, source, and date
- For expert quotes: capture verbatim with attribution

Keep a running notes file at `research/[topic-slug]-notes.md` as you go. Use it to accumulate raw findings before synthesis. Structure it by your outline sections.

## Phase 4: Report Synthesis

Write the full report. Target: **20,000-40,000 words** (50-100 pages at ~400 words/page).

**Report structure:**

```markdown
# [Full Topic Title]

**Research Date:** [date]
**Prepared by:** Rue
**Purpose:** [from intake]

---

## Executive Summary

[600-1000 word summary of key findings, conclusions, and implications]

---

## Table of Contents

[Auto-generated from section headings]

---

## 1. Introduction

[Context, why this topic matters, scope of this report, methodology note]

## 2. [Section based on outline]

### 2.1 [Subsection]
...

## 3-N. [Remaining sections — each 1,500-4,000 words]

...

## [N]. Conclusions & Implications

[Synthesis of key findings, actionable takeaways, open questions]

---

## Sources

[Full URL list — see Source Formatting below]
```

**Writing standards:**
- Every factual claim must have an inline citation: `[Source Name](URL)`
- Use headers, subheaders, bullet points, and tables to structure dense content
- Include data tables where you have comparable figures across sources
- Quote experts directly where the exact wording matters
- Do not hedge excessively — state findings clearly, note uncertainty where it genuinely exists
- Never use em dashes (use colons, semicolons, or split sentences)
- No AI-isms: no "delve into", "landscape", "pivotal moment", "underscores the importance"
- Tone: authoritative, direct, like a senior analyst briefing an executive

**Section depth targets:**
- Intro/context: 800-1,200 words
- Each major section: 2,000-4,000 words
- Each subsection: 500-1,500 words
- Conclusions: 1,000-1,500 words

## Phase 5: Sources Section

The final section of every report must be titled **Sources** and list every URL used.

Format:
```markdown
## Sources

### Primary Sources
- [Organization Name — Document Title](URL)

### News & Journalism
- [Publication — Article Title](URL)

### Research & Analysis
- [Author/Org — Title](URL)

### Data & Statistics
- [Source — Dataset/Report Name](URL)

### Expert Commentary
- [Name/Platform — Title](URL)
```

Minimum 40 sources. Aim for 60-100.

## Phase 6: Save & Deliver

1. Save the full report to the path agreed in intake (default: `research/[topic-slug]-YYYY-MM-DD.md`)
2. Delete the scratch notes file (`research/[topic-slug]-notes.md`)
3. Tell Tom: report path, word count, page estimate, source count, and 3-bullet summary of key findings

## Execution Note

Deep research takes significant time and many tool calls. Spawn as an isolated sub-agent:

```
sessions_spawn(task="[full research brief with intake answers]", runTimeoutSeconds=3600)
```

Include the full intake answers and outline in the task prompt. The sub-agent should follow this skill's phases exactly.
