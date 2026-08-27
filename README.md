### Hi, I'm Chen Yufeiyang 👋

Undergraduate in **Cyberspace Security** at Sun Yat-sen University, working toward **Fall 2027 M.S. programs in AI Security / AI Systems**.

I make LLM and agent systems **fail loudly instead of corrupting silently** — finding and fixing trust-boundary, data-fidelity, and scoring-correctness bugs in mainstream AI/ML open source.

---

#### 🚩 Featured project: [failroute](https://github.com/feiiiiii5/failroute)

[![CI](https://github.com/feiiiiii5/failroute/actions/workflows/ci.yml/badge.svg)](https://github.com/feiiiiii5/failroute/actions/workflows/ci.yml)
[![PyPI](https://img.shields.io/pypi/v/failroute)](https://pypi.org/project/failroute/)

**Background.** While contributing correctness fixes across AI/eval codebases, I kept meeting the same defect family under different names: an LLM judge outage becoming a legitimate-looking `0.0` score, a network error becoming "no results", a red-team metric reporting success from a judge that never ran. I stopped fixing these one by one and built the detector instead. `failroute` is a static analyzer for this class — *failure-routing*: converting a failure into a success-looking outcome at the wrong layer. It targets the **semantic gap no syntactic linter covers** (`except Exception: return 0.0` is invisible to ruff/Bandit/flake8-bugbear).

- Hand-labelled benchmark corpus (labels written independently of tool output), precision = recall = 1.0, enforced in CI; `mypy --strict`; 3 OS × 5 Python versions
- Measured on 8 real AI/eval repos: 647 findings vs 80 from ruff S110/S112 — 390 in the class syntactic rules cannot express
- `pip install failroute` · SARIF / GitHub code scanning · pre-commit · `[tool.failroute]` project config
- Built with an AI-assisted, human-audited workflow: LLM proposes, deterministic gates verify, humans own every judgment call (`docs/process.md`)

#### 🤝 How I contribute to open source

These are the rules I hold myself to in every upstream interaction:

- **Evidence before report.** Every issue I file carries a failure-consequence chain ("what wrong outcome does this produce in production?") and a minimal reproduction verified against the current release.
- **One consolidated report per defect family.** Findings are grouped and deduplicated — maintainers' time is the scarce resource.
- **Findings I cannot defend don't get filed.** After auditing one well-maintained red-teaming framework, I reviewed a sample of tool findings, concluded they were intentional contracts, and filed nothing. Silence, when justified, is also a contribution.
- **Only verifiable claims.** No inflated numbers, no claims about unmerged work; anything quantitative I say should be reproducible from a public checkout.
- **Security-sensitive issues go through private disclosure channels first** (the project's SECURITY.md / private vulnerability reporting), with details published only after coordinated handling.
- **Decisions are the maintainers'.** I argue with evidence, accept outcomes gracefully, and follow up at most once politely.

#### 🛠️ Open source highlights

Merged contributions across **UK AI Safety Institute** (`inspect_ai` scoring correctness), **Microsoft** (`PyRIT` — GCG optimizer state refactor merged after 8 review rounds with the maintainer adopting my design), **NVIDIA** (`garak` detector fidelity), **Trail of Bits** (`fickling` pickle-security analyzer), and other LLM frameworks (`pydantic-ai`, `uqlm`, `llama_index`, `Unstructured`).

#### 📊 Focus areas

- Correctness of AI evaluation & red-teaming toolchains (silent failures, score integrity)
- Trust boundaries in LLM/agent frameworks (MCP, instruction routing)
- Static analysis & AI-assisted development workflows with verifiable quality gates

#### 📫 Contact

- Email: fei76161@gmail.com
- Application-relevant CV available on request
