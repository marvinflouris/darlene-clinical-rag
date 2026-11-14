# ADR-027: Report unrecognised patterns instead of deciding silently

- Date: 2026-11-14
- Status: accepted. Adds to ADR-025 (no new steps are added).
- Context: Config facts were first proposed from a few pages and then contradicted by whole-book counts. About 40% of section labels use a second font, and "Treatment" appears both as a table header and as a standalone label. If a script does not recognise a style, it could attach that text to the wrong part. The coverage check in step 10 would still pass, because no text is lost, so the chunks would be wrong and nothing would show it. The first plan had no check for this.
- Options considered: (a) keep the first plan and rely on a manual checklist; (b) add a separate whole-book profile file and a page-range option; (c) add small "unrecognised pattern" reports inside the steps that already exist.
- Decision: (c). Step 3 lists numbered bold lines whose style is not configured as a heading, as possible missed headings. Step 5 lists known label words in a font that is not configured, and short bold lines it does not recognise, in data/reports/label_review.csv. Step 10 adds a shape check: conditions with no recognised labels, and unusually long chunks. The config holds only checked facts, and each value says how it was checked.
- Why: It catches the one failure the coverage check cannot see (text that is kept but placed in the wrong part), without adding a step or a new file type.
- Consequences: A few lines of reporting code are added to steps 3, 5 and 10. The reports must be read after each step. Anything they list is fixed in config/ and the step is re-run. ADR-025 still holds.
