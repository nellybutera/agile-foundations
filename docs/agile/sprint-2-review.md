# Sprint 2 Review

**Sprint dates:** Mar 25 – Apr 2, 2026  
**Sprint goal:** Extend the application with persistence, transfers, statement generation, thread safety, and a live CI pipeline — applying all process improvements from the Sprint 1 retrospective.

---

## Delivered Stories

| Story | Description | Status | Tests Added |
|---|---|---|---|
| US-05 | Account transfers — `TRANSFER_OUT` / `TRANSFER_IN` ledger entries, teller confirmation flow | ✓ Done | `TransactionManagerTest` (+3 tests) |
| US-06 | Account statement generation — formatted table, sortable by date or amount, summary footer | ✓ Done | `AccountServiceTest` |
| US-07 | File persistence — NIO flat-file I/O, auto-load on startup, auto-save on exit, manual save option | ✓ Done | — |
| US-08 | GitHub Actions CI — `mvn test` on push and PR, Surefire report upload | ✓ Done | Pipeline itself |
| US-09 | Structured logging — `java.util.logging.Logger` in `BankController` and `TransactionManager` | ✓ Done | — |

All five stories met the Definition of Done.

---

## Key Commits

| Date | Commit | What it delivered |
|---|---|---|
| Mar 30 | `feat: add FunctionalUtils` + `refactor: replace fixed arrays with collections` | Java Collections API migration (ArrayList, HashMap, stream operations); FunctionalUtils for shared stream helpers |
| Mar 31 | `added FilePersistenceService` → `autoloaded persisted data on startup` | NIO-based flat-file persistence; accounts and transactions survive application restarts |
| Mar 31 | `added ValidationUtils` + `added email field to Customer` | Regex-backed input validation using `Pattern`, `Matcher`, and `Predicate`; email validation wired into registration |
| Mar 31 | `added synchronized updateBalance` → `made TransactionManager thread-safe` | Race condition guards; `synchronizedList` + `synchronized addTransaction` prevent ledger corruption under concurrent access |
| Mar 31 | `added transfer between accounts` + `added StatementGenerator` | US-05 and US-06 delivered; 3 new tests |
| Apr 1 | `docs: add Javadocs to *` (6 commits) | Full Javadoc coverage across all packages |
| Apr 2 | `Merge pull request #3` | All Sprint 2 work merged to `main` via code-reviewed PR |

---

## Test Results

**Test suite at end of Sprint 2:** 32 tests across 4 files

| File | Tests | Focus |
|---|---|---|
| `AccountTest` | 8 | Core account state: balance, status, type |
| `AccountServiceTest` | 9 | Service-layer operations: create, deposit, withdraw, transfer, fees |
| `TransactionManagerTest` | 3 | Ledger correctness: deposit totals, withdrawal totals, transfer records |
| `ExceptionTest` | 12 | Exception hierarchy, input validator edge cases, closed-account guards |

All 32 tests passed. The CI pipeline confirmed a green build on the final push to `main`.

---

## Monitoring Evidence

Structured logging was added to `BankController` and `TransactionManager` using `java.util.logging.Logger`:

| Logger | Level | Event logged |
|---|---|---|
| `BankController` | `INFO` | Application start, shutdown, account created, deposit/withdrawal completed, transfer completed, manual save |
| `TransactionManager` | `FINE` | Every ledger entry (account number, type, amount) — available when `FINE` logging is enabled |

Sample log output (INFO level):
```
INFO: BankVault application started
INFO: Account created: number=ACC001 customer=Jane Doe type=Savings
INFO: Transaction completed: account=ACC001 type=DEPOSIT amount=1500.00
INFO: Transfer completed: from=ACC001 to=ACC002 amount=300.00
INFO: BankVault shutdown — data auto-saved to disk
```

---

## Demo Summary

By the end of Sprint 2, a bank teller could:

1. Start the application and have all previously saved data automatically loaded from disk
2. Register customers with email validation enforced at entry
3. Open Savings or Checking accounts, deposit, withdraw, and transfer between accounts
4. Generate a formatted account statement sortable by date or amount
5. Run a concurrent transaction simulation demonstrating thread-safe balance updates
6. Exit knowing all data has been auto-saved — no manual step required

The CI pipeline ran all 32 tests on every push and blocked merges on failure. The application logs key events at runtime for operational traceability.

---

![CI/CD Pipeline](../../assets/diagrams/cicd-pipeline.svg)
