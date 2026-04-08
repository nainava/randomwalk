# Random Walk Radar v2 — Cabinet of Curiosities

## The Problem with v1

The v1 radar was a grant database: "here are 100 gaps someone should fund." That's top-down allocation — identifying a problem and directing resources at it. It contradicts the entire thesis of the project.

The actual insight from the random walk dataset is that you *can't* predict where breakthroughs come from. Eng wasn't studying obesity. He was poking at lizard venom because it was interesting. The breakthrough came from the poking, not from anyone identifying a "funding gap in GLP-1 receptor agonists."

## What the Radar Should Be

Not "here are 100 problems that need funding." Instead: **"here are 100 things that are weird and interesting and nobody knows what they're for yet."**

The difference: one is top-down (we identified the gap, now fill it). The other is bottom-up (something strange is happening here, someone should poke at it).

## What Belongs on the Radar

1. **Unexpected experimental results that don't fit existing models.** A material that behaves in a way it shouldn't. A biological mechanism that doesn't make sense. An observation published once and never followed up because it didn't fit a fundable narrative.

2. **Properties without applications.** Not "this could be used for X" but "this does something weird and we don't know why." Exendin-4 was a property without an application for years — a peptide that happened to not degrade.

3. **Researchers doing unfashionable work that keeps producing surprising results.** Not "this field needs more funding" but "this person keeps finding things that don't make sense and the establishment ignores them." Karikó was this person for decades.

4. **Cross-field observations that nobody has claimed.** Things sitting in papers that are interesting to people in field A but invisible to field B — not because someone identified the connection, but because the connection hasn't been made yet and might lead anywhere.

5. **Failed experiments with unexplained residuals.** Experiments that "didn't work" but produced something unexpected that got filed away. The "failed" adhesive → Post-it Notes. The "failed" blood pressure drug → Viagra.

## The Prompt

```
Scan recent scientific literature for the weird, the unexplained, and the ignored. I want 100 entries for a "cabinet of curiosities" — not problems to solve, but mysteries to poke at.

For each entry, provide:

{
  "title": "Short, evocative name — not a research proposal title, more like a curiosity label",
  "type": "anomaly / property_without_use / unfashionable_researcher / cross_field_invisible / unexplained_residual",
  "what_happened": "2-3 sentences describing the weird thing. What was observed? Why is it strange? Write it so someone outside the field would say 'wait, what?'",
  "why_its_weird": "1-2 sentences on why this doesn't fit existing models or expectations. What should have happened instead?",
  "where_it_sits": "Which paper, lab, or dataset contains this observation? Be specific — journal, year, author.",
  "who_noticed": "The person or team who observed it. Are they still working on it? Did they move on?",
  "who_doesnt_know": "Which adjacent field would find this startling if they knew about it? Why haven't they seen it?",
  "follow_up_status": "Was this followed up? By how many groups? Is it sitting in a single paper gathering dust?",
  "poke_factor": 1-10 (how much does this make you want to go poke at it?),
  "field": "broad field tag",
  "year": "when was this first observed"
}

SELECTION RULES:

- NOT identified gaps or problems. No "this field needs more funding." No "these two fields should collaborate." That's grant-writing, not curiosity-tracking.
- YES to things that surprised the people who found them. Look for language like "unexpectedly," "contrary to predictions," "anomalous," "we don't understand why," "remains unexplained."
- YES to properties that exist without anyone knowing what they're for. Substances, organisms, or phenomena with characteristics that seem useful but have no identified use.
- YES to single-paper observations that were never replicated or followed up — not because they were wrong, but because they didn't fit anyone's funding narrative.
- YES to researchers producing a pattern of surprising results that the mainstream ignores.
- YES to observations in one field that would blow minds in another field if anyone made the connection.
- YES to "failed" experiments where the failure itself was interesting.

DIVERSITY: Spread across physics, biology, chemistry, materials, computing, earth science, social science, archaeology, ecology. Mix eras (some recent, some decades-old observations gathering dust). Mix scales (molecular to planetary).

TONE: Each entry should make the reader think "huh, that's weird" — not "that's important." Importance is what the random walk discovers later. Right now, it's just weird.

Use real papers, real researchers, real observations. If you're uncertain about a detail, flag it. Do not invent observations.
```

## After the Data is Built

Build an interactive HTML page — same dark, data-forward aesthetic as the main site. But the UI metaphor is different: not a dashboard with scores and filters, but a scrollable cabinet. Cards you can flip. Weird things you stumble across. The experience should feel like browsing a curiosity shop, not reading a report.

Each card shows the title and "what happened" on the front. Click/tap to reveal the full entry — why it's weird, where it sits, who doesn't know about it, follow-up status.

Sort by poke_factor by default but allow shuffle (random order) — because the whole point is that you don't know which ones matter.
