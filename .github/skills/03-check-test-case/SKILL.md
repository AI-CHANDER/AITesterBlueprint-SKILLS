# Verify Test Cases for a JIRA Ticket
---
name: 03-check-test-case
description: >

  Verify whether JIRA test cases provide complete coverage for a requirement, user story, acceptance criteria, business rules, and important test scenarios. 
  
  Use when a Senior tester or QA lead says "verify a test cases for JIRA-XXXX", "verify test cases for this story", "what should we verify here", or pastes an acceptance-criteria / user-story ticket, "check whether all test cases are
  covered", "find uncovered test cases", or provides a requirement/story together with existing JIRA test cases. 
  
  Compares requirements against existing tests, identifies covered and uncovered areas, calculates coverage, and produces a list of missing test cases for human review.
license: MIT
metadata:
  author: Chander Shekher
  stlc-phase: Verify the test cases
  version: 1.0.1
---

license: MIT
metadata:
  author: Chander Shekher
  stlc-phase: Test Design / Test Coverage Verification
  version: 1.0.0
---

# Test Case Coverage Verifier

You produce a **test coverage verification report for human review** — never treat the result as automatically final or approved.

Your job is to compare the source requirements against the test cases that already exist,
identify coverage gaps, and suggest missing test cases. Do not silently assume that a
test case covers a requirement when the mapping is unclear.

## When to use

- A JIRA key or story/requirement is provided and someone wants to verify test coverage.
- Existing JIRA test cases are available and someone wants to know whether all requirements
  and acceptance criteria are covered.
- Someone asks "are all test cases covered?", "what is missing?", or "find uncovered scenarios".
- Someone wants a list of additional test cases required for uncovered requirements.

## Workflow (follow in order)

### 1. Collect the source requirement

- If a JIRA key is given (for example `VOC-1234`), fetch the ticket.
- Prefer an available JIRA MCP tool.
- If no JIRA MCP tool is available, use an approved JIRA REST/API integration if configured.
- If neither works, ask the user to paste the requirement/story content — **do not invent
  requirement content**.
- Capture:
  - Summary
  - Description
  - Acceptance criteria
  - Business rules
  - Constraints
  - Components/modules
  - Linked requirements/issues
  - Relevant attachments
  - Sprint/fix version when useful for traceability

### 2. Collect the existing Jira test cases

- Retrieve all test cases linked to the requirement/story when the available JIRA integration
  supports this.
- Include test cases linked directly or through the project's supported traceability
  relationship.
- Capture only information needed for coverage analysis:
  - Test case ID/key
  - Test case title/summary
  - Description
  - Preconditions
  - Test steps
  - Expected results
  - Test type/labels/components when available
  - Requirement/story relationship
- Do not expose reporter, assignee, email, credentials, tokens, or other unnecessary
  personal information.

If the test cases cannot be fetched, ask the user to provide/export them. **Do not assume
that missing data means there are no test cases.**

### 3. Break requirements into testable coverage points

Convert the source requirement into atomic coverage points.

Consider:

- Each acceptance criterion
- Functional requirements
- Business rules
- Positive scenarios
- Negative scenarios
- Mandatory/optional field validation
- Boundary and limit conditions
- Invalid data
- Empty/null values
- Error handling
- Authentication and authorization
- Role/permission behavior
- Integration behavior
- Data validation
- State transitions
- Notifications
- Regression-impact areas
- API request/response validation where applicable
- UI behavior where applicable

Only include scenario types that are relevant to the requirement. Do not create artificial
coverage requirements.

### 4. Map requirements to existing Jira test cases

For every coverage point, determine:

- **Covered** — one or more existing test cases clearly verify it.
- **Partially Covered** — related coverage exists, but an important condition or path is
  missing.
- **Uncovered** — no existing test case verifies it.
- **Ambiguous** — a test may cover it, but the relationship cannot be confirmed from the
  available information.

Do not mark a requirement as covered only because the test title contains similar words.
Review the actual test steps and expected results when available.

Maintain traceability:

`Requirement / AC → Existing Test Case(s) → Coverage Status`

### 5. Identify uncovered test cases

For every **Uncovered** or relevant **Partially Covered** item, create a concise missing
test case proposal.

Use this format:

- **Test Case Title**
- **Requirement / Acceptance Criterion**
- **Scenario**
- **Precondition**
- **Test Steps**
- **Expected Result**
- **Priority** — P0 / P1 / P2
- **Reason for Gap**

Do not duplicate an existing Jira test case.

### 6. Calculate coverage

Calculate:

`Coverage % = (Fully Covered Coverage Points ÷ Total Applicable Coverage Points) × 100`

Also report:

- Total coverage points
- Fully covered
- Partially covered
- Uncovered
- Ambiguous
- Existing Jira test cases reviewed
- Additional test cases recommended

Do not use the raw number of Jira test cases as the denominator. One test case can cover
multiple requirements, and multiple test cases can cover one requirement.

### 7. Produce the verification report

Use this output structure:

## Test Case Coverage Verification — <JIRA-KEY>: <title>

### 1. Coverage Summary

| Metric | Result |
|---|---:|
| Requirements / Acceptance Criteria | XX |
| Applicable Coverage Points | XX |
| Jira Test Cases Reviewed | XX |
| Fully Covered | XX |
| Partially Covered | XX |
| Uncovered | XX |
| Ambiguous | XX |
| Coverage | XX% |

### 2. Requirement-to-Test Traceability

| # | Requirement / Acceptance Criterion | Jira Test Case(s) | Coverage |
|---|---|---|---|
| 1 | | | Covered |
| 2 | | | Partially Covered |
| 3 | | | Uncovered |

### 3. Covered Areas

List the requirements/scenarios that are clearly covered and identify the Jira test case(s).

### 4. Coverage Gaps

List only the areas that are partially covered, uncovered, or ambiguous.

### 5. Uncovered Test Cases

Generate the proposed missing test cases using the format from Step 5.

### 6. Final Coverage Status

Use one of:

- **PASS — 100% Coverage**
- **PARTIAL — Coverage Gaps Found**
- **FAIL — Major Coverage Missing**
- **REVIEW REQUIRED — Coverage Cannot Be Confirmed**

### 7. Human Review Gate

Summarize:

- What was verified
- What was assumed
- What could not be confirmed
- Which existing tests may need review
- Which new test cases are recommended

End with:

**Please review the uncovered/partially covered scenarios and confirm before creating or
modifying Jira test cases.**

## Output principles

- Keep the result focused on **coverage**, not general test-case quality.
- Show the mapping between requirements and existing Jira tests.
- Generate missing test cases only for genuine coverage gaps.
- Prefer concise, actionable gap descriptions.
- Preserve the terminology used in the Jira requirement.
- Keep every proposed test case traceable to a specific requirement, acceptance criterion,
  or identified coverage gap.

## Guardrails

- Never fabricate requirements, acceptance criteria, or existing Jira test cases.
- Never claim 100% coverage when any applicable requirement is uncovered or ambiguous.
- Do not treat a similar test title as proof of coverage.
- Do not count duplicate test cases as additional coverage.
- Do not create unnecessary test scenarios that are not supported by the requirement.
- Do not modify, create, delete, or approve Jira test cases unless the user explicitly asks
  for that action and the connected tool supports it.
- Never expose credentials, API tokens, passwords, or secrets.
- Do not expose unnecessary personal information such as reporter, assignee, email, or
  contact details.
- A human must review the final coverage result before it is treated as approved.

## Example decision

If the requirement contains:

- Valid login
- Invalid password
- Locked account
- Empty password validation

And Jira contains tests for:

- Valid login
- Invalid password

The result should be:

- Valid login → **Covered**
- Invalid password → **Covered**
- Locked account → **Uncovered**
- Empty password validation → **Uncovered**

Coverage:

`2 / 4 × 100 = 50%`

Recommended missing tests:

- Verify login behavior when the account is locked.
- Verify validation when the password field is empty.

## References

- `references/testcase-coverage-template.md` — standard coverage verification output
- `references/coverage-checklist.md` — requirement and scenario coverage checklist
- `scripts/fetch_jira.sh` — optional JIRA retrieval script
