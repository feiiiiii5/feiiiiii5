### Hi, I'm Yufeiyang Chen 👋

Undergraduate in **Cyber Science and Technology** at Sun Yat-sen University.

I work on one defect family across LLM and agent systems: **a failure being converted into a
success-looking result at the wrong layer**. A judge model that never ran becoming a legitimate
`0.0` score. A retry budget running out and the exhaustion being reported as an answer. A path
check that accepts `/tmp/scan/skill-evil` because the allowed directory is `/tmp/scan/skill`.
Nothing crashes, nothing is logged, and every conclusion built on top is wrong.

**91 merged pull requests across 31 AI/ML projects.** Most of my work lives in other people's
repositories; the table below is the part worth reading.

---

#### 🛠️ Merged upstream

| Project | ★ | What the change does |
|---|---:|---|
| [`modelcontextprotocol/servers#4662`](https://github.com/modelcontextprotocol/servers/pull/4662) | 90.3k | The memory server registered `search_nodes` with an unbounded `query`, so an oversized query still forced a full O(graph) scan over every entity name, type and observation for no retrieval value. Adds a length cap enforced by an exported schema, so the constraint is testable on its own. |
| [`run-llama/llama_index#22527`](https://github.com/run-llama/llama_index/pull/22527) | 52.1k | An empty embedding payload — which application code produces naturally, e.g. `"   ".split()` — was sent to AWS and came back as `ValidationException: Invalid parameter combination`, pointing operators at credentials and region config rather than at the empty list. Now rejected locally, before the call, on the shared gate for both the sync and async paths. |
| [`EleutherAI/lm-evaluation-harness#4039`](https://github.com/EleutherAI/lm-evaluation-harness/pull/4039) | 14.0k | The thousands-separator rule in answer normalisation fused bare digit tuples: gold `"0,1"` became `"01"`, so a model answering `(0,1)` was marked wrong. Twelve MATH gold answers were corrupted this way. |
| [`Tencent/AI-Infra-Guard#539`](https://github.com/Tencent/AI-Infra-Guard/pull/539) | 6.3k | Agent file tools used `str.startswith(base_dir)` for path containment, so `/tmp/scan/skill-evil/secrets.txt` passed a check meant to confine access to `/tmp/scan/skill` — a prompt-injected `SKILL.md` could read and write outside the sandbox. Replaced with `os.path.commonpath`. The maintainer merged it as *"this important security fix … a real prompt-injection attack vector."* |
| [`microsoft/PyRIT#2467`](https://github.com/microsoft/PyRIT/pull/2467) | 4.5k | Made the GCG optimizer's implicit cross-iteration invariants explicit and typed. The core maintainer opened **eight independent review threads** across 21 inline comments — including one where my own assertion used `inf` as a sentinel for "not updated", which would have misfired on a legitimately infinite loss. The implementation that shipped is mine. |
| [`UKGovernmentBEIS/inspect_ai#4906`](https://github.com/UKGovernmentBEIS/inspect_ai/pull/4906) | 2.8k | When remote exec exhausted its retries the sandbox's own error was discarded and a bare `RetryError` surfaced instead, hiding why the sandbox failed. Reports the underlying error. Merged after a full review cycle: changes requested, revised, approved. |
| [`UKGovernmentBEIS/inspect_evals#2132`](https://github.com/UKGovernmentBEIS/inspect_evals/pull/2132) | 0.7k | Over repeated epochs the calibration-error metric averaged attempts before scoring, so confidently-wrong and unconfidently-right answers cancelled out. A run where every attempt was maximally miscalibrated reported `cerr = 0.0`; the attempt-level truth was `1.0`. No exception, no warning. |
| [`cvs-health/uqlm#459`](https://github.com/cvs-health/uqlm/pull/459) | 1.2k | One LLM judge exhausting its retries left a `NaN` that plain `np.mean/max/min/median` propagated into **every** panel statistic for that prompt, while the run reported success. A panel exists so that one judge can fail without spoiling the result. |

Also merged into Trail of Bits `fickling`, `pydantic-ai`, `xgrammar`, `qdrant-client`, `pandera`,
`vllm`, `letta`, `griptape`, `openlit` and others — static-analysis false positives, data-contract
and structured-generation correctness, local/server semantic parity.

The pattern is always the same shape: find the layer where a failure stops being visible, then
make it visible again without changing the behaviour anyone depends on.

---

#### 🚩 failroute — a detector for that class

[![CI](https://github.com/feiiiiii5/failroute/actions/workflows/ci.yml/badge.svg)](https://github.com/feiiiiii5/failroute/actions/workflows/ci.yml)
[![PyPI](https://img.shields.io/pypi/v/failroute)](https://pypi.org/project/failroute/)

After fixing enough of these one at a time upstream, I stopped patching instances and tried to
name the category. `failroute` is a static analyser for **failure-routing**, targeting a gap no
syntactic linter covers by construction: `except Exception: return 0.0` is invisible to ruff,
Bandit and flake8-bugbear, and ruff's own `SIM105` actively recommends rewriting `try/except/pass`
into `contextlib.suppress(...)` — semantically identical, and invisible to every shipped linter
afterwards.

**Measured on 8 pinned PyPI releases** (2,124 `.py` files, 524,229 lines), paper frame `v0.8.0`:

- **621 findings.** The union of four established linters (ruff, Bandit, pylint, flake8-bugbear)
  co-locates with **255 of them — 41.1%**, leaving 366 that none of them reach. All 255 come from
  pylint alone; the other three add nothing on top of it.
- **The headline result is negative, and it is the reason the project is worth reading.** On a
  sample of 80 findings, **80% turned out to be deliberate design contracts** and only **15%**
  were real defects. A syntactic layer cannot tell an intentional degradation from a bug — and
  neither, it turns out, can mine.
- **The cheapest baseline nearly matches it.** `flake8 --select E722` yields 134 candidates, of
  which 9.0% are labelled defects — and **all twelve confirmed defects are inside that set**.
  Reading 134 sites gets you what reading 621 gets you.
- The labels are weak by construction: two LLM rounds agreed 80/80, which is evidence of shared
  bias, not of reliability. Both label sets are committed so the agreement can be checked item
  by item.

Engineering: **221 tests** across 3 OS × Python 3.9–3.13, `mypy --strict` clean, SARIF output
wired into GitHub code scanning, and the analyser scans its own source with zero findings. The
gate that actually has external validity is `bench/realworld/` — 87 cases anchored to real
coordinates in the pinned corpus, including the 80 human-labelled findings behind the paper. The
internal fixture corpus is a regression gate only: it was written by the same person as the
detector, with the same blind spot, and the repository says so. `pip install failroute`.

Built with an AI-assisted, human-audited workflow: the model proposes, deterministic gates verify,
and a person owns every judgment call
([`docs/process.md`](https://github.com/feiiiiii5/failroute/blob/main/docs/process.md)).

A preprint with the full methodology is in preparation.

---

#### 🤝 How I work upstream

- **Evidence before report.** Every issue carries a failure-consequence chain — *what wrong
  outcome does this produce in production?* — plus a minimal reproduction against the current release.
- **Findings I cannot defend don't get filed.** Running my own analyser over a well-maintained
  red-teaming framework produced 65 semantic-level findings. I sampled twelve, traced each one,
  concluded all twelve were deliberate design contracts, and filed none. A tool can propose;
  only a person can argue that a particular failure matters.
- **One consolidated report per defect family.** Findings get grouped and deduplicated. A
  maintainer's attention is the scarce resource, not my output.
- **Only verifiable claims.** No inflated numbers, no claims about unmerged work. Anything
  quantitative here is reproducible from a public checkout.
- **The decision is the maintainer's.** I argue with evidence, accept the outcome, and follow up
  at most once, politely. Security-sensitive findings go through a project's `SECURITY.md` or
  private vulnerability reporting first, with details withheld until coordinated handling completes.

*Most repositories on this profile are working forks used to prepare upstream patches; the merged
work lives in the links above.*
