# 🔁 Sprint 2 — Final Retrospective

![Sprint](https://img.shields.io/badge/Sprint-2-f97316?style=flat-square)
![Date](https://img.shields.io/badge/Date-Mar_25–Apr_2_2026-6b7280?style=flat-square)
![Final](https://img.shields.io/badge/Final_Retrospective-✓-8b5cf6?style=flat-square)

---

## 📋 Process Improvements Applied from Sprint 1

| Sprint 1 Action | Applied? | Evidence |
|---|:---:|---|
| One concern per commit | ✅ Yes | Sprint 2 commits are focused: `added FilePersistenceService`, `added ValidationUtils`, `added synchronized updateBalance` — each targets a single behaviour |
| Agree data model before coding | ✅ Yes | Collections migration was planned before Sprint 2; no mid-sprint architectural reversals occurred |
| Set up CI at the start of Sprint 2 | ⚠️ Partially | CI was configured as a dedicated story (US-08), though not as a day-one infrastructure step |

---

## ✅ What Went Well

### 1. Incremental feature layering
Sprint 2 features built cleanly on top of Sprint 1 foundations without breaking existing behaviour. File persistence required adding `Serializable` to existing model classes — a small, targeted change that did not force any restructuring of the service layer. This validates the benefit of the Sprint 1 SSOT refactor: a well-structured codebase absorbs new requirements with low friction.

### 2. Thread safety handled correctly
Introducing concurrency late in a project is typically risky. Using `Collections.synchronizedList` and `synchronized` methods in `TransactionManager`, combined with `synchronized updateBalance` in the account layer, produced a solution that is both correct and easy to reason about. The concurrent simulation confirmed the approach under load.

### 3. CI pipeline as a safety net
Once GitHub Actions was live, it caught a late-stage code review issue (`fix: resolve remaining code-review gaps`, Apr 1) before it was merged. This is the value proposition of CI: shifting defect detection left — from discovered in production to **blocked at the PR gate**.

---

## ⚠️ What to Improve

### 1. CI should be infrastructure, not a story
The most honest lesson: the CI pipeline was a Sprint 2 story when it should have been Sprint 0 infrastructure. Running tests locally for an entire sprint and only automating them at the end inverts the purpose of CI.

> [!IMPORTANT]
> In future projects, the pipeline will be the **first thing configured** — before any feature code is written.

### 2. Javadoc was batch-written at the end
Six consecutive `docs: add Javadocs` commits on Apr 1 indicate documentation was written in one session rather than alongside each feature. This creates debt that must be paid back before a merge.

> [!TIP]
> Javadoc should be part of the **Definition of Done enforced per commit**, not per PR.

---

## 💡 Key Lessons Learned

> [!NOTE]
> **Agile is about feedback loops, not just cadence.** The most impactful practice was the retrospective action item on commit granularity — a small process adjustment from Sprint 1 produced a noticeably cleaner Sprint 2 history. Retrospectives only have value when their outputs are actually applied.

> [!NOTE]
> **Architecture decisions made late are expensive.** The SSOT refactor in Sprint 1 was necessary but disruptive. Planning the data model upfront — even for a small system — reduces mid-sprint context switching and preserves delivery consistency.

> [!NOTE]
> **Infrastructure is not optional.** CI, logging, and persistence are easy to defer and easy to regret. Each became a first-class delivery item in Sprint 2 precisely because they were deferred from Sprint 1. Future plans will treat them as Sprint 0 tasks.
