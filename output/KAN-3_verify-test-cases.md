# Test Case Coverage Verification — KAN-3: Create test cases for login functionality and SRS document

> **Status:** DRAFT — pending human review
> **Source ticket:** [KAN-3](https://jiracshekher007.atlassian.net/browse/KAN-3) (AI_QA project)
> **Verified against:** the actual KAN-3 ticket fetched from JIRA (2026-08-17) and `output/KAN-3_Test_Cases.md`
> **Method:** 03-check-test-case skill — requirement-to-test-case traceability

---

## 1. Requirement Information

| Field | Details |
|---|---|
| Project | AI_QA |
| Ticket | KAN-3 — Create test cases for login functionality and SRS document |
| Ticket Type | Task |
| Priority | Medium |
| Status | To Do |
| Feature / Module | Login functionality + SRS document verification |
| Reviewed Date | 2026-08-17 |
| Reviewed By | Test Case Coverage Verifier (skill) |

---

## 2. Coverage Summary

| Metric | Result |
|---|---:|
| Requirements / Acceptance Criteria | 3 (R1, R2, R3) |
| Applicable Coverage Points | 3 |
| Jira Test Cases Reviewed | 32 (24 login + 8 SRS) |
| Fully Covered | 3 |
| Partially Covered | 0 |
| Uncovered | 0 |
| Ambiguous | 0 |
| Coverage | **100%** |

> **Note:** Coverage is computed at requirement level. The ticket contains **no explicit acceptance criteria** — coverage is derived from the ticket description only.

---

## 3. Requirement-to-Test Traceability

| # | Requirement / Acceptance Criterion | Jira Test Case(s) | Coverage |
|---|---|---|---|
| 1 | R1 — Secure authentication: registered users securely authenticate before accessing authenticated features | TC-02, TC-04, TC-05, TC-06, TC-17, TC-18, TC-19, TC-20, TC-21, TC-24 | Covered |
| 2 | R2 — Post-login access: product browsing, product customization, customer information, orders, order history, communication, payment-related functionality, delivery information | TC-03 | Covered |
| 3 | R3 — Login page elements: email/mobile/username field, password field, Login button, Forgot Password, password visibility control, Remember Me | TC-01, TC-07, TC-08, TC-09, TC-10, TC-11, TC-12, TC-13, TC-14, TC-15, TC-16, TC-22, TC-23 | Covered |

---

## 4. Test Scenario Coverage

| Scenario Type | Covered? | Test Case ID(s) |
|---|---|---|
| Positive scenarios | Yes | TC-02, TC-03 |
| Negative scenarios | Yes | TC-04, TC-05, TC-06, TC-20, TC-21, TC-24 |
| Mandatory field validation | Yes | TC-07, TC-08, TC-09 |
| Optional field validation | Yes | TC-16 (Remember Me) |
| Boundary conditions | Yes | TC-10, TC-11, TC-12 |
| Invalid data | Yes | TC-04, TC-05, TC-06, TC-22 |
| Error handling | Yes | TC-17, TC-18 |
| Authentication | Yes | TC-02, TC-19 |
| Authorization | Yes | TC-24 |
| Integration scenarios | NA | — |
| Business rules | NA | Ticket specifies no business rules |
| Data validation | Yes | TC-07, TC-08, TC-09, TC-10, TC-11, TC-12 |
| Regression impact | NA | — |
| SRS document verification | Yes | SRS-01 to SRS-08 |

---

## 5. Covered Areas

- **R1 — Secure authentication:** fully covered by 10 test cases spanning valid login (TC-02), invalid identifier/password/both (TC-04/05/06), deterministic error messages (TC-17), no sensitive data exposure (TC-18), session creation (TC-19), unregistered account (TC-20), disabled/locked account (TC-21), and unauthenticated access blocking (TC-24).
- **R2 — Post-login access:** covered by TC-03, which walks all 8 authenticated functions listed in the ticket (product browsing, customization, customer info, orders, order history, communication, payment, delivery).
- **R3 — Login page elements:** covered by TC-01 (page loads with identifier field, password field, Login button) plus dedicated cases for password visibility (TC-14), Forgot Password (TC-15), Remember Me (TC-16), and field-level validation for empty/whitespace/single-char/max-length/special-char inputs (TC-07–12, TC-22) and case sensitivity (TC-13).
- **SRS deliverable:** 8 verification cases (SRS-01–08) check SRS existence, login coverage, acceptance-criteria testability, boundary/error-state coverage, non-functional requirements, terminology consistency, traceability, and versioning/change history.

---

## 6. Coverage Gaps

No requirement-level gaps were found. However, the following items are **blocking execution** (they are gaps in the ticket/spec, not in test coverage):

1. **No acceptance criteria** exist in the KAN-3 ticket — the requirements are derived from the description only.
2. **Valid test credentials are TBD** — must be provisioned before execution.
3. **Target application / login URL is TBD** — the ticket does not name the product.
4. **Exact error-message strings are TBD** — required for deterministic assertion (TC-17).
5. **SRS document not yet delivered** — SRS-01 to SRS-08 verify a deliverable that does not yet exist.
6. **Credential rules are TBD** — identifier type (email/mobile/username), case sensitivity (TC-13), min/max length (TC-11/12).

---

## 7. Uncovered Test Cases

None required — all 3 requirement groups are covered by existing test cases.

---

## 8. Final Coverage Status

**PARTIAL — Coverage Gaps Found**

Requirement-level test coverage is 100%, but the ticket lacks acceptance criteria, test data, target environment, and the SRS deliverable, so the overall state is PARTIAL rather than PASS.

---

## 9. Human Review Gate

- **What was verified:** 32 test cases (24 login + 8 SRS) map to all 3 KAN-3 requirements extracted from the live JIRA ticket; requirement-level coverage is 100%.
- **What was assumed:** R1–R3 (from the ticket description) are the sole requirements, since the ticket contains no acceptance criteria.
- **What could not be confirmed:** actual execution results (no environment/credentials), and whether SRS-01–08 are valid before an SRS document exists.
- **Which existing tests may need review:** TC-13 (case sensitivity) and TC-19 (session cookie) are marked "TBD" pending spec confirmation.
- **Which new test cases are recommended:** none — coverage is complete at requirement level.

**Please review the uncovered/partially covered scenarios and confirm before creating or modifying Jira test cases.**
