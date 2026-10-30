# Hi, I'm Yufeiyang 👋

I'm an independent developer, tech enthusiast and undergraduate at Sun Yat-sen University. My work focuses on **AI evaluation and tools for AI agents**. I'm especially interested in bugs that make a system look successful when something underneath has failed.

## In the open-source community

I contribute fixes and regression tests, and work with maintainers through review. A few examples:

- **[Inspect Evals](https://github.com/UKGovernmentBEIS/inspect_evals/pull/2132):** preserve individual benchmark attempts when computing HLE confidence calibration, so averaging repeated runs doesn't hide confidently wrong answers.
- **[Serena](https://github.com/oraios/serena/pull/2030):** fail pending requests promptly when a write to the language server fails, instead of leaving them waiting for a timeout.
- **[TruLens](https://github.com/truera/trulens/blob/main/MAINTAINERS.md#area-triagers):** Area Triager for feedback functions and metrics, helping with issue and pull request triage.

## Projects I'm working on

**[failroute](https://github.com/feiiiiii5/failroute)** is a released Python tool for finding exception handlers that can hide failures behind normal-looking results. Its repository includes the CLI, tests and a public manuscript examining which of its candidate locations are also flagged by existing code checkers. A candidate is a place to investigate, not a confirmed bug.

**[rewardfail](https://github.com/feiiiiii5/rewardfail)** studies failures in reinforcement learning reward software. In controlled tests, changing where a math-checker failure appeared within a batch changed the outcome from an unflagged zero reward to a batch exception. The repository includes a public manuscript, experiments and a local prototype for keeping reward values and failure information aligned. The study does not include model training.

I originated failroute and selected rewardfail's research question and methods. AI coding agents assist implementation, testing, experiments, analysis and drafting. Both manuscripts are public and have not been peer reviewed.

## Let's talk

Questions, suggestions and collaboration ideas are welcome. If you try one of my tools or spot something I could improve, I'd love to hear about it through a repository issue or [LinkedIn](https://www.linkedin.com/in/yufeiyang-chen-a2167143b/).
