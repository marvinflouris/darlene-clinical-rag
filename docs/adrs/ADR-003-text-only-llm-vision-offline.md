# ADR-003: The main LLM is text-only; vision models are used only offline

- Date: 2026-11-07
- Status: accepted
- Context: Hard tables (ARV, TB, flowcharts) carry meaning visually. For example, dark grey cells mean 'not applicable'.
- Options considered: (a) a vision-capable LLM reading page images at question time; (b) a text-only LLM, with vision models used offline to prepare the tables.
- Decision: (b).
- Why: The project owner chose reasoning quality and judgement over multimodality. Prepared tables can be checked by experts before they are used.
- Consequences: Prepared tables must write out what the picture shows ('not applicable', 'no dose'). Vision output is a draft that experts verify. Prepared tables live in curated/ and are tracked in git.
