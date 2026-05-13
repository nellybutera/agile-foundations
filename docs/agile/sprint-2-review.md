# Sprint 2 — Review

![Status](https://img.shields.io/badge/Status-Complete-22c55e?style=flat-square)
![Stories](https://img.shields.io/badge/Stories_Delivered-5%2F5-22c55e?style=flat-square)
![Tests](https://img.shields.io/badge/Tests_Passing-32-3b82f6?style=flat-square)
![Points](https://img.shields.io/badge/Story_Points-15-8b5cf6?style=flat-square)
![CI](https://img.shields.io/badge/CI-Passing-22c55e?style=flat-square&logo=github-actions&logoColor=white)

| | |
|---|---|
| **Sprint dates** | Mar 25 – Apr 2, 2026 |
| **Sprint goal** | Persistence, transfers, CI pipeline, logging — with Sprint 1 process improvements applied |


## Sprint Goal Result

> [!NOTE]
> All five planned stories delivered and met the Definition of Done. The application now persists data across restarts, the CI pipeline runs on every push, and all 32 tests pass with a green build on `main`.


## Delivered Stories

| Story | Description | Status |
|:---:|---|:---:|
| `US-05` | Account transfers — `TRANSFER_OUT` / `TRANSFER_IN` ledger entries, teller confirmation flow | ✅ Done |
| `US-06` | Account statement — formatted table, sortable by date or amount, summary footer | ✅ Done |
| `US-07` | File persistence — NIO flat-file I/O, auto-load on startup, auto-save on exit, manual save | ✅ Done |
| `US-08` | GitHub Actions CI — `mvn test` on push and PR, Surefire report upload | ✅ Done |
| `US-09` | Structured logging — `java.util.logging.Logger` in `BankController` and `TransactionManager` | ✅ Done |


## Key Commits

| Date | Commit | What it delivered |
|---|---|---|
| Mar 30 | `feat: add FunctionalUtils` + `refactor: replace fixed arrays with collections` | Java Collections migration; shared stream helpers |
| Mar 31 | `added FilePersistenceService` → `autoloaded persisted data on startup` | NIO-based persistence; data survives restarts |
| Mar 31 | `added ValidationUtils` + `added email field to Customer` | Regex-backed validation using `Pattern`, `Matcher`, `Predicate` |
| Mar 31 | `added synchronized updateBalance` → `made TransactionManager thread-safe` | Race condition guards; `synchronizedList` + `synchronized addTransaction` |
| Mar 31 | `added transfer between accounts` + `added StatementGenerator` | US-05 and US-06 delivered; 3 new tests |
| Apr 1 | `docs: add Javadocs` (6 commits) | Full Javadoc coverage across all packages |
| Apr 2 | `Merge pull request #3` | All Sprint 2 work merged to `main` via code-reviewed PR |

## Test Results

| File | Tests | Coverage Focus |
|---|:---:|---|
| `AccountTest` | 8 | Core account state: balance, status, type |
| `AccountServiceTest` | 9 | Service operations: create, deposit, withdraw, transfer, fees |
| `TransactionManagerTest` | 3 | Ledger correctness: totals by type, thread-safe recording |
| `ExceptionTest` | 12 | Exception hierarchy, input validator edge cases, closed-account guards |
| **Total** | **32** | All passing — CI confirmed green on final push to `main` |


## Monitoring Evidence

Structured logging added via `java.util.logging.Logger`:

| Logger | Level | Events Logged |
|---|:---:|---|
| `BankController` | `INFO` | App start, shutdown, account created, deposit/withdrawal, transfer, manual save |
| `TransactionManager` | `FINE` | Every ledger entry (account, type, amount) — for detailed tracing when enabled |

**Sample output (`INFO` level):**

```
INFO: BankVault application started
INFO: Account created: number=ACC001 customer=Jane Doe type=Savings
INFO: Transaction completed: account=ACC001 type=DEPOSIT amount=1500.00
INFO: Transfer completed: from=ACC001 to=ACC002 amount=300.00
INFO: BankVault shutdown — data auto-saved to disk
```


## Demo Summary

By the end of Sprint 2, a bank teller could:

1. Start the application and have all **previously saved data auto-loaded** from disk
2. Register customers with **email validation** enforced at entry
3. Open accounts, deposit, withdraw, and **transfer between accounts**
4. Generate a formatted **account statement** sortable by date or amount
5. Run a **concurrent transaction simulation** demonstrating thread-safe balance updates
6. Exit knowing all data was **auto-saved** — no manual step required


![CI/CD Pipeline](../../assets/diagrams/cicd-pipeline.svg)
