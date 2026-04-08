# Random Walk Research — Build Prompt (Final)

## What This Is

An interactive website mapping cases where investment in X led to a discovery in Y. Each entry traces the full attribution chain — every jump, with real names, real institutions, real funding sources, and real dates. The tool is the argument. ~500 words of framing text. That's it.

## The Output Format

Each entry powers a working research tracker. The top-level fields populate a summary table (invention, inventor, date, use, funding source, funding reason). The chain field contains the full X→Y narrative with every step traced. Populate BOTH — the summary fields AND the deep chain.

Here's the schema:

```json
{
  "number": "001",
  "discovery_name": "GLP-1 Weight Loss Drugs",

  "tracker_summary": {
    "invention": "GLP-1 receptor agonists (Ozempic/Wegovy/Byetta)",
    "inventor": "Dr. John Eng (origin); Novo Nordisk (semaglutide)",
    "date": "1992 (exendin-4 isolation)",
    "current_use": "Obesity, type 2 diabetes, cardiovascular risk; studied for Alzheimer's, addiction",
    "initial_funding_source": "VA Medical Center research budget (Bronx, NY)",
    "initial_funding_reason": "General hormone research; investigating lizard venom effects on pancreatic function",
    "chain_length": "9 steps · 35+ years"
  },

  "the_x": "VA-funded hormone research at a Bronx medical center, investigating lizard venom's effects on the pancreas",
  "the_y": "A class of drugs reshaping global treatment of obesity, diabetes, cardiovascular disease, and potentially Alzheimer's and addiction",

  "summary": "A VA endocrinologist ordered dried lizard venom from a Utah serpentarium catalog. Thirty years later, 9% of the U.S. population is projected to be on GLP-1 drugs by the end of the decade.",

  "chain": [
    {
      "year": "EARLY 1980s",
      "who": "NIH gastroenterologists",
      "where": "National Institutes of Health",
      "what_they_were_doing": "Researchers studying venom from certain snakes and lizards notice it causes inflammation of the pancreas. Basic venom biology — nobody is thinking about diabetes drugs.",
      "the_jump": null,
      "funding": "NIH intramural research program",
      "critical": false
    },
    {
      "year": "LATE 1980s",
      "who": "Dr. John Eng",
      "where": "Bronx VA Medical Center, New York",
      "what_they_were_doing": "Endocrinologist working under Nobel laureate Rosalyn Yalow. Reads the NIH venom studies and gets curious about the Gila monster — a lizard that goes months without eating while maintaining stable blood sugar. Orders dried venom from a Utah serpentarium catalog.",
      "the_jump": "A clinician reading a basic science paper from a completely different field. Eng connected 'lizard venom affects the pancreas' with 'my diabetic patients need better insulin regulation.'",
      "funding": "VA research funds for general hormone research",
      "critical": false
    },
    {
      "year": "1992",
      "who": "Dr. John Eng, Dr. Jean-Pierre Raufman",
      "where": "Bronx VA Medical Center / SUNY Brooklyn",
      "what_they_were_doing": "Eng isolates a new peptide he names exendin-4. Raufman drives from Brooklyn to the Bronx with test tubes in his Toyota Camry. They discover exendin-4 is 53% similar to human GLP-1 but with a crucial difference: human GLP-1 degrades in ~2 minutes, exendin-4 lasts for hours.",
      "the_jump": "The critical discovery: a lizard peptide that mimics a human hormone but is vastly more durable. Published in the Journal of Biological Chemistry.",
      "funding": "VA Medical Center research budget",
      "critical": true
    }
  ],

  "sources": [
    "Eng J, et al. 'Isolation and characterization of exendin-4.' Journal of Biological Chemistry, 1992;267(11):7402-7405.",
    "VA Research: 'Diabetes drug from Gila monster venom' (2019)",
    "NIA: 'Exendin-4: From lizard to laboratory...and beyond' (2012)"
  ]
}
```

## The Prompt

```
I'm building a research dataset tracing the full attribution chains of major discoveries where investment in X led to a discovery in Y.

SELECTION RULE: Only include discoveries where the gap between funded intent and actual impact is real and documentable. Every entry should make someone say "wait, THAT'S where that came from?"

For each entry, use the JSON schema above. The most important fields are:

1. "the_x" and "the_y" — the funded intent vs. actual impact, stated clearly
2. "chain" — the full sequence of steps with REAL PEOPLE, REAL INSTITUTIONS, REAL FUNDING SOURCES, and REAL DATES
3. "the_jump" — at each step where the random walk changes direction, explain the specific moment or connection. This is the narrative core. Be specific and human.
4. "critical" — mark the step(s) where the most important jump happened
5. "sources" — cite actual papers, patents, articles, or institutional records

TRACE DEEP. "Ozempic started as a diabetes drug" is shallow. The full chain from NIH venom studies → John Eng at the Bronx VA → Gila monster venom from a Utah catalog → exendin-4 → VA refuses to patent → poster at ADA conference → Amylin Pharmaceuticals → FDA approval → weight loss side effect → $100B market → Alzheimer's research is deep. That depth is what makes this project different from every "accidental discoveries" listicle.

Include moments where the discovery ALMOST DIED — bureaucratic rejections, funding cuts, patent refusals, years of obscurity. These near-death moments are part of the random walk.

---

BUILD FULL CHAINS FOR:

1. THE TRANSFORMER / MODERN AI
   Trace from the actual research lineage. Not just "Google Brain published a paper." What were the precursor ideas? Who was working on attention mechanisms? What was the stated goal of the "Attention Is All You Need" project? How did a machine translation paper become the foundation of the entire AI revolution?

2. mRNA VACCINES
   Trace from Katalin Karikó's earliest mRNA work. Her specific rejected grants. The pseudouridine discovery with Drew Weissman. The years of institutional rejection. How BioNTech and Moderna licensed the technology. The COVID-19 moment.

3. THE INTERNET
   Trace from ARPA's specific Cold War concerns → packet switching (Paul Baran at RAND, Donald Davies at NPL — independently) → ARPANET → TCP/IP (Cerf, Kahn) → Berners-Lee's document management problem at CERN → the World Wide Web. Multiple random walks stacked.

4. CRISPR GENE EDITING
   Trace from Yoshizumi Ishino finding weird repeated sequences in E. coli (1987) → Francisco Mojica studying archaea in Spanish salt marshes → the bacterial immune system hypothesis → Doudna and Charpentier's 2012 paper → gene editing tool.

5. PENICILLIN
   Not just "Fleming noticed mold." Trace the FULL chain including the decade+ gap where nobody cared, Florey and Chain at Oxford picking it up, the wartime urgency, US pharmaceutical mass production.

6. VIAGRA
   Trace from Pfizer's specific angina/blood pressure research program → UK-92480 compound → failed cardiovascular trials → the clinical observation of the side effect → pivot to erectile dysfunction.

7. LITHIUM FOR BIPOLAR DISORDER
   John Cade injecting guinea pigs with urine from manic patients (1948) → using lithium urate as a control → noticing the calming effect → one of psychiatry's most important drugs.

8. MICROWAVE OVEN
   Raytheon's magnetron production for WWII radar → Percy Spencer's melted chocolate bar → Radarange → household microwaves.

9. TEFLON (PTFE)
   DuPont refrigerant gas research → Plunkett's failed experiment → nonstick coatings → aerospace applications.

10. POST-IT NOTES
    Spencer Silver's failed strong adhesive at 3M → years of no use case → Art Fry's church hymnal bookmark problem → Post-it Notes.

AFTER THESE 10, suggest 40 more with brief chain outlines (2-3 sentences each indicating the X, the Y, and the key jump). Prioritize:
- Chain depth (more jumps = more interesting)
- Field diversity (not all biomedical)
- Era diversity (especially post-2000)
- Jump type diversity (not all "noticed a side effect")
- Surprising origins (the weirder the better)
```

## After the Data is Built

Run the analysis prompt from v3 to extract patterns. Then write the ~500 word framing text. Then populate the HTML template with all entries.

The HTML prototype (random_walks.html) is already built with the GLP-1 entry as the first data point. Each new entry follows the same structure. The chain steps expand on click. Critical steps are highlighted. Sources are collapsible.
