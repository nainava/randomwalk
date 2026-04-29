# Lab Portfolio Crossings — Detection Prompt

## What to find

University labs where a single PI's group page lists active projects in two or more domains with high domain distance. Not "two people who met" — one lab, two worlds, same whiteboard. The students and postdocs in these labs are immersed in both domains simultaneously just by being in the room. This is the earliest, most structural signal for a random walk.

## Why this matters

The Still Bright pattern: a PhD student working in a lab that runs both copper purification and vanadium flow battery research combined the two into a company. The student didn't need to be co-advised across departments. The lab itself had both projects. The crossing happened because one person was exposed to both domains in the same physical and intellectual space.

This is the signal most likely to precede a breakthrough by years — and the most scrapable, because lab pages are public.

## What to search for

Go to the lab/group pages of research universities. Look for labs where the listed research projects, publications, or current student work spans two fields that would not normally appear together. The domain distance is the key filter — two subfields of biology is not interesting. Acoustics and pharmaceutical manufacturing is interesting. Fungal biology and computing is interesting. Seismology and cardiology is interesting.

These entries go into **radar.html** (Random Walk: Radar) as new entries at the **Configuration** stage, tagged with **Lab portfolio scan** as the detection method. Format each to match the existing radar.html entry structure.

For each lab found, produce:

```json
{
  "lab_name": "Name of the research group",
  "pi": "PI name",
  "institution": "University",
  "field_a": "First domain (from their listed projects)",
  "field_b": "Second domain (from their listed projects)",
  "domain_distance": "high / very high",
  "evidence": {
    "project_a": "What the lab is doing in field A (from their website)",
    "project_b": "What the lab is doing in field B (from their website)",
    "shared_infrastructure": "What tools, methods, or resources the two projects share in the lab (if any)",
    "student_exposure": "Are students/postdocs working on both, or are they siloed within the lab?"
  },
  "one_liner": "Plain language: what crossing could emerge from this configuration",
  "why_nobody_sees_it": "Why people in field A and field B wouldn't know about this lab",
  "source_url": "Link to the lab page"
}
```

## What makes a strong entry

- **High domain distance is mandatory.** A chemistry lab doing organic AND inorganic chemistry is not a crossing. A chemistry lab doing organic chemistry AND building robots is a crossing.
- **Both projects must be active.** Not "the PI published in this field 10 years ago." Current, listed, active projects.
- **The crossing should be non-obvious.** If it's an explicitly interdisciplinary program that everyone knows about (e.g., a well-funded "convergence" center), it's less interesting. The most valuable finds are labs where the PI probably doesn't even think of themselves as interdisciplinary — they just happen to have two projects in distant domains because their curiosity led them there.
- **Bonus: student/postdoc overlap.** If the same grad student or postdoc is contributing to both projects, the crossing conditions are strongest. That person IS the random walk.

## Where to look

- Lab pages at top research universities (MIT, Stanford, Berkeley, Caltech, Harvard, Princeton, Georgia Tech, UIUC, Northwestern, UChicago, Columbia, UCSD, UW, etc.)
- Look across departments that don't usually overlap: materials science + biology, physics + medicine, computer science + ecology, geology + energy, acoustics + anything medical, mathematics + anything applied
- NSF and NIH funded labs are more likely to have detailed project descriptions on their pages
- Don't limit to US — ETH, Cambridge, Oxford, Max Planck institutes, Tokyo, etc. are all valid

## What NOT to include

- Labs that are explicitly branded as "interdisciplinary" or "convergence" programs — these are known and funded
- Labs where the two domains are subfields of the same discipline
- Labs where the PI published in field B once, ten years ago, but the current group only works in field A
- Theoretical analogies ("these two fields use similar math") without a lab actively working on both
