# Random Walk Scouting Framework — Build Prompt

## What This Is

A systematic methodology for detecting random walks in progress — people working intensely in one field who are encountering or applying something from another field, right now, in real time. This is the missing piece between the retrospective atlas (proving the pattern exists) and the fellowship (funding people mid-walk).

The framework has four channels. Each one catches a different type of signal. Together they produce a pipeline of "Random Walks in Progress" candidates for the spotlight and eventually the fellowship.

---

## Channel 1: Cross-Citation Scraper

### Concept

When a paper in field A cites a paper from unrelated field B, that's a bibliometric fingerprint of cross-pollination happening right now. A neuroscience paper citing a materials science paper. A computer science paper citing evolutionary biology. An agriculture paper citing quantum mechanics. These cross-field citations are the textual trace of someone carrying an idea from one domain into another — the exact mechanism that produced optogenetics (algae biology → neuroscience), AlphaFold (game AI → structural biology), and cisplatin (electrochemistry → oncology).

### Prompt

```
I want to build a pipeline that identifies unusual cross-field citations in recent scientific papers. The goal is to find papers where the author is citing work from a field that is surprising relative to their own field — a signal that cross-pollination is happening.

Help me design this system:

DATA SOURCES:
- arXiv API (preprints across physics, math, CS, biology, economics, etc.)
- Semantic Scholar API (broader coverage, citation graph access)
- OpenAlex API (open bibliometric data, field classifications, citation links)
- PubMed API (biomedical literature)

THE SIGNAL I'M LOOKING FOR:
A paper published in the last 6 months whose reference list includes citations from a field that is categorically distant from the paper's own classification. Not just "a biology paper citing another biology paper in a different subfield" — that's normal. I want "a biology paper citing a condensed matter physics paper" or "a computer science paper citing an archaeology paper."

METHODOLOGY:
1. For each recent paper, extract its field classification (using the journal, arXiv category, or OpenAlex concept tags)
2. For each reference in that paper, extract the field classification of the cited work
3. Compute a "citation distance" — how far apart are the citing and cited fields?
4. Flag papers where citation distance exceeds a threshold

FIELD DISTANCE MEASUREMENT:
I need a way to quantify how "far apart" two fields are. Options:
- Use a hierarchical field taxonomy (like OpenAlex's concept tree) and measure tree distance
- Use co-citation frequency: if fields A and B are rarely cited together across the entire corpus, a paper citing both is unusual
- Use embedding distance: embed field labels and measure cosine similarity

Which approach is most practical given the available APIs? Can we combine them?

OUTPUT:
For each flagged paper, produce:
{
  "paper_title": "",
  "authors": "",
  "paper_field": "",
  "unexpected_citation": {
    "cited_paper_title": "",
    "cited_paper_field": "",
    "citation_distance_score": 0-10
  },
  "date": "",
  "abstract_excerpt": "The relevant sentence or passage explaining WHY they cited this distant work",
  "link": ""
}

Sorted by citation distance score. The highest-scoring papers are the ones where the cross-pollination is most unexpected.

FILTERS:
- Exclude review papers and meta-analyses (they cite broadly by nature)
- Exclude papers with >100 references (these are surveys, not focused research)
- Prioritize papers with <30 references where one or two citations are dramatically out of field — that's a researcher who went looking for something specific from another domain
- Prioritize first-author papers from early-career researchers (they're more likely to be doing the actual cross-domain work themselves rather than delegating)

PRACTICAL QUESTIONS:
- What's the realistic volume? If I scan 10,000 recent papers, how many will have genuinely surprising cross-citations?
- How do I avoid false positives from multidisciplinary journals (Nature, Science, PNAS) where cross-field citation is expected?
- Can I run this weekly as an automated pipeline?
- What's the cheapest way to prototype this — which API gives me the most useful data with the least friction?

Give me the architecture, the API calls, and a working Python prototype I can run.
```

---

## Channel 2: Conference Border-Crossers

### Concept

Eng presented his Gila monster venom work at the American Diabetes Association conference — he was a VA hormone researcher presenting at a diabetes conference. That mismatch between presenter background and conference field is a signal. When someone's home field doesn't match the conference they're presenting at, they're carrying knowledge across a boundary.

### Prompt

```
I want to build a system that identifies "conference border-crossers" — researchers who present at conferences outside their primary field.

THE SIGNAL:
A person whose publication history, institutional affiliation, or degree is in field A, presenting a poster or talk at a conference in field B. This person is mid-random-walk — they've found something in their home field that they think is relevant to another field, and they're trying to get it in front of people who wouldn't normally see it.

DATA SOURCES:
- Conference program books and abstract collections (many are publicly available as PDFs or web pages)
- Author institutional affiliations from the conference program
- Cross-referencing presenter names against their publication history (via Semantic Scholar or Google Scholar)

METHODOLOGY:
1. Scrape or manually collect presenter lists and abstracts from major conferences across multiple fields
2. For each presenter, look up their publication history to determine their "home field"
3. Flag presenters whose home field doesn't match the conference field
4. Extract their abstract to understand what cross-domain connection they're making

WHICH CONFERENCES TO START WITH:
I want to cover a breadth of fields. Suggest 20-30 major annual conferences across:
- Biomedical / pharma
- Materials science / chemistry
- Computer science / AI
- Physics / astronomy
- Neuroscience
- Engineering
- Earth science / ecology
- Social science / economics

For each, tell me:
- Whether their program/abstracts are publicly available
- When the next conference is
- How to access the presenter list

THE PRACTICAL CHALLENGE:
Conference programs are not standardized. Some are PDFs, some are web apps, some are behind registration walls. I need a realistic assessment of which conferences have scrapeable programs and which don't. For the ones that don't, what's the manual approach?

OUTPUT:
For each flagged border-crosser:
{
  "presenter_name": "",
  "home_field": "",
  "conference_name": "",
  "conference_field": "",
  "presentation_title": "",
  "abstract_excerpt": "",
  "what_theyre_carrying_across": "Brief description of the cross-domain connection",
  "their_publication_history_link": ""
}

This is inherently lower-volume than the citation scraper — maybe 5-20 border-crossers per major conference. But the signal quality is very high because these people have already self-selected as cross-pollinators.
```

---

## Channel 3: Failed Experiment Residuals

### Concept

Post-it Notes came from a failed adhesive. Viagra came from a failed blood pressure drug. Teflon came from a failed refrigerant synthesis. "Failure" is defined relative to the original goal — but the residual of failure has properties that are real. There are databases that systematically document failures: clinical trial results databases, retraction databases, negative results journals. These are graveyards of X→Y potential.

### Prompt

```
I want to build a pipeline that scans databases of "failed" research for anomalous residuals — unexpected observations or side effects noted in studies that didn't achieve their primary endpoint.

DATA SOURCES:

1. ClinicalTrials.gov results database
- Completed trials with status "terminated" or "completed" where primary endpoint was not met
- Specifically looking at the "adverse events" and "secondary outcomes" sections for unexpected positive effects
- Example of what I'm looking for: a trial for drug X targeting condition A that failed, but where patients reported improvement in unrelated condition B

2. Retraction Watch database
- Papers retracted for reasons other than fraud (methodology issues, irreproducibility)
- Some retracted papers contain observations that are real but were presented in a flawed framework
- The observation may be valid even if the conclusion was wrong

3. Journal of Negative Results in Biomedicine (and similar negative results journals)
- Published negative results often contain "however, we did observe..." asides that document unexpected findings the authors chose not to pursue

4. Patent databases (abandoned patents)
- Patents that were filed but not maintained may contain documented properties of materials or compounds that the filer decided were commercially uninteresting — but the properties are real

METHODOLOGY:
For ClinicalTrials.gov specifically:
1. Query for completed/terminated trials in the last 5 years where primary outcome = not met
2. Extract the "adverse events" and "other outcomes" sections
3. Use NLP/LLM to scan for language indicating unexpected positive effects: "unexpectedly improved," "incidental finding," "secondary analysis revealed," "post-hoc observation"
4. Flag trials where an adverse event or secondary outcome suggests a therapeutic effect in a different system than the one being targeted

OUTPUT:
{
  "trial_id": "",
  "original_target": "What the trial was trying to treat",
  "what_failed": "Why the primary endpoint wasn't met",
  "the_residual": "The unexpected observation or side effect",
  "potential_field": "What field might find this residual interesting",
  "date": "",
  "link": ""
}

This is systematizing how Viagra, minoxidil, and chlorpromazine were discovered — but instead of waiting 20 years for a clinician to notice, we scan for the signals systematically.

VOLUME ESTIMATE:
How many terminated/failed trials are there per year on ClinicalTrials.gov? Of those, what percentage have documented secondary observations worth flagging? I need to know if this produces 10 leads per month or 1,000.
```

---

## Channel 4: Open Nominations

### Concept

The human intelligence layer. People who read the atlas and recognize the pattern in their own work or someone they know. This catches things the scrapers miss — informal cross-pollination, garage projects, independent researchers, early-stage startup founders applying techniques from their PhD to a completely different problem.

### Prompt

```
Design a simple open nominations form for the Random Walk Research website. The form should capture enough information to evaluate whether someone is mid-random-walk without being so long that people don't fill it out.

THE FORM:

Field 1: "Who is working at an unexpected intersection?"
- Can be self-nomination or nominating someone else
- Name and contact (or link to their work)

Field 2: "What are the two fields colliding?"
- Field A (their background / training / primary expertise)
- Field B (the new domain they're applying it to)

Field 3: "What's the connection they've found?"
- 2-3 sentences. What insight or technique from field A are they bringing to field B?

Field 4: "How deep are they?"
- Are they casually interested or intensely committed?
- How long have they been working on this?
- Have they published, presented, or built anything at the intersection?

Field 5 (optional): "Why does this matter?"
- What could it lead to? (Acknowledging that the whole thesis is you can't predict this — but people often have intuitions worth capturing)

DESIGN NOTES:
- The form should be short enough to fill out in 3 minutes
- It should feel like recommending a person, not filling out a grant application
- The framing should reference the atlas: "The discoveries in our atlas all started with someone working at an unexpected intersection. Know someone doing that right now?"
- No login required, no account creation
- Submissions feed into a simple review pipeline (Airtable, Notion, or similar)

OUTPUT:
Design the form fields, the framing copy, and the backend pipeline for reviewing submissions. How do I triage 50 nominations per month into the 3-5 best candidates for the spotlight?
```

---

## Combining the Channels into the Spotlight

### Prompt

```
I have four channels feeding candidates into a pipeline:

1. Cross-citation scraper (automated, high volume, variable quality)
2. Conference border-crossers (semi-automated, lower volume, high signal)
3. Failed experiment residuals (automated, medium volume, requires interpretation)
4. Open nominations (human-submitted, variable volume, variable quality)

Design the editorial pipeline that takes these raw signals and produces "Random Walk Spotlight" entries — current cross-domain work written up with the same depth and care as the historical atlas.

PIPELINE STAGES:

Stage 1: Triage
- Automated scoring based on cross-field distance, researcher intensity indicators (publication depth in home field), and novelty
- Reduce raw pipeline to ~20-30 candidates per month

Stage 2: Verification
- Is the cross-pollination real? Is this person actually applying field A knowledge to field B, or is it superficial?
- Does their work show intensity (deep publication record, years of commitment) or is it casual?
- Has anyone else noticed this intersection?

Stage 3: Outreach
- Contact the researcher/builder. Verify the story. Ask what they're working on and why.
- This is where the human relationship starts — the same way Eng's story started with Andrew Young reading his poster

Stage 4: Spotlight
- Write up the random walk in progress: who they are, what their home field is, what they've encountered from another field, what's happening at the intersection, and why it's interesting
- Same editorial quality as the atlas entries
- Published on the site as a "Random Walk in Progress" with the researcher's knowledge and input

Stage 5: Fellowship consideration
- The best spotlight candidates become fellowship candidates
- Small grants ($5-15k) to keep them going at the intersection
- Transparent tracking of what happens

How do I run this pipeline as one person? What can be automated and what requires editorial judgment? What's the realistic monthly output — how many spotlights per month can one person produce at atlas quality?
```

---

## What This Becomes

When you present the full system to a funder, you're showing:

1. **The Atlas** — proof that random walks produce breakthroughs (backward-looking)
2. **The Framework** — a systematic methodology for detecting them in real time (the scouting system)
3. **The Spotlight** — current random walks written up with forensic depth (the editorial product)
4. **The Fellowship** — funding for people mid-walk (the deployment)

That's not a website. That's an institution with a methodology, a product, and a deployment mechanism. It's what Analogue claims to be but isn't — because they scout through personal networks and salon vibes, and you scout through systematic cross-citation analysis, conference mining, failure database scanning, and open nominations.

The proof of work replaces the network. The framework replaces the vibes.
