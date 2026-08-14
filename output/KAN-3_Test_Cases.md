# Test Cases — KAN-3: Create test cases for login functionality and SRS document

> **Status:** DRAFT — pending human review
> **Source ticket:** [KAN-3](https://jiracshekher007.atlassian.net/browse/KAN-3) (AI_QA project)
> **Generated from:** the actual KAN-3 ticket fetched from JIRA (2026-08-14)
> **Note:** Test cases below are derived **only** from the KAN-3 ticket content (summary + description) and the skill's requirement checklist. Where the ticket is silent, the gap is flagged as a question for the author — nothing is fabricated.

---

## 1. Document Information

| Field | Value |
|---|---|
| Project Name | AI_QA |
| Ticket | KAN-3 — Create test cases for login functionality and SRS document |
| Ticket Type | Task |
| Priority | Medium |
| Status | To Do |
| Document Version | 0.1 (Draft) |
| Author | Test Case Generator (skill) |
| Reviewer | TBD |
| Approval Date | TBD |
| Product/Application | Not stated in the ticket (TBD) |

---

## 2. Objective

Deliver two artifacts for KAN-3:

1. **Test cases for the login functionality** — a traceable, review-ready set of test cases covering the login module described in the ticket.
2. **SRS (Software Requirements Specification) document** — verification support: test cases that check the SRS document itself for completeness, clarity, and testability.

---

## 3. Scope

### In Scope

- Functional test cases for the login module (per ticket description)
- Boundary and empty-state test cases
- Security-oriented login cases
- SRS document review/verification test cases
- Traceability to requirements (RTM)

### Out of Scope

- Automation script implementation (test case design only)
- Performance / load testing
- Penetration testing
- Non-login features (post-login modules are only referenced as context)

---

## 4. Ticket Requirements (from the actual KAN-3 description)

**R1 — Secure authentication:** The Login module allows registered users to securely authenticate themselves before accessing features that require an authenticated account.

**R2 — Post-login access:** An authenticated user may subsequently access functions such as:
- Product browsing
- Product customization
- Customer information
- Orders
- Order history
- Communication
- Payment-related functionality
- Delivery information

**R3 — Login page elements** (as applicable):
- Email/mobile/username field
- Password field
- Login button
- Forgot Password option
- Password visibility control
- Remember Me option (if supported)

> **Gap:** No acceptance criteria, target URL/environment, credential rules (identifier type, min/max length, case sensitivity), or expected error messages are specified in the ticket. These are flagged in Section 8.

---

## 5. Test Case Design Techniques Applied

- Equivalence Partitioning (valid / invalid credential classes)
- Boundary Value Analysis (empty, single-char, max-length inputs)
- Error Guessing (wrong identifier, wrong password, both wrong)
- Use Case Testing (primary login journey)
- Requirements Review Checklist (SRS verification cases)

---

## 6. Test Cases

### 6.1 Login Functionality — Test Cases

| TC ID | Test Case Title | Preconditions | Test Steps | Test Data | Expected Result | Priority | Maps To |
|---|---|---|---|---|---|---|---|
| TC-01 | Verify login page loads successfully | Login page URL is accessible | 1. Open the login page URL<br>2. Observe page title, URL, and form elements | Login page URL (TBD) | Login page loads; email/mobile/username field, password field and Login button are visible | P0 | R3 |
| TC-02 | Verify login with valid credentials | Registered user credentials available | 1. Enter valid email/mobile/username<br>2. Enter valid password<br>3. Click Login | Valid credentials (TBD) | User is authenticated and granted access to authenticated features | P0 | R1 |
| TC-03 | Verify access to post-login features after successful login | Valid credentials | 1. Login successfully<br>2. Access each authenticated function | Valid credentials | Authenticated user can access Product browsing, Product customization, Customer information, Orders, Order history, Communication, Payment-related functionality, Delivery information | P0 | R2 |
| TC-04 | Verify login with invalid identifier (email/mobile/username) | Login page loaded | 1. Enter invalid identifier<br>2. Enter valid password<br>3. Click Login | Invalid identifier (e.g. `invalid@test.com`) | Appropriate error message displayed; user stays on login page; no authentication | P0 | R1 |
| TC-05 | Verify login with invalid password | Login page loaded | 1. Enter valid identifier<br>2. Enter invalid password<br>3. Click Login | Invalid password (e.g. `WrongPass!1`) | Appropriate error message displayed; user stays on login page; no authentication | P0 | R1 |
| TC-06 | Verify login with both identifier and password invalid | Login page loaded | 1. Enter invalid identifier<br>2. Enter invalid password<br>3. Click Login | Invalid identifier + invalid password | Appropriate error message displayed; no authentication | P1 | R1 |
| TC-07 | Verify login with empty identifier field | Login page loaded | 1. Leave identifier empty<br>2. Enter valid password<br>3. Click Login | Empty identifier | Field validation/error message displayed; no authentication | P1 | R3 |
| TC-08 | Verify login with empty password field | Login page loaded | 1. Enter valid identifier<br>2. Leave password empty<br>3. Click Login | Empty password | Field validation/error message displayed; no authentication | P1 | R3 |
| TC-09 | Verify login with both fields empty | Login page loaded | 1. Leave both fields empty<br>2. Click Login | Empty identifier + empty password | Validation messages displayed for both fields; no authentication | P1 | R3 |
| TC-10 | Verify login with whitespace-only input | Login page loaded | 1. Enter spaces in identifier field<br>2. Enter spaces in password field<br>3. Click Login | `"   "` / `"   "` | Inputs trimmed/treated as empty or explicit error; no authentication | P1 | R3 |
| TC-11 | Verify login with single-character input | Login page loaded | 1. Enter 1-char identifier<br>2. Enter 1-char password<br>3. Click Login | `a` / `b` | Error message or min-length validation; no authentication | P2 | R3 |
| TC-12 | Verify login with maximum-length input | Login page loaded | 1. Enter max-length identifier<br>2. Enter max-length password<br>3. Click Login | Max-length strings (limits TBD) | Input accepted or clean validation error; no crash | P2 | R3 |
| TC-13 | Verify identifier is case-sensitive | Login page loaded | 1. Enter identifier with wrong case<br>2. Enter correct password<br>3. Click Login | Mismatched-case identifier | Case mismatch → error message (if case-sensitive; TBD) | P1 | R3 |
| TC-14 | Verify password visibility control | Login page loaded | 1. Enter a password<br>2. Toggle the password visibility control | Password text | Password is masked by default; toggling reveals/hides the text | P1 | R3 |
| TC-15 | Verify Forgot Password option | Login page loaded | 1. Click Forgot Password<br>2. Follow the flow | Registered email/mobile | Forgot-password flow initiates correctly (e.g. reset link/OTP sent) | P1 | R3 |
| TC-16 | Verify Remember Me behavior (if supported) | Login page loaded | 1. Select Remember Me<br>2. Login<br>3. Close and reopen browser | Valid credentials | Session persists per Remember Me selection | P2 | R3 |
| TC-17 | Verify error message for invalid credentials | Login page loaded | 1. Enter invalid credentials<br>2. Click Login | Invalid credentials | Error message text is deterministic and assertable (exact text TBD) | P0 | R1 |
| TC-18 | Verify no sensitive data exposure in error | Login page loaded | 1. Enter invalid credentials<br>2. Observe error and page source | Invalid credentials | Error does not reveal password, tokens, or internal details | P1 | R1 |
| TC-19 | Verify session created after successful login | Valid credentials | 1. Login successfully<br>2. Inspect session cookie | Valid credentials | Session cookie set; secure flag present over HTTPS | P2 | R1 |
| TC-20 | Verify login with unregistered identifier | Login page loaded | 1. Enter unregistered identifier<br>2. Enter any password<br>3. Click Login | Unregistered identifier (e.g. `nobody@test.com`) | Appropriate error message; no authentication | P1 | R1 |
| TC-21 | Verify login with disabled/locked account | Disabled account available | 1. Enter disabled account credentials<br>2. Click Login | Disabled account (TBD) | Clear lockout/disabled message; no authentication | P2 | R1 |
| TC-22 | Verify login with special characters in credentials | Login page loaded | 1. Enter identifier with special chars<br>2. Enter password with special chars<br>3. Click Login | Special-char credentials | Input handled without error/validation issues | P2 | R3 |
| TC-23 | Verify login button state during submission | Login page loaded | 1. Enter valid credentials<br>2. Click Login and observe button state | Valid credentials | Button disabled/loading during request; no duplicate submissions | P2 | R3 |
| TC-24 | Verify unauthenticated access is blocked | No active session | 1. Attempt to access authenticated features directly (e.g. Orders) | — | Unauthenticated user is redirected to login or blocked | P1 | R1 |

### 6.2 SRS Document — Verification Test Cases

| TC ID | Test Case Title | Preconditions | Test Steps | Expected Result | Priority | Maps To |
|---|---|---|---|---|---|---|
| SRS-01 | Verify SRS document exists and is accessible | SRS document delivered | 1. Locate SRS document in deliverables folder<br>2. Open the document | SRS document exists at known path and opens without corruption | P0 | Summary: SRS document |
| SRS-02 | Verify SRS covers login functionality | SRS document available | 1. Review SRS login section<br>2. Check for functional requirements for login | Login requirements exist: secure authentication, post-login access, login page elements | P0 | R1, R2, R3 |
| SRS-03 | Verify SRS acceptance criteria are testable | SRS document available | 1. Review each requirement<br>2. Check for observable pass/fail criteria | Every requirement has testable acceptance criteria; no vague terms ("should", "etc.") | P0 | Gap: testability |
| SRS-04 | Verify SRS covers boundary and error states | SRS document available | 1. Check for empty, invalid, max-length input requirements | Boundary and error-state requirements are specified | P1 | Gap: boundary/error |
| SRS-05 | Verify SRS covers non-functional requirements | SRS document available | 1. Check for security, performance, a11y, i18n requirements | NFRs relevant to login are present (or explicitly out of scope) | P1 | Gap: non-functional |
| SRS-06 | Verify SRS has consistent terminology and defined terms | SRS document available | 1. Check glossary/definitions<br>2. Verify terms used consistently | Terms defined and used consistently (e.g. "identifier", "authenticated user") | P1 | Gap: clarity |
| SRS-07 | Verify SRS traceability to test cases | SRS document + test cases | 1. Map each login requirement to test cases<br>2. Update RTM | Every requirement maps to ≥1 test case; no orphan requirements | P1 | Gap: traceability |
| SRS-08 | Verify SRS versioning and change history | SRS document available | 1. Check version number<br>2. Check revision/change history table | Version and change history recorded | P2 | Gap: document quality |

---

## 7. Test Data & Environment

### Test Data (all TBD — pending author confirmation)

| Data | Value | Notes |
|---|---|---|
| Valid identifier (email/mobile/username) | TBD | Must be a registered, active account |
| Valid password | TBD | Store in secrets manager, never in repo |
| Invalid identifier | TBD | e.g. `invalid@test.com` |
| Invalid password | TBD | e.g. `WrongPass!1` |
| Unregistered identifier | TBD | e.g. `nobody@test.com` |
| Disabled/locked account | TBD | For TC-21 |

### Environment

- Login page URL (TBD)
- Browser: TBD
- Target application: not stated in the ticket

---

## 8. Entry & Exit Criteria

### Entry

- KAN-3 requirements clarified (see open questions in Section 10)
- Login page available at known URL
- SRS document delivered
- Valid test credentials provisioned

### Exit

- All P0 test cases pass (once approved)
- SRS verification completed
- Defects (if any) logged in Jira
- Test execution report produced

---

## 9. Risks & Assumptions

### Assumptions

- A login page/module exists at a known URL (to be confirmed by the author).
- Valid registered-user credentials will be provided externally.
- "Appropriate error messages" means deterministic, assertable strings.
- An SRS document for the login module exists or will be delivered for review.

### Risks

| Risk | Mitigation |
|---|---|
| No acceptance criteria in ticket | Blocking — require clarification from ticket author |
| No valid credentials | Blocking — request from ticket author |
| Target URL not confirmed | Blocking — confirm which login page |
| SRS not yet delivered | Blocking — confirm delivery timeline |
| CAPTCHA / 2FA / SSO on login | Use test env with these disabled or handled |
| Error message wording varies by locale | Pin exact expected strings after first run |

---

## 10. Human Review Gate

> **Do not proceed to automation or treat this as final until a human approves.**

### Assumptions made

- A login module exists at a URL to be confirmed — **not stated in KAN-3**.
- Valid registered-user credentials will be supplied externally — **not in the ticket**.
- The SRS document is a deliverable to be reviewed against these cases.
- Error messages are deterministic and assertable — exact text to be confirmed.

### Open questions for the ticket author (blocking)

1. **Which application and login URL** do these test cases target? The ticket does not name the product/application.
2. **What are the valid test credentials** (and where should they be stored)?
3. What **exact error message text** is expected for invalid credentials (identifier vs password)?
4. Is the identifier an **email, mobile number, or username** — and is it case-sensitive? What are the **min/max length** rules?
5. Is there **CAPTCHA / 2FA / SSO** on login that must be handled or bypassed?
6. Does the **SRS document already exist**, and where is it located? If not, is writing the SRS part of this ticket's scope?
7. Which **browsers/platforms** must be supported?
8. Should these test cases be **executed manually or automated**, and in which CI?

### Required before sign-off

- [ ] Confirm target application and login URL
- [ ] Provide valid test credentials
- [ ] Confirm expected error-message strings
- [ ] Confirm identifier type and field rules (case sensitivity, length limits)
- [ ] Confirm SRS document availability/location
- [ ] Approve test case scenarios (P0/P1/P2)
