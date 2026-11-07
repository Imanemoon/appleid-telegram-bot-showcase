# Testing & Quality

Only verified indicators are presented here. Every number below was recomputed
from the project as of **November 7, 2026**; where a result could not be
independently verified, it is not claimed.

## Scale

| Indicator | Value | Method |
|---|---:|---|
| Test files | 538 | Tracked files matching `test_*.py` |
| Production Python files | 191 | Tracked non-test `.py` files |
| Test functions | 7,193 | Occurrences of `def test_` across tracked test files |
| Test code size | 175,328 lines | Physical lines across all tracked test files |
| Production code size | 179,373 lines | Physical lines across all tracked non-test Python files |

The test code is roughly the same size as the production code — the project
treats tests as a first-class deliverable, not an afterthought.

## Test strategy

- **Unit tests.** Pure logic — parsers, pricing math, scrubbing/redaction
  utilities, state transitions — tested without infrastructure.
- **Integration tests.** Workflow orchestration and subsystem interaction,
  including conversation flows and handler wiring.
- **Database-backed suites.** The highest-risk invariants get dedicated
  suites: payment integrity, inventory reservation/lease semantics, backup
  retention, and post-restore validation.
- **Regression witnesses.** Bug fixes land with tests that reproduce the
  original defect first (the pre-fix behavior is kept as an explicit witness),
  including mutation-style variants for tricky paths.
- **Bench harnesses.** Repeatable instrumented scripts for performance-sensitive
  areas such as session warm-up, reporting create/navigate/retry/recreate
  metrics rather than ad-hoc timings.

## Continuous integration

- **GitHub Actions** runs the regression gate on every push to the mainline and
  on automated branches.
- The CI subset is **self-providing**: it runs without production secrets,
  external services, or a live database, using controlled test fixtures — so
  the gate is fast, deterministic, and runnable anywhere.
- **Automated PR flow.** An automation workflow creates pull requests for
  reviewed changes and merges them only after a full CI run has passed on the
  exact head commit — no duplicate runs, no skipping: every merged commit was
  validated by a complete run of its own.
- **Latest verified result.** The most recent CI run on the mainline (November
  7, 2026) completed **successfully**.

## What is deliberately not claimed

- No claim that every possible test passes at every moment — results are
  reported only from identified, verified runs.
- No flakiness or coverage-percentage numbers are published, because none were
  independently measured for this showcase.
- Bench and PR-reported performance numbers are labeled as reported claims, not
  guaranteed measurements (see
  [Engineering Highlights](ENGINEERING_HIGHLIGHTS.md)).
