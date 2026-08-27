### Hi, I'm Yufeiyang 👋

Undergraduate in **Cyberspace Security** at Sun Yat-sen University, working toward **Fall 2027 M.S. programs in AI Security / AI Systems**.

I make LLM and agent systems **fail loudly instead of corrupting silently** — finding and fixing trust-boundary, data-fidelity, and scoring-correctness bugs in mainstream AI/ML open source.

---

#### 🚩 Featured project: [failroute](https://github.com/feiiiiii5/failroute)

[![CI](https://github.com/feiiiiii5/failroute/actions/workflows/ci.yml/badge.svg)](https://github.com/feiiiiii5/failroute/actions/workflows/ci.yml)
[![PyPI](https://img.shields.io/pypi/v/failroute)](https://pypi.org/project/failroute/)

A static analyzer for **failure-routing** — the defect family where a failure is converted into a success-looking outcome at the wrong layer (a judge outage becoming a `0.0` score, a network error becoming "no results"). Built from patterns I kept fixing across AI/eval codebases; it detects the **semantic gap no syntactic linter covers** (`except Exception: return 0.0` is invisible to ruff/Bandit/flake8-bugbear).

- Hand-labelled benchmark corpus, precision = recall = 1.0, enforced in CI
- Measured on 8 real AI/eval repos: 647 findings vs 80 from ruff S110/S112 — 390 in the class syntactic rules cannot express
- `pip install failroute` · SARIF / GitHub code scanning · pre-commit · `[tool.failroute]` config
- Developed with an AI-assisted, human-audited workflow: LLM proposes, deterministic gates verify, humans own triage (`docs/process.md`)

#### 🛠️ Open source highlights

Merged contributions across **UK AI Safety Institute** (`inspect_ai` scoring correctness), **Microsoft** (`PyRIT` — GCG optimizer state refactor merged after 8 review rounds with the maintainer adopting my design), **NVIDIA** (`garak` detector fidelity), **Trail of Bits** (`fickling` pickle-security analyzer), and other LLM frameworks (`pydantic-ai`, `uqlm`, `llama_index`, `Unstructured`).

#### 📊 Focus areas

- Correctness of AI evaluation & red-teaming toolchains (silent failures, score integrity)
- Trust boundaries in LLM/agent frameworks (MCP, instruction routing)
- Static analysis & AI-assisted development workflows with verifiable quality gates

#### 📫 Contact

- Email: fei76161@gmail.com
- Application-relevant CV available on request
