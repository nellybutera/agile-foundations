# 🗂️ Sprint 0 — Planning

![Status](https://img.shields.io/badge/Status-Complete-22c55e?style=flat-square)
![Stories](https://img.shields.io/badge/Stories-9-3b82f6?style=flat-square)
![Total Points](https://img.shields.io/badge/Total_Points-26-8b5cf6?style=flat-square)
![Sprints](https://img.shields.io/badge/Execution_Sprints-2-f97316?style=flat-square)

| | |
|---|---|
| **Project** | BankVault — Console Banking System |
| **Role** | Apprentice Software Developer |
| **Organisation** | Amalitech Apprenticeship Programme |

---

## 🎯 Product Vision

> **BankVault** is a console-based banking platform that enables bank tellers to manage customers, accounts, and financial transactions in real time — built to demonstrate clean object-oriented architecture, robust error handling, and iterative delivery using Agile and DevOps practices.

The system is intentionally scoped as a CLI prototype: the goal is correctness of domain logic, observability of delivery cadence, and rigour in testing — not UI sophistication.

---

## 📌 Foundation Note

> [!NOTE]
> This project builds on a base scaffold provided through the Amalitech apprenticeship programme (`AT-Apprenticeship/bank-management-system`). The scaffold established the initial project skeleton and early class structure. All feature development, refactoring, testing, persistence, concurrency, CI integration, and monitoring described in Sprints 1 and 2 were individually authored as iterative delivery on top of that foundation — reflecting how professional developers operate: inheriting a codebase and delivering incrementally within it.

---

## 📋 Product Backlog

| ID | User Story | Priority | Points | Sprint |
|---|---|:---:|:---:|:---:|
| `US-01` | As a bank teller, I can register a new customer with name, age, contact, email, and address so that they are enrolled in the system | 🔴 High | 3 | Sprint 1 |
| `US-02` | As a customer, I can open a Savings or Checking account with an initial deposit so that I can store and manage my funds | 🔴 High | 3 | Sprint 1 |
| `US-03` | As a customer, I can deposit funds into my account so that my balance increases correctly | 🔴 High | 2 | Sprint 1 |
| `US-04` | As a customer, I can withdraw funds within allowed limits so that I can access my money | 🔴 High | 3 | Sprint 1 |
| `US-05` | As a customer, I can transfer funds between two accounts so that I can redistribute my money without manual steps | 🟡 Medium | 3 | Sprint 2 |
| `US-06` | As a customer, I can generate a formatted account statement showing my full transaction history | 🟡 Medium | 2 | Sprint 2 |
| `US-07` | As the system, I can persist all account and transaction data to disk so that no data is lost on restart | 🔴 High | 5 | Sprint 2 |
| `US-08` | As a developer, I can trigger the full test suite via an automated CI pipeline on every push | 🔴 High | 3 | Sprint 2 |
| `US-09` | As a bank administrator, I can see structured logs for key system events so that activity is traceable | 🟡 Medium | 2 | Sprint 2 |

> **Total estimated effort:** 26 story points &nbsp;|&nbsp; Sprint 1: 11 pts &nbsp;|&nbsp; Sprint 2: 15 pts

---

## 🔍 Acceptance Criteria

<details>
<summary><strong>US-01 — Customer Registration</strong></summary>

- The system accepts name, age, contact number, email, and address
- Email is validated against a standard format (RFC-compliant regex); invalid input is rejected with a clear message
- The customer is assigned a unique auto-generated ID (e.g. `CUST001`)
- The customer type is either `Regular` or `Premium`

</details>

<details>
<summary><strong>US-02 — Account Creation</strong></summary>

- The teller selects either Savings or Checking account type
- A Savings account enforces a minimum balance of `$500.00` and applies `3.5%` interest
- A Checking account supports an overdraft limit of `$1,000.00` and charges a `$10.00` monthly fee (waived for Premium customers)
- Each account is assigned a unique account number
- The account is linked to the customer's profile

</details>

<details>
<summary><strong>US-03 — Deposit</strong></summary>

- Only positive, non-zero amounts are accepted
- The account balance updates correctly after a successful deposit
- A transaction record (type `DEPOSIT`) is written to the ledger
- A confirmation is displayed with the updated balance

</details>

<details>
<summary><strong>US-04 — Withdrawal</strong></summary>

- Only positive, non-zero amounts are accepted
- Withdrawal is rejected if it would breach the minimum balance (Savings) or overdraft limit (Checking)
- A transaction record (type `WITHDRAWAL`) is written to the ledger
- A confirmation is displayed with the updated balance

</details>

<details>
<summary><strong>US-05 — Transfer</strong></summary>

- Both source and destination account numbers must be valid and active
- The amount is debited from the source as `TRANSFER_OUT` and credited to the destination as `TRANSFER_IN`
- The teller must confirm the transfer before it is executed
- Insufficient funds trigger an informative error; the ledger is not modified

</details>

<details>
<summary><strong>US-06 — Account Statement</strong></summary>

- The statement displays a formatted table: Transaction ID, Date/Time, Type, Amount, Balance
- Transactions can be sorted by date (newest first) or by amount (highest first)
- A summary footer shows total deposits, total withdrawals, and net change

</details>

<details>
<summary><strong>US-07 — File Persistence</strong></summary>

- Account and transaction data are written to a `data/` directory in pipe-delimited flat files
- Data is auto-loaded on application startup
- Data is auto-saved on clean application exit
- The teller can trigger a manual save at any time via the menu

</details>

<details>
<summary><strong>US-08 — CI Pipeline</strong></summary>

- A GitHub Actions workflow runs `mvn test` on every push to `main` and on every pull request
- The build fails fast if any test fails — the merge is blocked
- Surefire test reports are uploaded as build artefacts for review

</details>

<details>
<summary><strong>US-09 — Structured Logging</strong></summary>

- Key application events are logged using `java.util.logging.Logger`
- Logged events include: application start, shutdown, account creation, deposit/withdrawal, transfer, and manual save
- Transaction-level entries are logged at `FINE` level in `TransactionManager` for detailed tracing when needed

</details>

---

## ✅ Definition of Done

A backlog item is considered **Done** when **all** of the following are true:

- [x] Code compiles without errors (`mvn compile` exits 0)
- [x] All existing tests pass (`mvn test` exits 0)
- [x] The new feature has at least one corresponding unit test
- [x] All public methods have Javadoc comments
- [x] CI pipeline passes on push to `main`
- [x] No unused imports or dead code are present
- [x] The feature is reachable from the console menu (if user-facing)

---

## 🗓️ Sprint Plans

### Sprint 1 &nbsp;—&nbsp; Mar 11–19

> [!IMPORTANT]
> **Goal:** Deliver a working console application supporting customer registration, account creation, and core financial transactions — backed by a validated input layer and a foundational test suite.

| Story | Description | Points |
|:---:|---|:---:|
| `US-01` | Customer registration | 3 |
| `US-02` | Account creation (Savings + Checking) | 3 |
| `US-03` | Deposit | 2 |
| `US-04` | Withdrawal | 3 |
| | **Sprint 1 total** | **11** |

**Key technical tasks:** Build domain model · implement exception hierarchy · wire input validation · write AccountTest and AccountServiceTest

---

### Sprint 2 &nbsp;—&nbsp; Mar 25–Apr 2

> [!IMPORTANT]
> **Goal:** Extend the application with persistence, inter-account transfers, statement generation, thread safety, and a live CI pipeline — applying all improvements from the Sprint 1 retrospective.

| Story | Description | Points |
|:---:|---|:---:|
| `US-05` | Account transfers | 3 |
| `US-06` | Account statements | 2 |
| `US-07` | File persistence | 5 |
| `US-08` | CI/CD pipeline | 3 |
| `US-09` | Structured logging | 2 |
| | **Sprint 2 total** | **15** |

**Key technical tasks:** Migrate arrays to collections · implement NIO file I/O · add regex validation · make TransactionManager thread-safe · set up GitHub Actions · add `java.util.logging`

---

![Sprint Lifecycle](../../assets/diagrams/sprint-lifecycle.svg)
