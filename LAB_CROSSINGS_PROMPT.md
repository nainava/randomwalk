# Lab Crossings Instrument — Build Prompt

## What this is

An instrument that detects cross-domain research configurations in public university labs BEFORE the crossings produce papers or companies. Two parts: a backward-looking validation against the Atlas (proving the instrument would have worked historically) and a forward-looking live surface (detecting crossing conditions in real time from public data).

---

## PART 1: BACKWARD VALIDATION

### Goal

For each of the 11 deep chains in the Atlas, reconstruct what public signals existed BEFORE the breakthrough — and show that the lab crossings instrument would have flagged them. This is the proof of concept. If the instrument retroactively catches 7-8 of 11 historical breakthroughs, it's validated against ground truth.

### What to look for per chain

For each Atlas discovery, identify the moment of crossing — when knowledge from field A entered field B — and then ask: what was publicly visible about the researcher or lab BEFORE that moment?

**Signal types to search for:**

1. **Lab configuration** — Was the researcher's lab or group simultaneously running projects in two distant domains? (e.g., Eng's lab doing both hormone research AND investigating animal venoms)

2. **Researcher bibliography** — Was the researcher citing or reading papers from outside their home field before the breakthrough? (e.g., Deisseroth reading algae biology papers before optogenetics)

3. **Dissertation scope** — Did the key researcher's PhD or postdoc work span fields? (e.g., did anyone involved have training in both the origin and destination fields?)

4. **Grant portfolio** — Was there a grant that funded work crossing two domains? Or was the researcher holding grants in two separate fields simultaneously?

5. **Institutional adjacency** — Were two relevant labs in the same building, department, or institution? (e.g., Doudna and Charpentier's paths crossing through shared conferences and collaborators)

6. **Conference border-crossing** — Did the researcher present at conferences outside their home field before the breakthrough?

### The 11 chains to validate against

For each, provide:
- **The crossing moment**: When did field A knowledge enter field B?
- **What was publicly visible beforehand**: Which of the 6 signal types were present, with specific evidence (lab pages, grant records, publication history, institutional affiliations)
- **Would the instrument have flagged it?**: Yes/no/partial, with explanation
- **How far in advance**: How many months or years before the breakthrough paper would the signal have been detectable?

```
1. GLP-1 / Semaglutide
   Crossing: Venom biology → endocrinology (Eng reading NIH venom papers, late 1980s)
   Look for: Eng's publication history before 1992. Was he citing venom literature? Was the Bronx VA doing any venom-adjacent work? Was there a grant covering both hormone research and comparative biology?

2. Transformer / Modern AI
   Crossing: Attention mechanisms from one neural architecture → machine translation → general-purpose AI
   Look for: The "Attention Is All You Need" authors' prior publication history. Were they citing work from outside NLP? Was Google Brain's project portfolio visible? Were any authors trained in fields other than ML?

3. mRNA Vaccines
   Crossing: mRNA biology → immunology → vaccine platform
   Look for: Karikó and Weissman's collaboration. Were they in the same building at UPenn? What was Karikó's grant history before the pseudouridine discovery? Was Weissman citing mRNA literature before their collaboration?

4. CRISPR
   Crossing: Bacterial genomics (Mojica) → molecular biology (Doudna/Charpentier) → gene editing tool
   Look for: Mojica's publication history in the 1990s. Who was citing his work? Were Doudna or Charpentier's labs working on bacterial immunity before 2012? What grants funded the early CRISPR work?

5. The Internet (ARPANET)
   Crossing: Cold War communications resilience → academic networking → global information system
   Look for: Baran at RAND and Davies at NPL — were their publications visible to each other? Were there shared conferences or citation links?

6. Penicillin
   Crossing: Bacteriology (Fleming) → biochemistry (Florey/Chain) → industrial manufacturing
   Look for: Were Florey and Chain's labs at Oxford configured to work on both biochemistry and microbiology? What was their grant portfolio before picking up Fleming's observation?

7. Viagra
   Crossing: Cardiovascular pharmacology → urology
   Look for: Pfizer's UK-92480 research team. Were any team members publishing in or trained in urology before the side effect was noticed?

8. Lithium for Bipolar
   Crossing: Veterinary/animal research → psychiatry
   Look for: Cade's background. Was he trained in both animal biology and psychiatry? Was his hospital doing any cross-domain work?

9. Microwave Oven
   Crossing: Radar/magnetron manufacturing → food science/consumer appliances
   Look for: Spencer's lab at Raytheon. Were they doing any non-military work? Was there any food science expertise in the building?

10. Teflon
    Crossing: Refrigerant chemistry → materials science → consumer products
    Look for: Plunkett's lab at DuPont. Were they investigating any non-refrigerant properties of fluoropolymers?

11. Post-it Notes
    Crossing: Adhesive chemistry (Silver) → consumer products (Fry)
    Look for: Were Silver and Fry in the same building at 3M? What was 3M's internal structure — did adhesive research and consumer product development share physical space?
```

### Output format

For each chain, produce a brief (200-300 word) case study:

```
## [Discovery Name]

**The crossing:** [One sentence: what knowledge moved from where to where]

**What was publicly visible before the breakthrough:**
- [Signal type]: [Specific evidence]
- [Signal type]: [Specific evidence]

**Would the instrument have flagged it?** [Yes/No/Partial]

**Lead time:** [How far in advance the signal was detectable]

**What the instrument would have shown:**
"[Lab/researcher] at [institution]: projects spanning [field A] and [field B]. [Specific configuration that would appear on the surface.]"
```

After all 11, provide a summary: X of 11 would have been caught. Average lead time. Which signal types were most predictive.

---

## PART 2: FORWARD-LOOKING SURFACE

### Goal

Build a live, queryable surface showing current cross-domain research configurations in public university labs. Each entry represents a structural condition for a crossing — not a completed crossing, but the conditions that precede one.

### Data sources (all public)

**1. NSF Award Search (nsf.gov/awardsearch)**
- All active NSF grants with abstracts
- Search for grants whose abstracts reference concepts from two or more distant NSF directorates (e.g., a grant in BIO that references materials science concepts, or a grant in CISE that references neuroscience)
- Flag grants with co-PIs from different departments
- Flag grants in cross-disciplinary programs (RAISE, EAGER, Growing Convergence Research)

**2. NIH RePORTER (reporter.nih.gov)**
- All active NIH grants with abstracts and PI information
- Search for PIs holding active grants in two different NIH institutes (e.g., NINDS and NIBIB)
- Search for grant abstracts that cite MeSH terms from distant medical subject headings
- Flag R21 (exploratory) and R01 grants whose abstracts span subfields

**3. University lab pages**
- Scrape lab/group pages from top 50 research universities
- Extract: PI name, department, listed research projects, recent publications, current lab members and their backgrounds
- Flag labs listing active projects in two or more distant domains
- Flag labs where current members (postdocs, grad students) have training in a different field from the PI

**4. Dissertation abstracts (ProQuest / institutional repositories)**
- Search for dissertations whose chapter titles or abstracts span two distant fields
- Flag dissertations with committee members from different departments
- Flag dissertations that cite literature from multiple fields in their bibliography

**5. Preprint cross-citations (arXiv, bioRxiv, medRxiv)**
- Scan recent preprints for papers citing work from distant subject categories
- Flag papers where authors' prior publications are in a different field from the current paper
- This overlaps with the existing Finder methodology but feeds into the same surface

### Signal classification

Each detected configuration gets classified by:

**Domain distance:** How far apart are the two fields? Use NSF directorate distance, NIH institute distance, or arXiv category distance as a rough proxy. A neuroscience lab doing computer science is higher distance than a neuroscience lab doing psychology.

**Stage:** How early in the chain is this signal?
- **Configuration** (earliest): Lab has projects in two fields but no output yet
- **In progress**: Dissertation or grant is actively producing cross-domain work
- **Early output**: A preprint or conference paper has appeared but no journal publication
- **Published**: Journal paper exists (this is where the current Finder operates — the latest stage)

**Signal type:**
- Lab portfolio (simultaneous projects in distant fields)
- Researcher migration (person trained in A now working in B)
- Grant bridge (single grant spanning domains)
- Dissertation span (thesis crossing fields)
- Cross-citation (paper citing distant literature)
- Institutional adjacency (two relevant labs sharing space)

**Confidence:** How strong is the evidence that a real crossing is happening vs. superficial keyword overlap?
- High: Multiple signal types present, clear domain distance, active work visible
- Medium: Single signal type, moderate domain distance
- Low: Keyword-level match only, may be superficial

### Output format per entry

```json
{
  "lab_or_researcher": "Name, institution",
  "field_a": "Origin domain",
  "field_b": "Destination domain",
  "domain_distance": "high / medium / low",
  "stage": "configuration / in_progress / early_output / published",
  "signals": [
    {
      "type": "lab_portfolio | researcher_migration | grant_bridge | dissertation_span | cross_citation | institutional_adjacency",
      "evidence": "Specific description of what was found",
      "source": "URL or database reference"
    }
  ],
  "one_liner": "Plain language description of the crossing configuration",
  "why_interesting": "What makes this crossing non-obvious or high-potential",
  "confidence": "high / medium / low",
  "detected": "Date the instrument flagged this"
}
```

### Editorial review layer

Raw signals from scraping will have a high false-positive rate. Before anything appears on the public surface:

1. Automated scraping produces candidate configurations
2. Each candidate is reviewed for: Is the domain distance real or superficial? Is there evidence of active work, not just keyword overlap? Is this a known, well-funded interdisciplinary program (low novelty) or a genuinely unexpected configuration (high novelty)?
3. Reviewed candidates get the one-liner and why_interesting fields written editorially
4. Only reviewed entries appear on the live surface

### The surface itself

A queryable page on the Random Walk site showing current lab crossing configurations:
- Filterable by domain distance, stage, signal type, institution, field
- Each entry expandable to show full evidence and sources
- Updated monthly as new scraping runs complete
- Historical entries remain visible — building a longitudinal record of what was flagged and what eventually happened (closing the loop back to the Atlas)

### What this is NOT

- Not a recommendation engine ("you should fund this")
- Not a prediction ("this will produce a breakthrough")
- Not a ranking of labs or researchers
- Not private or paywalled — the surface is public, built on public data

It's an instrument. It shows you where the structural conditions for crossings exist right now. What you do with that information is up to you. But if you're a funder looking for where to place bets on cross-domain research, this is the only surface that shows you the configurations before they produce papers.

### Network effect (later)

Phase 1 is public data only. Phase 2: once the surface is trusted and used by funders, private labs and companies opt in — sharing their own crossing configurations into the system in exchange for visibility to funders. This creates a self-reinforcing loop: more data → better surface → more funders → more labs sharing → more data. But this only works if Phase 1 proves the instrument is useful on public data alone.

---

## HOW THE PIECES FIT TOGETHER

```
Lab Crossings Surface (this instrument)
  ↓ detects configurations
Finder (existing)
  ↓ tracks active crossings that have produced early output
Radar (existing)
  ↓ curates raw anomalies and weird properties
Atlas (existing)
  ↓ validates everything retroactively with 51 forensic chains

Fellowship → funds people identified by the surface
```

The Atlas is the proof. The surface is the product. The Fellowship is the deployment mechanism.
