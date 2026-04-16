# Product Feedback Analyser

A practical workflow design for turning raw customer feedback into prioritised product opportunities, using Qualtrics, Excel, and Microsoft Copilot.

---

## 1. Product definition

**Product name:** Signal — Product Feedback Analyser

**What it is:** Signal is a lightweight, repeatable workflow (not a piece of software) that consolidates customer feedback from multiple channels into a single Excel workbook, uses Microsoft Copilot to surface themes and pain points, and outputs a prioritised list of product opportunities ready to feed into roadmap and backlog conversations.

**Who it is for:**
- Product Managers who own a product area and need evidence-based prioritisation
- Product teams that receive feedback across multiple channels but lack a consistent way to synthesise it
- Cross-functional partners (design, research, CX, engineering leads) who need a shared view of what customers are actually saying

**Core purpose:** To convert large volumes of unstructured customer feedback into a structured, prioritised set of opportunities that can directly influence product decisions.

**Main value to a product team:**
- A single source of truth for customer feedback
- A repeatable rhythm that does not depend on one person's memory
- Prioritisation grounded in evidence rather than the loudest voice in the room
- Faster path from "we heard something" to "we decided something"

---

## 2. Problem being solved

**The problem:** Customer feedback arrives through multiple channels (surveys, support tickets, sales calls, app store reviews, user interviews) and sits in silos. Without a consolidation and synthesis step, the team cannot see what matters most or where to invest.

**Why the current state is inefficient:**
- Feedback lives in different tools owned by different teams
- No shared categorisation, so the same pain point gets described five different ways
- Volume makes it impossible to read everything manually each cycle
- Recency bias takes over — whatever was raised last week feels most urgent
- No link between what customers said and what gets built

**Why feedback often fails to influence prioritisation:**
- It is not summarised in a form leadership can act on
- It is anecdotal rather than aggregated
- It is not weighted by frequency, severity, or strategic fit
- It is presented after the roadmap is already set, not before
- PMs default to assumptions because synthesising raw feedback is time-consuming

**Why this analyser improves product decision-making:**
- Forces consolidation into one structured place
- Uses Copilot to do the heavy lifting on pattern detection
- Produces a prioritised opportunity list on a regular cadence
- Creates a defensible audit trail: every opportunity links back to real customer evidence
- Replaces "I think customers want X" with "Here is what 47 customers said, grouped into 6 themes, ranked by impact"

---

## 3. End-to-end workflow

| Step | Stage | What happens | Who owns it |
|---|---|---|---|
| 1 | **Collect** | Feedback gathered via Qualtrics surveys, plus exports from support, app stores, and interview notes | PM + CX |
| 2 | **Consolidate** | All feedback pasted/imported into the `Raw Feedback` sheet in the Excel workbook | PM |
| 3 | **Clean and prepare** | Remove duplicates, blank rows, off-topic responses; standardise dates and source tags | PM |
| 4 | **Categorise** | Tag each row with product area, customer segment, and feedback type (bug, usability, feature request, praise) | PM, Copilot-assisted |
| 5 | **Detect themes** | Copilot clusters semantically similar comments into named themes | Copilot, PM reviews |
| 6 | **Identify pain points** | Themes converted into named pain points with severity and frequency counts | PM |
| 7 | **Generate opportunities** | Each pain point translated into one or more product opportunity statements | PM |
| 8 | **Prioritise** | Opportunities scored against the prioritisation framework (Section 7) | PM, with team input |
| 9 | **Report** | Stakeholder summary and PM summary generated for the cadence review | PM |
| 10 | **Feed roadmap** | Top opportunities go into backlog grooming and quarterly planning | PM + engineering lead |

---

## 4. Inputs

The workflow standardises every piece of feedback against the following fields. The first block is captured at intake; the second block is added during analysis.

**Captured at intake:**

| Field | Type | Example |
|---|---|---|
| Feedback ID | Auto-increment | FB-00347 |
| Date received | Date | 2026-03-12 |
| Source | Text | Qualtrics, Zendesk, App Store, Sales call, Interview |
| Channel | Text | Survey, Ticket, Review, Verbal |
| Customer segment | Text | SMB, Enterprise, Free tier, Trial |
| Customer ID (optional) | Text | CUST-2241 |
| Product area | Text | Onboarding, Billing, Reporting, Mobile app |
| Feedback text | Long text | The verbatim comment |
| Language | Text | EN, FR, DE |

**Added during analysis:**

| Field | Type | Example |
|---|---|---|
| Feedback type | Text | Bug, Usability, Feature request, Praise, Question |
| Sentiment | Text | Positive, Neutral, Negative |
| Theme | Text | Slow report generation |
| Pain point category | Text | Performance, Discoverability, Reliability, Cost |
| Severity | 1–5 | 4 |
| Frequency (theme count) | Number | 23 |
| Opportunity area | Text | Improve report engine performance |
| Linked opportunity ID | Text | OPP-014 |
| Confidence in evidence | 1–5 | 4 |
| Notes | Long text | "Recurring across enterprise segment" |

---

## 5. Excel workbook design

**Workbook purpose:** A single file that holds everything from raw input to prioritised output, so any PM picking it up can trace any opportunity back to the comments that produced it.

**Sheets:**

| Sheet | Purpose | Key columns |
|---|---|---|
| `00 README` | How to use the workbook, cadence, owner, version | — |
| `01 Raw Feedback` | Every piece of feedback, one row each | All intake fields from Section 4 |
| `02 Tagged Feedback` | Same rows enriched with analysis fields | All analysis fields from Section 4 |
| `03 Themes` | One row per theme with description and count | Theme ID, name, description, frequency, dominant sentiment, linked product area |
| `04 Pain Points` | One row per pain point | Pain point ID, name, category, severity, frequency, linked themes |
| `05 Opportunities` | The opportunity backlog | Opportunity ID, statement, linked pain points, scores, total score, status |
| `06 Prioritised View` | Sorted view of top opportunities for stakeholders | Filtered/sorted from `05` |
| `07 Reports` | Snapshot summaries per cycle (monthly archive) | Cycle date, headline themes, top opportunities, decisions taken |
| `08 Glossary` | Standard tag definitions to keep tagging consistent | Tag, definition, example |

**How sheets connect:**
- `01` flows into `02` (same rows, enriched).
- `02` aggregates into `03` (themes) via theme tags.
- `03` rolls up into `04` (pain points) via pain point category.
- `04` generates entries in `05` (opportunities).
- `05` is filtered into `06` for stakeholder review.
- Every cycle, a snapshot is saved into `07`.

**Maintenance:**
- PM imports new feedback weekly into `01`.
- PM runs Copilot prompts to populate `02` analysis fields.
- PM reviews and corrects Copilot output (this is non-negotiable — see Section 12).
- PM updates scores in `05` monthly or when new evidence shifts the picture.

**Manual vs Copilot-assisted:**

| Manual (PM owns) | Copilot-assisted |
|---|---|
| Tag definitions and glossary | First-pass categorisation |
| Final theme names | Clustering similar comments |
| Severity scores | Sentiment tagging |
| Strategic alignment scoring | Drafting summaries |
| Final opportunity statements | Surfacing pattern candidates |
| Decision on what enters the roadmap | Drafting stakeholder reports |

---

## 6. Analysis logic

**Grouping similar feedback:** Comments are clustered by semantic similarity (Copilot reads phrasing, intent, and the product area tag). A cluster becomes a candidate theme when it contains at least 3 distinct customer comments. PM reviews and either confirms, splits, or merges clusters.

**Identifying themes:** A theme is a named pattern of related feedback (for example, "Difficulty finding saved reports"). Themes are short, customer-language, and specific enough to act on. Themes are not "bad UX" or "performance" — those are categories, not themes.

**Detecting recurring pain points:** A pain point is the underlying problem behind one or more themes. Recurrence is measured by frequency (how many comments) and reach (how many segments or product areas it touches). A pain point that appears in two segments at moderate frequency may matter more than one that spikes in a single segment.

**Separating symptoms from root problems:** For each theme, ask "why is the customer saying this?" twice. The first answer is usually the symptom ("the report is slow"); the second answer is closer to the root ("they cannot complete their Monday morning workflow on time"). Both are recorded; prioritisation considers the root.

**Distinguishing feedback types:**

| Type | Marker | Example |
|---|---|---|
| **Bug** | Something is broken or behaving incorrectly | "The export button does nothing on Safari" |
| **Usability issue** | Works as built but hard to use | "I could not figure out how to invite a teammate" |
| **Feature request** | Something missing | "I wish I could schedule reports" |
| **Praise** | Positive signal | "The new dashboard is much clearer" |
| **Question** | User confusion that may indicate a doc or UX gap | "Where do I change my billing address?" |

**Identifying opportunities from raw comments:** Each pain point produces one or more opportunity statements in the form: *"For [segment], improve [product area] so that [outcome the customer can achieve]."* This forces the opportunity to be customer-outcome-led rather than feature-led.

**Converting qualitative feedback into structured insight:** The pipeline is: verbatim comment → tagged row → cluster → theme → pain point → opportunity → score. Every opportunity in the backlog can be traced backwards through this chain to the original customer voices.

---

## 7. Prioritisation framework

A simple weighted scoring model. Every opportunity is scored 1–5 on each of six criteria:

| Criterion | What it measures | Weight |
|---|---|---|
| **Frequency** | How often this came up across feedback | 1.0 |
| **Severity** | How painful for the customer when it occurs | 1.0 |
| **Customer impact** | Breadth across segments and product areas | 1.0 |
| **Strategic alignment** | Fit with current product and company strategy | 1.5 |
| **Confidence in evidence** | Quality and consistency of the supporting feedback | 1.0 |
| **Implementation effort** | Inverse — lower effort scores higher (5 = small, 1 = very large) | 0.5 |

**Formula:**

```
Opportunity Score =
  (Frequency × 1.0)
+ (Severity × 1.0)
+ (Customer Impact × 1.0)
+ (Strategic Alignment × 1.5)
+ (Confidence × 1.0)
+ (Effort × 0.5)
```

**Maximum possible score:** 30.

**How to use it:**
- Score in a team session, not alone, to reduce single-person bias.
- Sort opportunities by total score for a starting view.
- Treat the score as a conversation starter, not a verdict. The PM still applies judgement on sequencing, dependencies, and timing.
- Re-score quarterly or whenever significant new evidence arrives.

---

## 8. Outputs

The workflow produces the following artefacts each cycle:

- **Top themes** — ranked list of recurring patterns with frequency counts
- **Top customer pain points** — the underlying problems behind the themes, with severity and reach
- **Opportunity backlog** — full list of opportunity statements with current scores
- **Prioritised recommendations** — top 5–10 opportunities recommended for action
- **Insight summaries** — short narrative explaining what changed since last cycle
- **Stakeholder-ready report** — one-page summary for leadership
- **PM working summary** — longer view for the product team
- **Roadmap recommendations** — proposed additions or re-sequencing of roadmap items, with evidence links

---

## 9. Microsoft Copilot usage

**How Copilot fits in:** Copilot is used inside Excel and Word to accelerate steps that would otherwise be slow manual work — clustering comments, drafting tags, summarising patterns, and producing first-draft reports. The PM remains the editor and decision-maker. Copilot is the analyst's assistant, not the analyst.

**Where Copilot helps most:**
- First-pass sentiment tagging on the `Tagged Feedback` sheet
- Clustering similar comments into candidate themes
- Drafting theme names and pain point descriptions
- Generating stakeholder and PM summaries
- Producing roadmap input narratives

**Where Copilot should not be relied on alone:**
- Final theme naming
- Severity and strategic alignment scoring
- Deciding what enters the roadmap

### 12 practical Copilot prompts

1. **Summarising themes**
   > "Read the comments in column [Feedback Text] of the Tagged Feedback sheet. Group them into 5–10 distinct themes. For each theme, give a short name, a one-sentence description, the number of comments, and 3 example quotes."

2. **Clustering related comments**
   > "Cluster the rows in the Tagged Feedback sheet by semantic similarity of the Feedback Text. Output a table with Cluster ID, suggested name, comment count, and the row IDs included."

3. **Identifying pain points**
   > "From the themes in the Themes sheet, identify the underlying customer pain points. For each pain point, provide a name, a category (Performance, Discoverability, Reliability, Cost, Other), and the themes it covers."

4. **Spotting common complaints**
   > "List the 10 most common complaints in the Tagged Feedback sheet, ordered by frequency. For each, provide a short label and the count."

5. **Surfacing opportunity areas**
   > "For each pain point in the Pain Points sheet, suggest 1–2 product opportunity statements in the format: 'For [segment], improve [product area] so that [outcome].' Keep them customer-outcome-led, not feature-led."

6. **Detecting sentiment patterns**
   > "Analyse sentiment across the Tagged Feedback sheet. Show the distribution of Positive, Neutral, and Negative feedback overall, then broken down by Product Area and Customer Segment. Flag any product area where Negative exceeds 50%."

7. **Summarising by customer segment**
   > "Summarise the top 3 themes and top 3 pain points for each Customer Segment in the Tagged Feedback sheet. Output as a table."

8. **Summarising by product area**
   > "For each Product Area in the Tagged Feedback sheet, summarise the dominant themes, the most severe pain points, and any standout positive feedback. Limit to 5 bullets per product area."

9. **Generating prioritised recommendations**
   > "Using the Opportunities sheet and the scoring formula in column [Total Score], list the top 10 opportunities. For each, give the opportunity statement, total score, and a one-sentence justification grounded in the evidence."

10. **Creating a stakeholder summary**
    > "Write a one-page summary for product leadership covering: (a) the 3 biggest customer pain points this cycle, (b) the top 5 prioritised opportunities, (c) what changed since last cycle, and (d) recommended next steps. Plain business language, no jargon."

11. **Creating a PM summary**
    > "Write a working summary for the product team covering: theme list with counts, pain point list with severity, opportunity backlog with scores, notable quotes, and open questions that need user research follow-up."

12. **Creating roadmap inputs**
    > "Translate the top 5 prioritised opportunities into roadmap-ready entries. For each, provide: title, problem statement, proposed outcome, supporting evidence summary, suggested success metric, and an effort indicator (S/M/L)."

---

## 10. Example output

### Sample feedback rows (illustrative)

| ID | Date | Source | Segment | Product Area | Feedback Text | Type | Sentiment |
|---|---|---|---|---|---|---|---|
| FB-201 | 2026-03-02 | Qualtrics | Enterprise | Reporting | "Reports take over a minute to load on Monday mornings." | Bug | Negative |
| FB-202 | 2026-03-02 | Zendesk | SMB | Onboarding | "I had no idea I needed to verify my email before inviting users." | Usability | Negative |
| FB-203 | 2026-03-03 | App Store | Free | Mobile app | "Crashes when I open the dashboard tab." | Bug | Negative |
| FB-204 | 2026-03-04 | Qualtrics | Enterprise | Reporting | "We need to schedule reports — exporting manually each week is painful." | Feature request | Negative |
| FB-205 | 2026-03-05 | Sales call | Enterprise | Billing | "Switching plans is confusing, I had to ask support." | Usability | Neutral |
| FB-206 | 2026-03-05 | Zendesk | SMB | Onboarding | "Took me 20 minutes to find where to add a teammate." | Usability | Negative |
| FB-207 | 2026-03-06 | Qualtrics | SMB | Reporting | "Love the new dashboard layout." | Praise | Positive |
| FB-208 | 2026-03-07 | Interview | Enterprise | Reporting | "If I could schedule the weekly export, I'd save an hour every Monday." | Feature request | Negative |
| FB-209 | 2026-03-08 | Zendesk | Trial | Onboarding | "I almost gave up before I figured out the verification step." | Usability | Negative |
| FB-210 | 2026-03-09 | App Store | Free | Mobile app | "Dashboard tab still crashing after the latest update." | Bug | Negative |

### Top 5 themes

1. Slow report generation (Enterprise, Reporting)
2. Confusing onboarding around verification and team invites (SMB and Trial)
3. Mobile dashboard crashes (Free, Mobile)
4. Demand for scheduled report exports (Enterprise)
5. Plan-switching friction (Enterprise, Billing)

### Top 5 pain points

| Pain point | Category | Severity | Frequency |
|---|---|---|---|
| Reports cannot be relied on for weekly workflows | Performance | 5 | High |
| New users get blocked during onboarding | Discoverability | 4 | High |
| App is unstable on key surface | Reliability | 5 | Medium |
| Manual export work is repetitive | Efficiency | 3 | Medium |
| Self-serve plan management is unclear | Discoverability | 3 | Low–Medium |

### Top 5 product opportunities

1. For Enterprise users, improve report engine performance so that weekly reports complete reliably under 15 seconds.
2. For SMB and Trial users, redesign the onboarding flow so that new users can invite a teammate within 5 minutes.
3. For Free users on mobile, fix dashboard tab crashes so that the app is stable across the most-used surface.
4. For Enterprise users, introduce scheduled report exports so that recurring weekly work can be automated.
5. For Enterprise users, simplify in-product plan switching so that customers can manage plans without contacting support.

### Prioritised opportunity table

| ID | Opportunity | Freq | Sev | Impact | Strat (×1.5) | Conf | Effort (×0.5) | Total |
|---|---|---|---|---|---|---|---|---|
| OPP-01 | Improve report engine performance | 5 | 5 | 4 | 5 (7.5) | 4 | 2 (1.0) | **26.5** |
| OPP-02 | Redesign onboarding around verification & invites | 4 | 4 | 4 | 4 (6.0) | 4 | 4 (2.0) | **24.0** |
| OPP-03 | Fix mobile dashboard crash | 4 | 5 | 3 | 3 (4.5) | 5 | 3 (1.5) | **23.0** |
| OPP-04 | Scheduled report exports | 3 | 3 | 3 | 4 (6.0) | 4 | 3 (1.5) | **20.5** |
| OPP-05 | Simplify in-product plan switching | 2 | 3 | 2 | 3 (4.5) | 3 | 4 (2.0) | **16.5** |

---

## 11. Operating model

**Cadence:**

| Activity | Frequency |
|---|---|
| Import new feedback into `Raw Feedback` | Weekly |
| Tag and enrich into `Tagged Feedback` | Weekly |
| Run theme + pain point analysis | Monthly |
| Score and re-score opportunities | Monthly |
| Stakeholder review | Monthly |
| Roadmap input | Quarterly (and ad hoc when something major emerges) |

**Owners:**

| Step | Owner |
|---|---|
| Feedback collection | PM (with CX support) |
| Consolidation and cleaning | PM |
| Tagging and enrichment | PM, Copilot-assisted |
| Theme and pain point review | PM, with designer/researcher input |
| Opportunity scoring | PM, with team |
| Stakeholder reporting | PM |
| Roadmap decisions | PM with engineering and product leadership |

**Review rituals:**
- **Weekly 30-min PM hygiene slot** — import, clean, tag.
- **Monthly 60-min insight review** — PM walks team through new themes, pain points, and proposed opportunities.
- **Quarterly roadmap input session** — top opportunities formally considered for the next quarter's plan.

**How insights feed into backlog and roadmap:**
- Top opportunities each cycle become candidates for backlog grooming.
- Each opportunity carries its evidence trail, so backlog items can be defended and explained to stakeholders.
- The Reports archive (`07 Reports`) provides the longitudinal view: which pain points are persistent, which have been resolved, which are emerging.

**Keeping it sustainable:**
- Time-box each step. If tagging takes more than 60 minutes a week, the inflow needs filtering, not more PM hours.
- Keep the glossary tight — fewer, clearer tags beat sprawling taxonomies.
- Archive monthly snapshots so the workbook does not become unreadable.
- Rotate the scoring session participants quarterly to keep judgement fresh.

---

## 12. Risks and limitations

- **Copilot can mis-cluster or mis-tag.** Outputs must be PM-reviewed. Treat Copilot as a fast first draft, never a final answer.
- **Selection bias in feedback.** People who respond to surveys or contact support are not representative of all customers. Silent users are invisible to this workflow.
- **Volume bias.** Frequency is one input, not the whole answer. A pain point affecting 5 strategic enterprise customers may matter more than one affecting 50 trial users.
- **Recency bias.** Recent feedback feels more important. The monthly cadence and longitudinal archive exist to counter this.
- **Translation loss.** Verbatim comments lose nuance when summarised. Always preserve the link from opportunity back to original quotes.
- **Tag drift.** Without a maintained glossary, the same pain point gets tagged five ways and themes fragment.
- **Over-reliance on the score.** The prioritisation formula is a conversation starter. Strategic context, dependencies, sequencing, and timing remain PM judgement calls.
- **Single-PM bottleneck.** If only one person knows how to run the workflow, it dies when they leave or get busy. The README sheet and operating model exist to make handover possible.

---

## 13. Final summary

The Product Feedback Analyser is a lightweight workflow that takes customer feedback from wherever it lives, brings it into one structured Excel workbook, uses Microsoft Copilot to accelerate pattern detection, and produces a prioritised list of product opportunities backed by real customer evidence.

It does three things a product team usually struggles to do consistently: it consolidates feedback into one place, it converts unstructured comments into structured insight, and it forces prioritisation against a clear framework rather than the loudest voice in the room.

The value is not the tooling. Qualtrics, Excel, and Copilot are means to an end. The value is the operating rhythm — a repeatable cycle of collect, synthesise, prioritise, decide — that makes customer feedback a genuine input to the roadmap rather than background noise.
