# Sprint 2 — Final Retrospective

**Sprint dates:** Mar 25 – Apr 2, 2026

---

## Process Improvements Applied from Sprint 1

The Sprint 1 retrospective identified three specific action items. Here is how each was addressed:

| Sprint 1 Action | Applied in Sprint 2? | Evidence |
|---|---|---|
| One concern per commit | ✓ Yes | Sprint 2 commits are focused: `added FilePersistenceService`, `added ValidationUtils`, `added synchronized updateBalance` — each targets a single behaviour |
| Agree the data model before coding | ✓ Yes | The collections migration was planned before Sprint 2 began; no mid-sprint architectural reversals occurred |
| Set up CI at the start of Sprint 2 | Partially | CI was configured during Sprint 2, though as a dedicated story (US-08) rather than a day-one step |

---

## What Went Well

**1. Incremental feature layering**  
Sprint 2 features built cleanly on top of Sprint 1 foundations without breaking existing behaviour. File persistence, for example, required adding `Serializable` to existing model classes — a small, targeted change that did not force any restructuring of the service layer. This validates the benefit of the Sprint 1 SSOT refactor: a well-structured codebase absorbs new requirements with low friction.

**2. Thread safety handled correctly**  
Introducing concurrency late in a project is typically risky — shared mutable state that worked in a single-threaded context often breaks under concurrent access. The decision to use `Collections.synchronizedList` and `synchronized` methods in `TransactionManager`, combined with `synchronized updateBalance` in the account layer, produced a solution that is both correct and easy to reason about. The concurrent simulation confirmed the approach under load.

**3. CI pipeline as a safety net**  
Once the GitHub Actions pipeline was live, it caught a late-stage code review issue (`fix: resolve remaining code-review gaps`, Apr 1) before it was merged. This is exactly the value proposition of CI: shifting defect detection left, from "discovered in production" to "blocked at the PR gate."

---

## What to Improve

**1. CI should be live from Sprint 1, not Sprint 2**  
The most honest lesson from this project is that the CI pipeline was a Sprint 2 deliverable when it should have been infrastructure set up in Sprint 0. Running tests locally for an entire sprint and only automating them in the final sprint inverts the purpose of CI. In future projects, the pipeline will be the first thing configured — before any feature code is written.

**2. Javadoc was batch-written at the end**  
Six consecutive `docs: add Javadocs` commits on Apr 1 indicate that documentation was accumulated and written in one session rather than alongside each feature. While the result is complete and accurate, this approach creates a documentation debt that has to be paid back before a merge. In future sprints, Javadoc will be part of the Definition of Done enforced per commit, not per PR.

---

## Key Lessons Learned

- **Agile is about feedback loops, not just cadence.** The most impactful practice was the retrospective action item on commit granularity. A small process adjustment from Sprint 1 produced a noticeably cleaner Sprint 2 commit history — demonstrating that retrospectives only have value when their outputs are actually applied.

- **Architecture decisions made late are expensive.** The SSOT refactor in Sprint 1 was necessary but disruptive. Planning the data model upfront — even for a small system — reduces mid-sprint context switching and preserves the team's ability to deliver consistently.

- **Infrastructure is not optional.** CI, logging, and persistence are easy to defer and easy to regret. Each of them became a first-class delivery item in Sprint 2 precisely because they were deferred from Sprint 1. Future project plans will treat them as Sprint 0 tasks.
