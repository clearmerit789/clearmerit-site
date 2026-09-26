# Spreadsheet Cleanup Before Automation Checklist

A small checklist for Excel / Google Sheets / CSV workflows that are about to be automated.

**CLEAR MERIT note:** This is a public working resource derived from recurring paid-demand patterns and our own Internal / Working Demo practices. It is **not external client production proof**.

## Why this exists

Automation can make a clean process faster.

It can also make a messy process fail faster.

Before adding Apps Script, n8n, Make, Zapier, AI, or a larger system, lock the data rules first.

## 1. Preserve the raw source

- Keep an untouched source copy.
- Record when the source was received/exported.
- Do not overwrite the only original file.
- If multiple files exist, identify which one is authoritative.

**Pass condition:** you can always return to the original data.

## 2. Define the duplicate key

Write down what makes two rows "the same."

Examples:
- Order ID
- Email + submission date
- Employee ID
- Invoice number
- Customer + site + service date

Do not deduplicate only because two rows look similar.

**Pass condition:** the duplicate rule can be explained in one sentence.

## 3. Normalize data types

Decide the accepted format for each important field.

Typical problem fields:
- dates
- currency
- percentages
- phone numbers
- IDs with leading zeroes
- status values
- free-text categories

**Pass condition:** every important column has one intended data type / format.

## 4. Separate safe fixes from ambiguous fixes

Some corrections are deterministic:
- trim extra spaces
- normalize date format
- remove exact duplicate rows
- standardize known status labels

Some are not:
- guessing a missing customer
- deciding which conflicting amount is correct
- merging two almost-matching people
- correcting an unclear ID

Ambiguous rows should go to a **Review** queue instead of being silently changed.

**Pass condition:** the process knows when to stop and ask a human.

## 5. Protect formulas and calculated fields

Check:
- formulas copied down consistently
- references do not shift unexpectedly
- imported values do not overwrite formulas
- blanks and errors are handled intentionally
- totals still reconcile after cleanup

**Pass condition:** formula outputs match the agreed test cases.

## 6. Add validation before automation

Useful controls include:
- dropdowns for status/category
- required-field checks
- numeric/date validation
- duplicate warning
- allowed-value lists
- Review flag for exceptions

**Pass condition:** common bad inputs are caught before they spread.

## 7. Reconcile the result

After cleanup, compare the result with the source.

At minimum check:
- source row count
- output row count
- duplicates removed
- rows held for review
- key totals / subtotals
- expected missing values

**Pass condition:** every row difference is explainable.

## 8. Test the second run

A workflow that works once may fail on rerun.

Ask:
- Will the same input create duplicate rows?
- Will the same email/form submission be processed twice?
- Will a retry send the same external message twice?
- Can the workflow tell "already processed" from "new"?

Use an idempotency / unique-key rule when external side effects are involved.

**Pass condition:** running the same test input twice does not create unintended duplicate outcomes.

## 9. Confirm ownership and handoff

For the final workbook/process, define:
- owner
- source of truth
- who reviews exceptions
- what counts as complete
- what happens when the owner is absent
- where the rules are documented

**Pass condition:** another person can operate it without reconstructing the rules from memory.

## 10. Automate only the repeatable path

Only after the checks above pass, choose the part worth automating.

A good first scope is usually:

**one representative file + one cleanup rule set + one repeatable automation path + explicit acceptance checks**

Avoid rebuilding the entire process before the smallest paid/useful path is proven.

---

## 15-minute pre-automation diagnosis

Before starting, answer these six questions:

1. What is the raw input?
2. What output must be trusted?
3. What makes a row unique?
4. Which corrections are safe to make automatically?
5. Which cases require human review?
6. What exact checks prove the result is correct?

If those answers are unclear, fix the rules before adding more automation.

---

CLEAR MERIT  
Operational workflow fixes, spreadsheet/data cleanup, automation QA, and bounded back-office improvements.

https://clearmerit.kr
