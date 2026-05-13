# Sprint 1 — Review

![Status](https://img.shields.io/badge/Status-Complete-22c55e?style=flat-square)
![Stories](https://img.shields.io/badge/Stories_Delivered-4%2F4-22c55e?style=flat-square)
![Tests](https://img.shields.io/badge/Tests_Passing-17-3b82f6?style=flat-square)
![Points](https://img.shields.io/badge/Story_Points-11-8b5cf6?style=flat-square)

| | |
|---|---|
| **Sprint dates** | Mar 11 – 19, 2026 |
| **Sprint goal** | Core banking operations: customers, accounts, deposit, withdrawal |

---

## Sprint Goal Result

> [!NOTE]
> All four planned stories were delivered and met the Definition of Done. The application runs end-to-end from customer registration through account transactions. Data was in-memory only at this stage — persistence was scoped to Sprint 2.

---

## Delivered Stories

| Story | Description | Status | Tests Added |
|:---:|---|:---:|---|
| `US-01` | Customer registration — Regular + Premium types, email validation | ✅ Done | `AccountServiceTest` |
| `US-02` | Account creation — Savings (`$500` min, `3.5%` interest) and Checking (`$1,000` overdraft) | ✅ Done | `AccountTest` |
| `US-03` | Deposit — balance update and ledger entry | ✅ Done | `AccountTest` |
| `US-04` | Withdrawal — overdraft guard and minimum balance enforcement | ✅ Done | `AccountTest`, `ExceptionTest` |


## Key Commits

| Date | Commit | What it delivered |
|---|---|---|
| Mar 11 | `Initial commit` → `added bank class, account manager and transaction manager` | Complete domain model: Customer, Account (Savings/Checking), Transaction, Bank, AccountManager, TransactionManager |
| Mar 12–13 | `Refactored banking architecture for Single Source of Truth` → `main class complete` | SSOT architecture enforced; Main class and interactive menu wired end-to-end |
| Mar 13–16 | `Fixed design flow: allowing multiple accounts per customer` | Corrected account-customer ownership model — one customer can hold multiple accounts |
| Mar 17 | `Refactored AccountManager and Transaction Manager` | Separated account management and transaction ledger responsibilities; reduced coupling |
| Mar 19 | `Added try catch blocks` → `added OverdraftLimitExceededException` → `Merge PR #1` | Full exception hierarchy (7 custom exceptions), input validation, Javadoc, test suite — merged via PR #1 |


## Test Results

> [!NOTE]
> **17 tests** across `AccountTest` and `AccountServiceTest` — all passing.
> Tests ran locally via `mvn test`. The CI pipeline was scoped to Sprint 2.

Coverage focused on:
- Account creation with correct initial state
- Deposit and withdrawal with boundary values
- Exception cases: insufficient funds, closed-account operations, invalid inputs

---

## Demo Summary

By the end of Sprint 1, a bank teller could:

1. Register a new **Regular** or **Premium** customer with validated email
2. Open a **Savings** or **Checking** account with an initial deposit
3. **Deposit** funds into any active account
4. Attempt a **withdrawal** — the system enforces overdraft limits and minimum balance rules with descriptive error messages
5. Navigate a clean **7-option console menu** grouped by domain area

> [!WARNING]
> Data did not survive a restart at this stage — all state was held in memory. Persistence was deliberately deferred to Sprint 2.
