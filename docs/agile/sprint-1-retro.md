# Sprint 1 — Retrospective

![Sprint](https://img.shields.io/badge/Sprint-1-22c55e?style=flat-square)
![Date](https://img.shields.io/badge/Date-Mar_11–19_2026-6b7280?style=flat-square)


## What Went Well

### 1. Consistent, incremental delivery
The commit history reflects genuine day-by-day progress — no large end-of-sprint dumps. Each commit added a discrete, named capability: customer classes, exception classes, the bank layer, the main class. This cadence made it straightforward to identify exactly when each feature was introduced and to isolate regressions.

### 2. Designing the exception framework early
Defining a custom exception hierarchy (`InsufficientFundsException`, `OverdraftLimitExceededException`, `AccountNotFoundException`, etc.) before wiring up the controller paid dividends. When error paths were needed in `BankController`, the vocabulary already existed — no ad-hoc `RuntimeException` throwing, no retrofitting later.

---

## What to Improve

### 1. Early commits mixed too many concerns
Several commits in the first two days bundled domain classes, service logic, and controller code into a single change. The `added remaining account classes and java classes from the target folder` commit, for example, introduced multiple classes at once.

> [!TIP]
> In Sprint 2, commits will target a single behaviour — one feature or one refactor per commit.

### 2. The initial architecture needed a mid-sprint correction
The `Refactored banking architecture for Single Source of Truth` commit (Mar 12) and the `Refactored AccountManager and Transaction Manager` commit (Mar 17) indicate the original design was not fully reasoned before coding started. Two separate refactor passes in the same sprint is a signal that architecture decisions should happen in Sprint 0, not emerge reactively.

> [!TIP]
> In Sprint 2, the data model will be agreed upfront before any feature code is written.


## Action Items for Sprint 2

| # | Action | Why |
|:---:|---|---|
| 1 | One concern per commit — no bundling of unrelated changes | Reduces review noise and makes history self-documenting |
| 2 | Agree the data model before writing any Sprint 2 feature code | Prevents mid-sprint refactor loops |
| 3 | Set up GitHub Actions CI at the **start** of Sprint 2, not the end | Ensures tests run automatically from the first Sprint 2 push |
