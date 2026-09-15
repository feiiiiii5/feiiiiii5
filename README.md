### Yufeiyang Chen

Undergrad studying Cyber Science and Technology at Sun Yat-sen University.

I submit patches to open-source ML and evaluation libraries, mainly around exception handling, fallback logic, and edge cases in test runners. I started contributing upstream in July 2026. If a PR or issue I file is unhelpful, noisy, or based on incorrect assumptions, please close it or leave a comment.

#### failroute

An AST-based static analyzer for Python that checks for exception handlers returning values callers cannot distinguish from successful runs. It detects six patterns: swallowed exceptions, silent constant fallbacks, masked exceptions, `contextlib.suppress` blocks, implicit `None` fall-through, and exception variables rebound inside their handlers.

`pip install failroute`

I tested it against eight pinned PyPI distributions (2,124 Python files, 524,229 lines scanned). It generated 621 candidate sites. Four standard linters (ruff, bandit, pylint, and flake8 with flake8-bugbear) together covered 255 of those.

Evaluating a labeled sample showed a low defect yield:
* In findings standard linters missed, roughly 1 in 56 was an actual bug.
* In findings standard linters already flagged, 12 in 48 were actual bugs.
* All 12 confirmed bugs were bare `except:` lines. Running `flake8 --select E722` caught all 12 across 134 total candidates, reaching the same recall with a search space roughly five times smaller.
* The benchmark labels were produced by two rounds of LLM agents without human review. A preprint covering the methodology is in preparation.

Project details:
* 221 tests on Python 3.9 through 3.13 across Linux, macOS, and Windows.
* Runs clean under `mypy --strict`, outputs SARIF for GitHub code scanning, and reports zero findings when run on its own code.
* Validated on `bench/realworld/` (87 cases anchored to the pinned corpus). The internal test fixtures share my own blind spots and are only used as regression checks.
* Uses an AI-assisted development workflow where models draft implementations, deterministic tests verify them, and manual review decides what gets merged (`docs/process.md`).

#### Upstream pull requests

| Repo / PR | Notes |
|---|---|
| [microsoft/PyRIT #2467](https://github.com/microsoft/PyRIT/pull/2467) | Refactored loop state from loose locals into explicit types (issue opened by maintainer). My initial patch used `loss = float("inf")` as a sentinel for unmeasured runs, which would hide actual numeric overflows. The maintainer caught it in review and I replaced it with an explicit boolean flag so the measurement state is clear. |
| [UKGovernmentBEIS/inspect_evals #2132](https://github.com/UKGovernmentBEIS/inspect_evals/pull/2132) | Multi-epoch calibration error in Humanity's Last Exam was being averaged across epochs before calculating calibration (issue opened by maintainer). Made a reproduction case showing this outputs 0.0 calibration error instead of 1.0 on miscalibrated answers. Fixed the multi-epoch code path, kept single-epoch outputs byte-identical, and bumped the task version. |
| [cvs-health/uqlm #459](https://github.com/cvs-health/uqlm/pull/459) | When an evaluation model ran out of retries, it returned unhandled `NaN` values that silently poisoned the aggregate score for the whole prompt while exiting cleanly. Pruned failed models from the calculation and flagged affected prompts. |
| [UKGovernmentBEIS/inspect_ai #5068](https://github.com/UKGovernmentBEIS/inspect_ai/pull/5068) | Removed a try/except that swallowed permission errors where an internal code comment indicated they should be raised. |
| [Tencent/AI-Infra-Guard #539](https://github.com/Tencent/AI-Infra-Guard/pull/539) | Fixed a directory path check that allowed sibling folders sharing the same name prefix (issue reported by another user). |

Three of the five issues above were scoped and opened by other people before I worked on them.

#### Notes on reporting bugs

I check candidate issues against actual call paths before opening tickets or PRs. For example, running failroute over PyRIT gave several dozen warnings. I stepped through twelve of them in the codebase, found that all twelve were deliberate design decisions, and filed zero issues. If an edge case does not cause a practical problem in how the software runs, I leave it alone.

Repositories on this account are primarily working forks for upstream pull requests.
