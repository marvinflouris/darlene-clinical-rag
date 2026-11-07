# ADR-007: Parent-child chunks: drug lines and table rows are small chunks, the whole table is the parent

- Date: 2026-11-07
- Status: accepted
- Context: A Management table holds many drugs. As one chunk, a question about one drug matches weakly. Cut by size, a dose can be separated from its child doses.
- Options considered: (a) the whole table as one chunk; (b) fixed-size cuts; (c) one small chunk per drug line or row, with the whole table as parent.
- Decision: (c). Small chunks are searched. The parent is fetched by parent_chunk_id and given to the LLM together with the matched line.
- Why: Precise matching on the line, with the full table (sub-headings, '-Or' alternatives, notes) for context.
- Consequences: parent_chunk_id is set when the pieces are made (steps 5 to 8). Step 9 checks that every parent exists. Plain prose parts normally have no parent. This is the small-to-big pattern.
