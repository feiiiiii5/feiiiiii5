## Hi there 👋

I'm **fei** — an undergraduate student at **Sun Yat-sen University (中山大学)**, majoring in **Cybersecurity (网络空间安全)**. I'm preparing for 27fall US master's applications in CS/AI.

### 🔭 Currently working on

I'm contributing to open-source AI/ML infrastructure projects — focusing on **event-sourced queue systems**, **LLM evaluation harnesses**, and **Python ML tooling**. My goal is to ship production-quality fixes that maintainers actually merge, not just PR volume.

### 🌱 Recent contributions

#### Merged PRs

- **[langwatch/langwatch](https://github.com/langwatch/langwatch)** — TypeScript event-sourcing queue system
  - `#5738` fix(model-providers): prefer enabled row over narrower-scope disabled row in collapse (#5575) — fixed a model provider collapse bug where a narrower-scope disabled row could shadow a broader enabled row
  - `#5739` fix(traces): hoist langwatch.labels from resource attrs in trace accumulation — fixed silent metadata drop in trace accumulation

- **[rhesis-ai/rhesis](https://github.com/rhesis-ai/rhesis)** — Python testing framework for LLM systems
  - `#2156` chore(backend): remove dead code for dimensions and demographics

#### Open PRs in active review

- **[langwatch/langwatch](https://github.com/langwatch/langwatch)** — `#5883` fix(group-queue): skip already-dropped siblings in restageDrainedSiblings (#5857) — fixes a job resurrection bug where already-dropped siblings get re-staged, re-dispatched, and re-dropped on every retry cycle, inflating the drop counter and re-running side effects on terminal payloads

- **[dottxt-ai/outlines](https://github.com/dottxt-ai/outlines)** — `#1933` fix(vllm): don't mutate caller's extra_body across VLLM/AsyncVLLM calls — fixes a silent cross-call leakage where `structured_outputs` config from one call bleeds into the next, causing data corruption in structured generation

- **[BerriAI/litellm](https://github.com/BerriAI/litellm)** — `#33653` fix(logging): stabilize StandardLoggingPayload.model across success and failure paths — ensures logging payload shape consistency so downstream observability pipelines don't break on failure paths

- **[EleutherAI/lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness)** — `#3939` fix(vllm-vlm): pass tokenize=False to processor.apply_chat_template — fixes a crash with OpenGVLab/InternVL3-2B where `AutoProcessor.from_pretrained` returns a `Tokenizer` (not `ProcessorMixin`) whose `apply_chat_template` defaults to `tokenize=True`

- **[Giskard-AI/giskard-oss](https://github.com/Giskard-AI/giskard-oss)** — `#2614` fix(llm): warn on unknown Anthropic completion params — mirrors the OpenAI translator's warning behavior so dropped params are surfaced to users

- **[NVIDIA/garak](https://github.com/NVIDIA/garak)** — `#1942` feat: show probe name in detector progress bar — UX improvement for long-running LLM vulnerability scans

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** — `#2526` fix: evaluation step field preservation

- **[rhesis-ai/rhesis](https://github.com/rhesis-ai/rhesis)** — `#2176` & `#2177` frontend field preservation fixes

### 🛠️ Tech stack

- **Languages**: Python, TypeScript, JavaScript, C++
- **Backend**: FastAPI, Node.js, Fastify, ClickHouse, Redis, PostgreSQL
- **AI/ML**: Hugging Face Transformers, vLLM, LiteLLM, PyTorch, structured generation (outlines)
- **Frontend**: React, Next.js
- **Tooling**: Git (SSH signing), GitHub CLI (`gh`), Docker, testcontainers, vitest, pytest
- **Infra**: macOS (Apple Silicon), SSH over 443, structured logging, observability (OpenTelemetry)

### 📚 What I'm learning

- Distributed queue systems (Redis + Lua + ClickHouse event-sourcing patterns)
- LLM evaluation methodology (bias probes, structured generation correctness, multimodal eval)
- TypeScript type-level programming (generic constraints on queue definitions)
- Open-source contribution workflow (4-stage pipeline: project-finder → deep-research → issue-fix → pr-readiness, with skeptical-reviewer subagent gate)

### 📫 How to reach me

- GitHub: [@feiiiiii5](https://github.com/feiiiiii5)
- Email: `204683769+feiiiiii5@users.noreply.github.com`

### ⚡ Fun fact

Every PR I open goes through a 4-stage pipeline: deep research (architecture + issue/PR history + conflict-risk assessment) → surgical fix → skeptical-reviewer subagent (adversarially traces data flow and tries to break the fix before submission). The reviewer has caught multiple false-green tests that would have shipped regressions.

---

> "Test input parameters decide which code path runs — a green test means nothing if it didn't actually exercise the bug." — lesson from langwatch #5857 workflow

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/TypeScript-007ACC?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch" />
  <img src="https://img.shields.io/badge/macOS-000000?style=flat-square&logo=apple&logoColor=white" alt="macOS" />
</p>
