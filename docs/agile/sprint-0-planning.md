# Sprint 0 — Planning

**Project:** BankVault — Console Banking System  
**Role:** Apprentice Software Developer  
**Organisation:** Amalitech Apprenticeship Programme  
**Sprint Duration:** Sprints run in two-week cycles (simulated here across the development timeline)

---

## 1. Product Vision

> **BankVault** is a console-based banking platform that enables bank tellers to manage customers, accounts, and financial transactions in real time — built to demonstrate clean object-oriented architecture, robust error handling, and iterative delivery using Agile and DevOps practices.

The system is not a web application. It is intentionally scoped as a CLI prototype: the goal is correctness of domain logic, observability of delivery cadence, and rigour in testing — not UI sophistication.

---

## 2. Foundation Note

This project builds on a base scaffold provided through the Amalitech apprenticeship programme (`AT-Apprenticeship/bank-management-system`). The scaffold established the initial project skeleton and early class structure. All feature development, refactoring, testing, persistence, concurrency, CI integration, and monitoring described in Sprints 1 and 2 were implemented as iterative, individually-authored work on top of that foundation — reflecting how professional developers operate: inheriting a codebase and delivering incrementally within it.

---

## 3. Product Backlog

| ID | User Story | Priority | Story Points | Sprint |
|---|---|---|---|---|
| US-01 | As a bank teller, I can register a new customer with their name, age, contact, email, and address so that they are enrolled in the system | High | 3 | Sprint 1 |
| US-02 | As a customer, I can open a Savings or Checking account with an initial deposit so that I can store and manage my funds | High | 3 | Sprint 1 |
| US-03 | As a customer, I can deposit funds into my account so that my balance increases correctly | High | 2 | Sprint 1 |
| US-04 | As a customer, I can withdraw funds from my account within allowed limits so that I can access my money | High | 3 | Sprint 1 |
| US-05 | As a customer, I can transfer funds between two accounts so that I can redistribute my money without manual withdrawal and deposit steps | Medium | 3 | Sprint 2 |
| US-06 | As a customer, I can generate a formatted account statement showing my full transaction history so that I can review and verify my financial activity | Medium | 2 | Sprint 2 |
| US-07 | As the system, I can persist all account and transaction data to disk so that no data is lost when the application restarts | High | 5 | Sprint 2 |
| US-08 | As a developer, I can trigger the full test suite via an automated CI pipeline on every push so that regressions are caught before they reach the main branch | High | 3 | Sprint 2 |
| US-09 | As a bank administrator, I can see structured operation logs for key system events so that application activity is traceable and auditable | Medium | 2 | Sprint 2 |

**Total estimated effort:** 26 story points

---

## 4. Acceptance Criteria

### US-01 — Customer Registration
- The system accepts name, age, contact number, email, and address
- Email is validated against a standard format (RFC-compliant regex); invalid input is rejected with a clear message
- The customer is assigned a unique auto-generated ID (e.g. `CUST001`)
- The customer type is either `Regular` or `Premium`

### US-02 — Account Creation
- The teller selects either Savings or Checking account type
- A Savings account enforces a minimum balance of $500.00 and applies 3.5% interest
- A Checking account supports an overdraft limit of $1,000.00 and charges a $10.00 monthly fee (waived for Premium customers)
- Each account is assigned a unique account number
- The account is linked to the customer's profile

### US-03 — Deposit
- Only positive, non-zero amounts are accepted
- The account balance updates correctly after a successful deposit
- A transaction record (type `DEPOSIT`) is written to the ledger
- A confirmation is displayed with the updated balance

### US-04 — Withdrawal
- Only positive, non-zero amounts are accepted
- Withdrawal is rejected if it would breach the minimum balance (Savings) or overdraft limit (Checking)
- A transaction record (type `WITHDRAWAL`) is written to the ledger
- A confirmation is displayed with the updated balance

### US-05 — Transfer
- Both source and destination account numbers must be valid and active
- The amount is debited from the source as `TRANSFER_OUT` and credited to the destination as `TRANSFER_IN`
- The teller must confirm the transfer before it is executed
- Insufficient funds trigger an informative error; the ledger is not modified

### US-06 — Account Statement
- The statement displays a formatted table: Transaction ID, Date/Time, Type, Amount, Balance
- Transactions can be sorted by date (newest first) or by amount (highest first)
- A summary footer shows total deposits, total withdrawals, and net change

### US-07 — File Persistence
- Account and transaction data are written to a `data/` directory in pipe-delimited flat files
- Data is auto-loaded on application startup
- Data is auto-saved on clean application exit
- The teller can trigger a manual save at any time via the menu

### US-08 — CI Pipeline
- A GitHub Actions workflow runs `mvn test` on every push to `main` and on every pull request
- The build fails fast if any test fails — the merge is blocked
- Surefire test reports are uploaded as build artefacts for review

### US-09 — Structured Logging
- Key application events are logged using `java.util.logging.Logger`
- Logged events include: application start, application shutdown, account creation, deposit/withdrawal, transfer, and manual data save
- Transaction-level entries are logged at `FINE` level in `TransactionManager` for detailed tracing when needed

---

## 5. Definition of Done

A backlog item is considered **Done** when all of the following conditions are met:

- [ ] The feature compiles without errors (`mvn compile` exits 0)
- [ ] All existing tests pass (`mvn test` exits 0)
- [ ] The new feature has at least one corresponding unit test
- [ ] All public methods have Javadoc comments
- [ ] The CI pipeline passes on push to `main`
- [ ] No unused imports or dead code are present
- [ ] The feature is reachable from the console menu (if user-facing)

---

## 6. Sprint 1 Plan — Mar 11–19

**Sprint Goal:** Deliver a working console application that supports customer registration, account creation, and core financial transactions, backed by a validated input layer and a foundational test suite.

| Story | Description | Points |
|---|---|---|
| US-01 | Customer registration | 3 |
| US-02 | Account creation (Savings + Checking) | 3 |
| US-03 | Deposit | 2 |
| US-04 | Withdrawal | 3 |

**Sprint 1 capacity:** 11 story points  
**Key technical tasks:** Build domain model, implement exception hierarchy, wire input validation, write AccountTest and AccountServiceTest.

---

## 7. Sprint 2 Plan — Mar 25–Apr 2

**Sprint Goal:** Extend the application with persistence, inter-account transfers, statement generation, thread safety, and a live CI pipeline; apply all process improvements identified in the Sprint 1 retrospective.

| Story | Description | Points |
|---|---|---|
| US-05 | Account transfers | 3 |
| US-06 | Account statements | 2 |
| US-07 | File persistence | 5 |
| US-08 | CI/CD pipeline | 3 |
| US-09 | Structured logging | 2 |

**Sprint 2 capacity:** 15 story points  
**Key technical tasks:** Migrate arrays to collections, implement NIO file I/O, add regex validation, make TransactionManager thread-safe, set up GitHub Actions, add `java.util.logging`.

---

![Sprint Lifecycle](../../assets/diagrams/sprint-lifecycle.svg)
