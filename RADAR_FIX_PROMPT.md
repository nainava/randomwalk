# Radar Data Fix Prompt

You're editing `radar_data.js` for the Random Walk Radar — a "cabinet of curiosities" of weird things happening in science that nobody knows what to do with. Not problems to solve — mysteries to poke at.

## Three fixes needed:

### 1. Rebuild "structural_analogies" (currently 20 entries — cut to ~15, replace the bad ones)

**The problem:** Most of the current structural_analogies entries describe known, published mathematical parallels — not mysteries. "Ant Colony Immune Systems Use the Same Protocol as TCP/IP" and "Ribosome Translation Dynamics Follow Traffic Flow Equations Exactly" are interesting facts, not curiosities. The connection HAS been made. Someone published a paper about it. That's not what this category is for.

**The spec:** This category should contain cases where a principle or mechanism is well-understood in Field A, and an unsolved problem exists in Field B, and the two fields haven't connected yet. The analogy is WAITING to be noticed — it hasn't been. Both halves exist independently. The insight is that they map onto each other but nobody in either field has realized it.

**What to do:** Go through all 20 entries. Keep only the ones where the connection is genuinely unmade or underexploited. Replace the rest with entries where you can identify:
- A well-characterized mechanism/principle in one field
- An unsolved or poorly-solved problem in a different field
- A plausible structural mapping between them that does NOT already have a published paper connecting them

If you can easily Google "[Field A concept] applied to [Field B problem]" and find a Nature paper, it doesn't belong here.

### 2. Cut well-known entries across ALL categories

**The problem:** Several entries would not make a scientifically literate person say "wait, WHAT?" because they've already heard of them. Every entry must clear this bar.

**Cut or replace these specifically:**
- "The Wow! Signal" — famous, discussed for decades
- "Fast Radio Bursts" — widely covered, active mainstream research
- "JWST Galaxies Are Too Mature, Too Early" — headline news for 2 years
- "LK-99 Failed but Ambient-Pressure Hydride Superconductors Are Getting Warmer" — viral internet discourse
- "Muon g-2 Anomaly" — well-covered in popular science
- "LK-99 Failed as a Superconductor but Revealed an Unknown Phase Transition" — second LK-99 entry

**General rule for replacements:** If it was a trending topic on science Twitter or got a Veritasium video, it's too well-known. Replace with something from the same category that's genuinely obscure and surprising.

### 3. Remove the duplicate

"Lithium in Drinking Water Correlates With Lower Suicide Rates" appears in both `weird_substances` and `therapeutic_side_effects`. Keep the one in `weird_substances` (it's the better entry with more detail). Delete the `therapeutic_side_effects` version and replace it with a new entry.

## Quality bar for all new/replacement entries

Every entry must have:
- Real researchers named (not "scientists discovered")
- Real papers cited in `source` field
- A `why_its_weird` that would make someone stop scrolling
- A `who_doesnt_know` that identifies a specific field or profession that would find this startling
- A `follow_up_status` that honestly describes where this stands

Do NOT invent citations. If you can't find a real paper, don't include the entry.
