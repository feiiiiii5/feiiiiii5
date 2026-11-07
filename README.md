### Hi, I'm Yufeiyang 👋

Undergraduate at Sun Yat-sen University, working on **AI evaluation and agent tooling**. I'm most interested in silent failures: an eval, judge or reward function that reports success while something underneath has broken.

- 🔧 **412 merged PRs across 87 open-source repositories** (as of 2026-11-07, [see them all](https://github.com/search?q=is%3Apr+is%3Amerged+author%3Afeiiiiii5+-user%3Afeiiiiii5&type=pullrequests)), mostly in LLM evaluation, red-teaming and observability tools
- 🧭 [Area Triager](https://github.com/truera/trulens/blob/main/MAINTAINERS.md#area-triagers) for feedback functions and metrics in **TruLens**
- 🔬 Studying how failures in reward and evaluation code turn into scores that look normal
- 🤖 I pick the problems, design the approach and review every change; AI coding agents help with implementation, tests and drafting

### Selected contributions

| Project | What changed |
|---|---|
| [Inspect Evals #2132](https://github.com/UKGovernmentBEIS/inspect_evals/pull/2132) | HLE calibration keeps individual attempts, so averaging repeated runs no longer hides confidently wrong answers |
| [Opik #8152](https://github.com/comet-ml/opik/pull/8152) | G-Eval finds the real score field and maps multi-token scores like `10` to the right log-probabilities |
| [PyRIT #3125](https://github.com/microsoft/PyRIT/pull/3125) | Metadata filters compare keys literally on SQLite and Azure SQL, so a dotted key can't match or delete the wrong records |
| [xgrammar #834](https://github.com/mlc-ai/xgrammar/pull/834) | JSON Schema `prefixItems` accept valid short arrays without letting later items skip a position |
| [Serena #2030](https://github.com/oraios/serena/pull/2030) | Pending requests fail promptly when a write to the language server fails, instead of waiting for a timeout |

Most active in: PyRIT · Opik · TruLens · Inspect · Rhesis · OpenInference · Pandera

### Projects

| | |
|---|---|
| [**rewardfail**](https://github.com/feiiiiii5/rewardfail) | How math-checker failures in RL reward code become zero rewards or batch crashes depending on where they land. Manuscript, experiments and a prototype fix |
| [**failroute**](https://github.com/feiiiiii5/failroute) | Python CLI that flags exception handlers which can hide failures behind normal-looking results, with tests and a manuscript |
| [**QuantCore**](https://github.com/feiiiiii5/QuantCore) | Local-first A-share research and backtesting workbench with a C++20 engine and zero-copy pybind11 bindings |
| [**releasefloor**](https://github.com/feiiiiii5/releasefloor) | Checks recorded runtime requirements (ELF/Mach-O, architectures) across release archives without executing them |

Both manuscripts are public and not yet peer reviewed.

### Tools

Python · C++20 · pybind11 · LLM eval frameworks (Inspect, TruLens, Opik, PyRIT)

### Say hi

Found a bug in one of my tools or want to collaborate? Open an issue or reach me on [LinkedIn](https://www.linkedin.com/in/yufeiyang-chen-a2167143b/).
