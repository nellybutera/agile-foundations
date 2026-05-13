# Sprint 1 Review

**Sprint dates:** Mar 11 – 19, 2026  
**Sprint goal:** Deliver a working console application supporting customer registration, account creation, and core financial transactions — backed by validated input and a foundational test suite.

---

## Delivered Stories

| Story | Description | Status | Tests Added |
|---|---|---|---|
| US-01 | Customer registration (Regular + Premium types, email validation) | ✓ Done | `AccountServiceTest` |
| US-02 | Account creation — Savings ($500 min, 3.5% interest) and Checking ($1,000 overdraft, $10 fee) | ✓ Done | `AccountTest` |
| US-03 | Deposit — balance update + ledger entry | ✓ Done | `AccountTest` |
| US-04 | Withdrawal — balance update, overdraft guard, min-balance guard | ✓ Done | `AccountTest`, `ExceptionTest` |

All four stories met the Definition of Done: compiled, tested, Javadoc'd, and reachable from the console menu.

---

## Key Commits

| Date | Commit | What it delivered |
|---|---|---|
| Mar 11 | `Initial commit` through `added bank class, account manager and transaction manager` | Complete domain model: Customer, Account (Savings/Checking), Transaction, Bank, AccountManager, TransactionManager |
| Mar 12–13 | `Refactored banking architecture for Single Source of Truth` → `main class complete` | SSOT architecture enforced; Main class and interactive menu wired end-to-end |
| Mar 13–16 | `Fixed design flow: allowing multiple accounts per customer` | Corrected the account-customer ownership model; one customer can hold multiple accounts |
| Mar 17 | `Refactored AccountManager and Transaction Manager` | Separated account management and transaction ledger responsibilities; reduced coupling |
| Mar 19 | `Added try catch blocks` → `added OverdraftLimitExceededException` → `Merge pull request #1` | Full exception hierarchy (7 custom exceptions), input validation, Javadoc, test suite — merged via PR #1 from apprenticeship review branch |

---

## Test Results

**Test suite at end of Sprint 1:** 17 tests across `AccountTest` and `AccountServiceTest`

All 17 tests passed. Coverage focused on:
- Account creation with correct initial state
- Deposit and withdrawal with boundary values
- Exception cases: insufficient funds, closed-account operations, invalid inputs

_Note: The CI pipeline was not yet live in Sprint 1 — tests were run locally via `mvn test`. Setting up automated CI was scoped to Sprint 2._

---

## Demo Summary

By the end of Sprint 1, a bank teller could:

1. Register a new Regular or Premium customer with validated email
2. Open a Savings or Checking account with an initial deposit
3. Deposit funds into any active account
4. Attempt a withdrawal — the system enforces overdraft limits and minimum balance rules and raises a descriptive error when either is breached
5. Navigate a clean 7-option console menu grouped by domain (Manage Accounts, Process Transaction, etc.)

The application ran entirely in-memory at this stage — data did not survive a restart. Persistence was deferred to Sprint 2.
