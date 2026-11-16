### Hi, I'm Fei

I am an independent developer and open-source contributor focusing on AI evaluation, red-teaming, and agent tooling. I also study Cyber Science and Technology at Sun Yat-sen University.

My primary research and engineering interest is **silent failures in evaluation pipelines**—cases where an eval harness, LLM judge, or RL reward function hits an underlying fault but still returns a plausible, normal-looking score.

* **Open Source:** [412 merged PRs across 87 repositories](YOUR_LINK_HERE) (as of Nov 2025), primarily across LLM evaluation, observability, and structured generation.
* **Maintainer / Reviewer:** Area Reviewer for feedback functions and metrics in [TruLens](https://github.com/truera/trulens).
* **Active Ecosystems:** PyRIT · Opik · TruLens · Inspect · Rhesis · OpenInference · Pandera

---

### Selected Contributions

| PR | Impact & Mechanism |
| :--- | :--- |
| **[Inspect Evals #2132](LINK)** | Preserved individual attempt outcomes in HLE calibration so averaging repeated runs no longer masks high-confidence incorrect answers. |
| **[Opik #8152](LINK)** | Fixed G-Eval score field resolution and mapped multi-token scores (e.g., `10`) to their correct log-probabilities. |
| **[PyRIT #3125](LINK)** | Enforced literal key comparisons for metadata filters on SQLite and Azure SQL, preventing dotted keys from matching or deleting unintended records. |
| **[xgrammar #834](LINK)** | Allowed valid short arrays in JSON Schema `prefixItems` without permitting subsequent items to skip positional validation. |
| **[Serena #2030](LINK)** | Made pending requests fail immediately upon language server write errors instead of hanging until timeout. |

> **Note on workflow:** I use coding agents in my development loop. I manually triage issues, define acceptance criteria, verify root causes, and rigorously audit and test all generated patches before submitting PRs and addressing maintainer review.

---

### Research & Projects

**Silent Failures & Reliability**
* **[rewardfail](LINK)** — Empirical study and prototype fix on how math-checker failures in RL reward code silently degrade into zero rewards or batch crashes depending on exception boundaries. *(Code, experiments & non-peer-reviewed preprint)*
* **[failroute](LINK)** — Static analysis CLI for Python that flags exception handlers capable of masking runtime failures behind normal-looking return values. *(Tooling & non-peer-reviewed preprint)*

**Systems & Tooling**
* **[QuantCore](LINK)** — Local-first A-share research and backtesting workbench powered by a C++20 execution engine and zero-copy `pybind11` bindings.
* **[releasefloor](LINK)** — Static inspector that verifies recorded runtime requirements (ELF/Mach-O headers, target architectures) across release archives without binary execution.

---

### Stack & Contact

* **Languages & Core:** Python, C++20, `pybind11`, SQL
* **AI & Eval Infra:** Inspect, TruLens, Opik, PyRIT, OpenInference

Found a bug in one of my tools or want to talk about eval reliability? Feel free to open an issue in the respective repo or reach out on [LinkedIn](YOUR_LINKEDIN_URL).
