# Data Cleaning & validation Case Study

Audited and cleaned a raw employee records dataset (420 rows) containing realistic
data-entry errors, then measured the impact of the cleaning process in concrete,
before-and-after terms. Every value was cleaned and validated using live spreadsheet
formulas — nothing was manually overwritten — so the process is fully repeatable if
new raw data arrives.

## Issues found in the raw data
- Inconsistent text formatting (mixed case, stray spacing) in names and category fields
- Inconsistent category labels — Department, Gender, and Status each had 4–7 different
  raw spellings for the same value (e.g. "HR", "hr", "H.R.", "Human Resources")
- Missing and impossible values (blank or out-of-range ages, negative salaries)
- Mixed currency formatting (plain numbers, comma-formatted, Naira-symbol-prefixed)
- Ambiguous date formats — day-first (DD/MM/YYYY) entries caused genuine parsing
  failures, a common real-world data-entry risk
- Invalid email addresses (doubled symbols, missing domains, embedded spaces)
- Duplicate employee records, some re-entered with different text formatting

## Methodology
- **Text fields**: standardized with TRIM + PROPER
- **Category fields**: every raw variant mapped to one standardized value using
  lookup tables and INDEX/MATCH
- **Age & Salary**: validated against realistic ranges; flagged for review rather
  than auto-corrected, since guessing real values isn't safe
- **Hire date**: parsed with DATEVALUE; unparseable dates flagged
- **Email**: validated structurally and flagged if malformed
- **Duplicates**: flagged with COUNTIF rather than silently removed, so a reviewer
  can decide which record to keep

## Key decision: flag, don't guess
Ambiguous or impossible values were never auto-corrected. Every questionable record
is flagged "NEEDS REVIEW" with the specific reason, so a human makes the final call —
this mirrors how real data quality roles work.

## Results

| Metric | Before | After |
|---|---|---|
| Total records | 420 | 420 |
| Ready to use | unknown | 233 (55.5%) |
| Flagged for review | unknown | 187 (44.5%) |
| Duplicate records | unidentified | 40 identified |
| Invalid/missing ages | unknown | 27 identified |
| Invalid/missing salaries | unknown | 38 identified |
| Unparseable hire dates | unknown | 81 identified |
| Invalid email addresses | unknown | 37 identified |

## Outcome
233 of 420 records (55.5%) passed every validation check and were ready to use
immediately. The remaining 187 were not discarded — each is flagged with the exact
issue found, so review time is targeted only where needed.

## Tools used
Excel/Google Sheets formulas: TRIM, PROPER, UPPER, INDEX, MATCH, IFERROR, SUBSTITUTE,
VALUE, DATEVALUE, FIND, COUNTIF, conditional formatting, lookup-table standardization.
