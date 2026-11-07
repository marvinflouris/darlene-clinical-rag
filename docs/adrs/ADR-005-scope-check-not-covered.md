# ADR-005: Answers stay within what the UCG covers; "not covered" is a valid answer

- Date: 2026-11-07
- Status: accepted
- Context: The 50 baseline questions include ICD-10 coding, prices, stock and kidney values. The UCG has only coarse ICD codes (diabetes is the range E08-E13), few renal-dosing mentions, and no prices.
- Options considered: (a) always answer from the closest match; (b) a scope check that can return 'not covered'.
- Decision: (b).
- Why: A wrong or invented answer is the biggest danger in a clinical tool.
- Consequences: The system needs a scope check. Patient facts such as allergies and kidney function are inputs to the query and are not retrieved. Price and stock are out of scope. Placeholder chunks with no data say 'not loaded yet'. The 50 baseline questions double as tests for this.
