# Test Plan — KAN-2: Automate Login Functionality

> **Status:** DRAFT — pending human review
> **Source ticket:** [KAN-2](https://jiracshekher007.atlassian.net/browse/KAN-2) (AI_QA project)
> **Generated from:** the actual KAN-2 ticket fetched from JIRA (2026-08-14)

---

## 1. Document Information

| Field | Value |
|---|---|
| Project Name | AI_QA |
| Product/Application | VWO (Wingify) — Login page (subject to confirmation) |
| Version | TBD |
| Test Plan Version | 0.1 (Draft) |
| Author | Test Plan Generator (skill) |
| Reviewer | TBD |
| Approval Date | TBD |

---

## 2. Objective

Automate the login functionality using **Selenium with Python and Pytest**, per KAN-2. The automation must:

- Verify successful login with **valid credentials**.
- Verify **appropriate error messages** for **invalid credentials**.
- Add **assertions** to validate expected results.

The goal is a repeatable, CI-ready automated login test suite that catches regressions in the login flow.

---

## 3. Scope

### In Scope

- Functional Testing (login happy path & error paths)
- UI automation (Selenium)
- Data-driven / parametrized credential tests
- Assertions on success redirect + error message content
- CI/CD execution readiness (headless browser)

### Out of Scope

- Mobile / responsive testing
- Performance / load testing
- Security testing (penetration)
- Non-login features

---

## 4. Features to be Tested

- Login page loading
- Valid credential login → successful navigation to dashboard/home
- Invalid username → appropriate error message
- Invalid password → appropriate error message
- Empty fields → validation message (boundary)
- Assertions validating expected vs. actual results

---

## 5. Test Environment

| Environment | URL | Purpose |
|---|---|---|
| QA | TBD | Primary automation target |
| UAT | TBD | Optional |
| Pre-Prod | TBD | Optional |
| Production | TBD | Not recommended for automation |

### Supported Platforms

- Windows (primary)
- macOS (CI parity)

### Supported Browsers

- Chrome (primary)
- Edge (optional)
- Firefox (optional)

---

## 6. Defect Management

### Defect Lifecycle

New → Assigned → In Progress → Fixed → Retest → Closed (Reopened as needed)

### Defect Tool

Jira (AI_QA project)

### Severity

Critical / High / Medium / Low

### Priority

P1 / P2 / P3 / P4

---

## 7. Test Strategy

### Test Design Techniques

- Equivalence Partitioning (valid / invalid credential classes)
- Boundary Value Analysis (empty, single-char, max-length inputs)
- Error Guessing (wrong username, wrong password, both wrong)
- Use Case Testing (login as primary user journey)

### Execution Strategy

1. Smoke test on a stable login page
2. Functional validation of each login scenario
3. Regression on login flow
4. CI run (headless)

### Best Practices

- Shift-Left Testing
- Risk-Based Testing
- Continuous Testing (CI pipeline)

---

## 8. Test Schedule

| Activity | Planned Date | Owner | Status |
|---|---|---|---|
| Test Planning | TBD | QA Lead | Draft |
| Test Case Design | TBD | Test Engineer | Pending |
| Test Execution | TBD | Test Engineer | Pending |
| Regression | TBD | Test Engineer | Pending |
| Closure | TBD | QA Lead | Pending |

---

## 9. Test Deliverables

- Test Plan (this document)
- Automated test suite (Python + Pytest + Selenium)
- Test Execution Report
- Defect Report
- Test Summary Report
- Sign-off Document

---

## 10. Test Scenarios (P0/P1/P2)

Each scenario maps to an explicit requirement in the ticket or a gap identified below.

| ID | Scenario | Expected Result | Priority | Maps To |
|---|---|---|---|---|
| TC-01 | Login page loads successfully | Page title/URL correct, login form visible | P0 | AC: verify login |
| TC-02 | Valid credentials → login | Successful navigation to dashboard/home | P0 | AC: valid login |
| TC-03 | Invalid username | Appropriate error message displayed | P0 | AC: invalid creds |
| TC-04 | Invalid password | Appropriate error message displayed | P0 | AC: invalid creds |
| TC-05 | Both username & password invalid | Appropriate error message displayed | P1 | Gap: negative path |
| TC-06 | Empty username field | Validation/error message displayed | P1 | Gap: boundary |
| TC-07 | Empty password field | Validation/error message displayed | P1 | Gap: boundary |
| TC-08 | Whitespace-only input | Treated as empty or error message | P1 | Gap: boundary |
| TC-09 | Case-sensitive username/password | Mismatched case → error message | P1 | Gap: ambiguity |
| TC-10 | Assertions validate all expected results | No false positives; each assertion maps to expected state | P0 | AC: assertions |
| TC-11 | Locked/disabled account (if applicable) | Clear lockout message | P2 | Gap: security |
| TC-12 | Session/cookie set after login | Session persists; logout works | P2 | Gap: state |

---

## 11. Test Data & Environment

### Test Data

| Data | Value | Notes |
|---|---|---|
| Valid username | TBD (from test env) | Must be a real active account |
| Valid password | TBD (from test env / secrets) | Store securely, never in repo |
| Invalid username | TBD | e.g. `invalid_user@test.com` |
| Invalid password | TBD | e.g. `WrongPass!1` |

### Environment

- Base URL of the login page (TBD)
- Browser: Chrome (headless for CI)
- WebDriver: Selenium WebDriver matching browser version

---

## 12. Entry & Exit Criteria

### Entry

- Stable login page available at known URL
- Valid test credentials provisioned
- Selenium/Pytest environment ready

### Exit

- All P0 scenarios pass
- All assertions validated
- Defects (if any) logged in Jira
- Test execution report produced

---

## 13. Risks & Assumptions

### Assumptions

- The login page under test is the VWO (Wingify) login at the app URL (to be confirmed by author).
- Valid credentials will be provided by the ticket owner (not included in the ticket).
- Browser automation (Selenium) is permitted on the target environment.
- The error message text for invalid credentials is deterministic and assertable.

### Risks

| Risk | Mitigation |
|---|---|
| No valid credentials provided | Blocking — request from ticket author |
| Target URL not confirmed | Blocking — confirm which login page |
| Error message wording varies by locale | Pin exact expected strings after first run |
| CAPTCHA / 2FA on login | Use test environment with CAPTCHA/2FA disabled or handled |
| Headless browser differences | Run smoke locally + headless in CI |
| Credentials stored insecurely | Use env vars / secrets manager, never commit |

---

## 14. Human Review Gate

> **Do not proceed to writing test cases or automation until a human approves.**

### Assumptions made

- Target app is the VWO (Wingify) login page — **not stated in the ticket**.
- Valid test credentials will be supplied externally — **not in the ticket**.
- "Appropriate error messages" means deterministic, assertable strings.

### Open questions for the ticket author (blocking)

1. **Which application/login URL** should the automation target? (VWO/Wingify app URL?)
2. **What are the valid test credentials** (and where should they be stored)?
3. What **exact error message text** is expected for invalid credentials (username vs password)?
4. Is there **CAPTCHA / 2FA / SSO** on the login that the automation must handle or bypass?
5. Which **browsers/platforms** must the suite support (Chrome only, or Edge/Firefox too)?
6. Should the suite run in **CI (headless)** — and if so, which pipeline?

### Required before sign-off

- [ ] Confirm target login URL
- [ ] Provide valid test credentials
- [ ] Confirm expected error-message strings
- [ ] Confirm browser/platform matrix
- [ ] Approve test scenarios (P0/P1/P2)
