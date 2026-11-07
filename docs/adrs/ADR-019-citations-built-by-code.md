# ADR-019: Citations are built by code from metadata

- Date: 2026-11-07
- Status: proposed
- Context: A model can invent a page number or a section name.
- Options considered: (a) let the model write citations; (b) the model returns only chunk IDs and code builds the citations.
- Decision: (b). A citation shows the section number and title, the section type, the printed and PDF page, and the stored line as the excerpt (not the model's paraphrase). Prepared tables also show their verification status. If two sources disagree, both citations appear. Every claim needs a citation.
- Why: The citation text cannot be invented, because it comes from stored metadata.
- Consequences: Needs printed_page, pdf_page, section_path and table_verification_status in every chunk. Format to be finalised in Stage 3.
