# ADR-017: Condition-first retrieval

- Date: 2026-11-07
- Status: proposed
- Context: The 30 expert questions follow the shape 'Am I right to prescribe X for Y with Z?', and some contain a wrong premise. Drugs appear widely (amoxicillin in about 41 sections, metronidazole about 37, gentamicin about 33), and a wrong drug may not appear in the right condition at all. The book is organised by syndrome (chancroid sits inside Genital Ulcer Disease).
- Options considered: (a) search by drug name; (b) resolve the condition first, load its management, then compare the drug.
- Decision: (b). Steps: extract the condition, drug, patient group and regimen from the question; resolve the diagnosis to a condition_id using the condition list, ICD-10 and an alias list; load the whole Management plus blocks that apply to it; compare and give a verdict; run the scope check.
- Why: Drug-first search is noisy, and a whole condition's management is small enough to load.
- Consequences: The whole-condition route is the core of the system, not a later add-on. Patient group (age, pregnancy) matters and is used as a soft ranking, not a hard filter. Details are to be designed in Stage 3.
