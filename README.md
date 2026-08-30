### Hi, I'm Yufeiyang Chen 👋

Undergraduate in **Cyberspace Security** at Sun Yat-sen University.

I work on one defect family across LLM and agent systems: **a failure being converted into a
success-looking result at the wrong layer**. An LLM judge that never ran becoming a legitimate
`0.0` score. A network error becoming "no results". A red-team report that comes back clean
because the scorer silently died. Nothing crashes, nothing is logged, and every conclusion
built on top is wrong.

---

#### 🚩 failroute — a detector for that class

[![CI](https://github.com/feiiiiii5/failroute/actions/workflows/ci.yml/badge.svg)](https://github.com/feiiiiii5/failroute/actions/workflows/ci.yml)
[![PyPI](https://img.shields.io/pypi/v/failroute)](https://pypi.org/project/failroute/)

After fixing enough of these one at a time upstream, I stopped patching instances and tried to
name the category. `failroute` is a static analyzer for **failure-routing**, and it targets a gap
no syntactic linter covers by construction — `except Exception: return 0.0` is invisible to ruff,
Bandit and flake8-bugbear, and ruff's own `SIM105` actively recommends rewriting
`try/except/pass` into `contextlib.suppress(...)`, which is semantically identical and invisible
to every shipped linter afterwards.

Six detectors: swallowed exceptions, silent constant fallbacks, masked exceptions,
`contextlib.suppress` blind spots, handlers falling through to an implicit `None`, and exception
variables rebound inside their own handler.

- **Hand-labelled corpus of 68 samples** (36 positive / 32 negative), annotated independently of
  the tool's output; detectors held to precision = recall = 1.0 in CI
- **124 tests** across 3 operating systems × 5 Python versions; `mypy --strict`; the analyzer scans
  its own source with zero findings
- **Measured on 8 real AI/eval repositories**: 670 findings where ruff's `S110`/`S112` report 79,
  with an overlap of 70 — 449 of them in the semantic family syntactic rules cannot express
- `pip install failroute` · SARIF output / GitHub code scanning · pre-commit hook ·
  `[tool.failroute]` project configuration
- Built with an AI-assisted, human-audited workflow: the model proposes, deterministic gates
  verify, and a person owns every judgment call ([`docs/process.md`](https://github.com/feiiiiii5/failroute/blob/main/docs/process.md))

#### 🤝 How I work upstream

These are the rules I hold myself to, and the reason I file less than I find:

- **Evidence before report.** Every issue carries a failure-consequence chain — *what wrong
  outcome does this produce in production?* — plus a minimal reproduction against the current release.
- **One consolidated report per defect family.** Findings get grouped and deduplicated.
  A maintainer's attention is the scarce resource, not my output.
- **Findings I cannot defend don't get filed.** Running my own analyzer over a well-maintained
  red-teaming framework produced 65 semantic-level findings. I sampled twelve, traced each one,
  concluded all twelve were deliberate design contracts, and filed none of them. A tool can
  propose; only a person can argue that a particular failure matters.
- **Only verifiable claims.** No inflated numbers, no claims about unmerged work. Anything
  quantitative here is reproducible from a public checkout.
- **Security-sensitive findings go through private channels first** — a project's `SECURITY.md`
  or private vulnerability reporting — with details withheld until coordinated handling completes.
- **The decision is the maintainer's.** I argue with evidence, accept the outcome, and follow up
  at most once, politely.

#### 🛠️ Selected upstream work

Merged correctness fixes across 20+ AI/ML projects, including:

| Project | Organisation | What it fixed |
|---|---|---|
| [`PyRIT`](https://github.com/microsoft/PyRIT) | Microsoft | Made the GCG optimizer's implicit cross-iteration invariants explicit and typed — merged after **eight review rounds**, with the maintainer adopting my design rather than rewriting it |
| [`inspect_ai`](https://github.com/UKGovernmentBEIS/inspect_ai) · [`inspect_evals`](https://github.com/UKGovernmentBEIS/inspect_evals) | UK AI Security Institute | Scoring-correctness defects in an evaluation framework: a scorer reporting a calibration error of `0.0` at a ground truth of `1.0`, graders bypassed without a signal, retry errors hiding their real cause |
| [`uqlm`](https://github.com/cvs-health/uqlm) | CVS Health | A single judge exhausting its retries turned the whole panel's statistics into `NaN` while the run still reported success |
| [`fickling`](https://github.com/trailofbits/fickling) | Trail of Bits | Malformed pickle input raising a bare exception instead of failing clearly (CWE-502) |
| [`garak`](https://github.com/NVIDIA/garak) | NVIDIA | Detector fidelity and honest confidence intervals when the bootstrap degenerates |
| [`pandera`](https://github.com/unionai-oss/pandera) · [`pydantic-ai`](https://github.com/pydantic/pydantic-ai) · [`outlines`](https://github.com/dottxt-ai/outlines) | — | Data-contract and structured-generation correctness |

I also reported a deserialization trust-boundary issue in PyTorch's distributed-checkpoint reader
through GitHub's private security-advisory channel; the advisory is currently under triage.

#### 📊 What I'm interested in

- Correctness of AI evaluation and red-teaming toolchains — silent failures, score integrity
- Trust boundaries in LLM and agent frameworks
- Static analysis for semantic defect classes, and development workflows with verifiable quality gates

#### 📫 Contact

fei76161@gmail.com
